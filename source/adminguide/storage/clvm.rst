.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information#
   regarding copyright ownership.  The ASF licenses this file
   to you under the Apache License, Version 2.0 (the
   "License"); you may not use this file except in compliance
   with the License.  You may obtain a copy of the License at
   http://www.apache.org/licenses/LICENSE-2.0
   Unless required by applicable law or agreed to in writing,
   software distributed under the License is distributed on an
   "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the
   specific language governing permissions and limitations
   under the License.

From CloudStack 4.23 onwards, CloudStack supports two types for Clustered Logical Volume Manager (CLVM) primary storage:
- CLVM: LVM volumes with RAW format
- CLVM_NG (Next Generation): LVM volumes with QCOW2 format that supports advanced features.

Both use the same underlying infrastructure:
- `lvmlockd` daemon for lock management
- `sanlock` for distributed locking
- Shared volume groups across cluster hosts

The key difference is the disk image format used on top of the LVM volumes which enabled different feature sets.

CLVM (RAW format):
~~~~~~~~~~~~~~~~~~

- Logical volumes are formatted as RAW disk images
- Provides basic block storage functionality
- Suitable for workloads that do not require advanced features

Advantages:

- Slightly better performance (no QCOW2 overhead)
- Simpler storage stack

Disadvantages:

- No incremental snapshots - always full copy
- Larger snapshot storage requirements
- Slower snapshot operations
- Higher secondary storage bandwidth usage

.. note:: 
The original CLVM implementation used the clvmd (Clustered LVM daemon) along with corosync/pacemaker for cluster coordination. This technology has been deprecated in modern Linux distributions (RHEL 8+, Ubuntu 20.04+). CloudStack's current implementation uses the modern lvmlockd + sanlock stack, which is more reliable. This same modern infrastructure is shared with CLVM_NG - the only difference between CLVM and CLVM_NG is the disk image format (RAW vs QCOW2), not the locking mechanism.

CLVM_NG (QCOW2 format):
~~~~~~~~~~~~~~~~~~~~~~~

- Logical volumes are formatted as QCOW2 disk images
- QCOW2 layer provides advanced features like:
  - Incremental snapshots (only changes since last snapshot)
  - Linked clones
- Still benefits from LVM volume management

**Advantages:**

- **Incremental snapshots** with dirty bitmaps
- Reduction in snapshot storage
- Faster snapshot operations
- Reduced secondary storage bandwidth
- Persistent bitmap tracking

**Disadvantages:**

- Slight performance overhead from QCOW2 layer
- More complex storage stack
- Bitmaps lost during volume migration - hence the next snapshot will be a full snapshot (but subsequent snapshots will be incremental again)

Key features
~~~~~~~~~~~~

Incremental Snapshots with QCOW2 bitmaps (CLVM_NG only)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CLVM_NG supports incremental snapshots using QCOW2's bitmap feature. When a snapshot is taken, a bitmap is created to track which blocks have changed since the last snapshot.

CLVM (RAW format) always performs full snapshots, copying all data regardless of changes, which results in larger snapshot sizes and longer snapshot times.

Exclusive volume locking
^^^^^^^^^^^^^^^^^^^^^^^^^

CLVM/CLVM_NG use `lvmlockd` and `sanlock` to provide exclusive locking of logical volumes across cluster hosts. This ensures data integrity and prevents concurrent access issues.

- **Active Volumes**: Locked exclusively on the host running the VM
- **Inactive Volumes**: Can be in shared mode or deactivated
- **Lock Transfer**: Automatic during VM migration
- **Lock Tracking**: CloudStack tracks which host owns each volume lock

Lightweight Migration
^^^^^^^^^^^^^^^^^^^^^

When migrating VMs between pools on the same volume group:

- **No Data Copy**: Volume stays in same VG, only lock is transferred
- **Zero Network Traffic**: No data movement required
- **Same VG Required**: Source and destination pools must use same VG

Physical Extents (PEs) and Size Calculation for CLVM_NG
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

LVM divides physical volumes into **Physical Extents (PEs)** - the smallest allocatable unit of storage:

- **Default PE Size**: 4 MiB (4096 KiB)
- **Configurable Range**: 1 KiB to 16 GiB (power of 2)
- **Impact**: All LVM allocations are rounded up to PE boundaries

**Example:**

.. code-block:: text

   Requested: 10.5 GB volume
   PE Size: 4 MiB
   Calculation: ceil(10.5 GB / 4 MiB) = ceil(2688) = 2688 PEs
   Actual Size: 2688 × 4 MiB = 10.5 GB (exactly)

QCOW2 metadata overhead
^^^^^^^^^^^^^^^^^^^^^^^

