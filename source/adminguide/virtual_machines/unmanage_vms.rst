About Unmanaged Virtual Machines
--------------------------------

As of ACS 4.14, CloudStack has the concept of **unmanaged** virtual machines.  These are virtual machines that are on CloudStack
managed hosts, but that are not in CloudStack's database and therefore CloudStack cannot control (manage) then in any way.  Previously,
such VMs could exist, but CloudStack did not 'see' them (their existence *would* be reported in logs as unrecognised VMs).

From ACS 4.14 onwards, CloudStack is able to list these VMs via the listUnmanagedInstances API command and then import (also known as ingest)
those unmanaged VMs via the importUnmanagedInstance API so that they become CloudStack managed guest instances

From ACS 4.15 onwards, administrators are able to unmanage guest virtual machines.

.. note:: This is currently only available for **vSphere** clusters.

Unmanaging Virtual Machines via API
-----------------------------------

Administrators are able to unmanage guest virtual machines from CloudStack. Once unmanaged, CloudStack can no longer monitor, control or administer the provisioning and orchestration related operations on a virtual machine.

To unmanage a guest virtual machine, an administrator must invoke the unmnageVirtualMachine API passing the ID of the virtual machine to unmanage. The API has the following preconditions:

- The virtual machine must not be destroyed
- The virtual machine state must be 'Running’ or ‘Stopped’
- The virtual machine must be a VMware virtual machine

The API execution will perform the following pre-checks, failing if they are not met:

- There are no volume snapshots associated with any of the virtual machine volumes
- There is no ISO attached to the virtual machine

.. note:: This is currently only available for **vSphere** clusters.


Preserving unmanaged virtual machine NICS
-----------------------------------------

The zone setting: unmanage.vm.preserve.nics can be used to preserve virtual machine NICs and its MAC addresses after unmanaging them. If set to true, the virtual machine NICs (and their MAC addresses) are preserved when unmanaging it. Otherwise, NICs are removed and MAC addresses can be reassigned.


Unmanaging virtual machine actions
----------------------------------

- Clean up virtual machine NICs and deallocate network resources used such as IP addresses and DHCP entries on virtual routers.

   - If ‘unmanage.vm.preserve.nics’ = ‘false’ then the NICs are deallocated and removed from CloudStack

   - If ‘unmanage.vm.preserve.nics’ = ‘true’ then the NICs remain allocated and are not removed from the database. The NIC’s MAC addresses remain preserved and therefore cannot be assigned to any new NIC.

- Clean up virtual machine volumes in the CloudStack database

- Clean up virtual machine snapshots in the CloudStack database (if any) · Revoke host access to any managed volumes attached to the VM

- Clean up the virtual machine from the following:

   - Remove the virtual machine from security groups (if any)

   - Remove the virtual machine from instance groups (if any)

   - Remove firewall rules for the virtual machine (if any)

   - Remove forwarding rules for the virtual machine (if any)

   - Remove load balancing rules for the virtual machine (if any)

   - Disable static NAT (if the virtual machine is assigned to it)

   - Remove the virtual machine from affinity groups (if any)

- Set VM details as removed in the CloudStack database

- Decrement the account resources count for volumes and virtual machines

- Generate usage events:

   - For volumes destroyed, with type: ‘VOLUME.DELETE’

   - For virtual machine snapshots destroyed (if any), with type: ‘VMSNAPSHOT.DELETE’
   
   - For virtual machine NICs destroyed: with type: ‘NETWORK.OFFERING.REMOVE’
   
   - For the virtual machine being unmanaged: stopped and destroyed usage events (similar as the generated usage events when expunging a virtual machine), with types: ‘VM.STOP’ and ‘VM.DESTROY