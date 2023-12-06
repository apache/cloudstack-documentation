Converting a Hyper-V Instance to a Template
-------------------------------------------

To convert a Hyper-V Instance to a XenServer-compatible CloudStack Template,
you will need a standalone XenServer host with an attached NFS VHD SR.
Use whatever XenServer version you are using with CloudStack, but use
XenCenter 5.6 FP1 or SP2 (it is backwards compatible to 5.6).
Additionally, it may help to have an attached NFS ISO SR.

For Linux Instances, you may need to do some preparation in Hyper-V before
trying to get the Instance to work in XenServer. Clone the Instance and work on the
clone if you still want to use the Instance in Hyper-V. Uninstall Hyper-V
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

The next step is make sure the Instance is not running in Hyper-V, then get
the VHD into XenServer. There are two options for doing this.

Option one:

#. Import the VHD using XenCenter. In XenCenter, go to Tools>Virtual
   Appliance Tools>Disk Image Import.

#. Choose the VHD, then click Next.

#. Name the Instance, choose the NFS VHD SR under Storage, enable "Run
   Operating System Fixups" and choose the NFS ISO SR.

#. Click Next, then Finish. An Instance should be created.

Option two:

#. Run XenConvert, under From choose VHD, under To choose XenServer.
   Click Next.

#. Choose the VHD, then click Next.

#. Input the XenServer host info, then click Next.

#. Name the Instance, then click Next, then Convert. An Instance should be created.

Once you have an Instance created from the Hyper-V VHD, prepare it using the
following steps:

#. Boot the Instance, uninstall Hyper-V Integration Services, and reboot.

#. Install XenServer Tools, then reboot.

#. Prepare the Instance as desired. For example, run sysprep on Windows Instances.
   See `“Creating a Windows
   Template” <#creating-a-windows-template>`_.

Either option above will create an Instance in HVM mode. This is fine for
Windows Instances, but Linux Instances may not perform optimally. Converting a Linux
instance to PV mode will require additional steps and will vary by
distribution.

#. Shut down the instance and copy the VHD from the NFS storage to a web
   server; for example, mount the NFS share on the web server and copy
   it, or from the XenServer host use sftp or scp to upload it to the
   web server.

#. In CloudStack, create a new Template using the following values:

   -  URL. Give the URL for the VHD

   -  OS Type. Use the appropriate OS. For PV mode on CentOS, choose
      Other PV (32-bit) or Other PV (64-bit). This choice is available
      only for XenServer.

   -  Hypervisor. XenServer

   -  Format. VHD

The Template will be created, and you can create instances from it.