CLVM_NG uses QCOW2 format on LVM volumes, which adds metadata overhead. The actual disk usage may be higher than the requested size due to QCOW2's internal structures, especially when snapshots are involved. This is important to consider when planning storage capacity for CLVM_NG pools.

**QCOW2 Metadata Components:**

1. **QCOW2 Header**: 72 bytes minimum (usually one cluster = 64 KiB)
2. **L1 Table**: References L2 tables (grows with volume size)
3. **L2 Tables**: Map clusters to physical storage
4. **Refcount Tables**: Track cluster reference counts
5. **Bitmaps**: For incremental snapshots (optional)

Size Calculation for CLVM_NG Volumes
"""""""""""""""""""""""""""""""""""""

When creating CLVM_NG volumes, CloudStack accounts for:

1. **Requested Virtual Size**: The size visible to the VM
2. **QCOW2 Metadata**: Overhead for QCOW2 structures
3. **PE Alignment**: Round up to PE boundaries

Checking Volume Sizes
""""""""""""""""""""""

.. code-block:: bash

   # Check LVM volume size (physical)
   lvs -o lv_name,lv_size /dev/vgname/volumename

   # Check QCOW2 virtual size
   qemu-img info /dev/vgname/volumename

Backing File Support in CLVM_NG
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CLVM_NG supports **QCOW2 backing files** for template-based volume creation, enabling efficient template deployment and linked clones:

**How It Works:**
1. **Template Volume**: Created as QCOW2 on CLVM_NG pool
2. **Backing File**: Template volume becomes backing file (base image)
3. **Child Volume**: New VM volumes reference template, store only differences
4. **Copy-on-Write (CoW)**: Modified blocks stored in child volume, reads fall through to backing file

**Benefits:**
- **Space Savings**: Multiple VMs share single template image
- **Fast Deployment**: VM creation in seconds (no full copy needed)
- **Efficient Storage**: Only differences (deltas) consume space

When deploying a VM from a template on CLVM_NG:

.. code-block:: text

   1. Template registered in CloudStack
      ↓
   2. Template stored as QCOW2 in CLVM_NG pool
      /dev/vgname/template-uuid
      ↓
   3. User deploys VM from template
      ↓
   4. CloudStack creates child volume with backing file
      lvcreate -L <size> -n vm-volume-uuid vgname
      qemu-img create -f qcow2 -F qcow2 -b /dev/vgname/template-uuid /dev/vgname/vm-volume-uuid
      ↓
   5. VM starts using child volume
      (reads from template, writes to child)

Global Settings
~~~~~~~~~~~~~~~

clvm.secure.zero.fill
^^^^^^^^^^^^^^^^^^^^^

- **Type:** Boolean
- **Default:** `false`
- **Scope:** Storage Pool
- **Category:** Advanced
- **Description:** When enabled, CLVM volumes are zero-filled at deletion time to prevent data recovery by VMs reusing the space, as thick LVM volumes write data linearly
- **Impact:** 
  - Enabled: Volumes are securely wiped on deletion (slower deletion, more secure)
  - Disabled: Fast deletion, but data may be recoverable
- **Propagation:** Setting is propagated to hosts when they connect to the storage pool. Changing requires disconnecting/reconnecting hosts or restarting KVM agent
- **Recommendation:** Enable for environments with strict security/compliance requirements (PCI-DSS, HIPAA). Disable for performance-critical environments where deletion speed matters more than data security
- **Use Case:** Production environments handling sensitive data, multi-tenant environments with strict data isolation requirements

For incremental snapshots to work with CLVM_NG enabled the `kvm.incremental.snapshot` global setting must also be set to `true`.

VM snapshots are currently not supported on CLVM/CLVM_NG volumes.

Setting up Clustered LVM on CloudStack KVM hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configure shared storage using iSCSI, Fibre Channel, or shared SAS/NVMe devices.

Install `lvm2` and `sanlock` packages on all cluster hosts that will access the CLVM storage pool.

```
# Example for OL9
dnf install lvm2-lockd sanlock -y
systemctl enable sanlock --now
systemctl enable lvmlockd --now

# Update /etc/lvm/lvm.conf to set use_lvmlockd = 1
# Update /etc/lvm/lvmlocal.conf set host_id to a unique value for each host (e.g. hostname or IP or ID (1, 2, 3...))
```

Just on one of the hosts, initialize the shared physical volume (PV) that will be used for CLVM storage pools and start the VG in shared mode:

```
pvcreate /dev/sdb # Initialize the shared physical volume (replace with actual device)
vgcreate --shared --lock-type sanlock sharedvg /dev/sdb
```

On all other hosts, perform the following:
```
lvmdevices --adddev /dev/sdb # adds the disk to /etc/lvm/devices/system.devices
vgchange lockstart sharedvg # Start the VG in shared mode
```
