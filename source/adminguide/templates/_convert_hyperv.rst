Converting a Hyper-V VM to a Template
-------------------------------------

To convert a Hyper-V VM to a XenServer-compatible CloudStack template,
you will need a standalone XenServer host with an attached NFS VHD SR.
Use whatever XenServer version you are using with CloudStack, but use
XenCenter 5.6 FP1 or SP2 (it is backwards compatible to 5.6).
Additionally, it may help to have an attached NFS ISO SR.

For Linux VMs, you may need to do some preparation in Hyper-V before
trying to get the VM to work in XenServer. Clone the VM and work on the
clone if you still want to use the VM in Hyper-V. Uninstall Hyper-V
Integration Components and check for any references to device names in
/etc/fstab:

#. From the linux\_ic/drivers/dist directory, run make uninstall (where
   "linux\_ic" is the path to the copied Hyper-V Integration Components
   files).

#. Restore the original initrd from backup in /boot/ (the backup is
   named \*.backup0).

#. Remove the "hdX=noprobe" entries from /boot/grub/menu.lst.

#. Check /etc/fstab for any partitions mounted by device name. Change
   those entries (if any) to mount by LABEL or UUID. You can get that
   information with the blkid command.

The next step is make sure the VM is not running in Hyper-V, then get
the VHD into XenServer. There are two options for doing this.

Option one:

#. Import the VHD using XenCenter. In XenCenter, go to Tools>Virtual
   Appliance Tools>Disk Image Import.

#. Choose the VHD, then click Next.

#. Name the VM, choose the NFS VHD SR under Storage, enable "Run
   Operating System Fixups" and choose the NFS ISO SR.

#. Click Next, then Finish. A VM should be created.

Option two:

#. Run XenConvert, under From choose VHD, under To choose XenServer.
   Click Next.

#. Choose the VHD, then click Next.

#. Input the XenServer host info, then click Next.

#. Name the VM, then click Next, then Convert. A VM should be created.

Once you have a VM created from the Hyper-V VHD, prepare it using the
following steps:

#. Boot the VM, uninstall Hyper-V Integration Services, and reboot.

#. Install XenServer Tools, then reboot.

#. Prepare the VM as desired. For example, run sysprep on Windows VMs.
   See `“Creating a Windows
   Template” <#creating-a-windows-template>`_.

Either option above will create a VM in HVM mode. This is fine for
Windows VMs, but Linux VMs may not perform optimally. Converting a Linux
VM to PV mode will require additional steps and will vary by
distribution.

#. Shut down the VM and copy the VHD from the NFS storage to a web
   server; for example, mount the NFS share on the web server and copy
   it, or from the XenServer host use sftp or scp to upload it to the
   web server.

#. In CloudStack, create a new template using the following values:

   -  URL. Give the URL for the VHD

   -  OS Type. Use the appropriate OS. For PV mode on CentOS, choose
      Other PV (32-bit) or Other PV (64-bit). This choice is available
      only for XenServer.

   -  Hypervisor. XenServer

   -  Format. VHD

The template will be created, and you can create instances from it.
