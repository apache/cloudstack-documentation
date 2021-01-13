About Virtual Appliances
------------------------

CloudStack allows users to deploy virtual appliances on VMware such as its been made directly though vCenter.
Vendors of virtual appliances for VMware often produce ‘templates’ of their appliances in an OVA format.
An OVA file contain disc images, as well as the configuration data of the virtual appliance and also at times a EULA which must be acknowledged.
Virtual Appliances are supported only on VMware.

Deployment options (configurations)
-----------------------------------

VMware templates can provide different deployment options in their OVF descriptor file. CloudStack obtains
the different deployment options when the template is registered and it displays them to the users
in the virtual machine deployment wizard, under the 'Compute Offering' section.

After the user selects a deployment option, CloudStack lists the compute offerings which match or exceed the
deployment options hardware requirements for CPU and memory.

.. note::
    All the custom unconstrained compute offerings are displayed, but only those constrained custom offerings
    in which the maximum or minimum requirements for CPU and memory are supported by the selected deployment option.

.. |vapps-deployment-opts.png| image:: /_static/images/vapps-deployment-opts.png
.. |vapps-eulas.png| image:: /_static/images/vapps-eulas.png
.. |vapps-networks.png| image:: /_static/images/vapps-networks.png
.. |vapps-properties.png| image:: /_static/images/vapps-properties.png

The 'Compute Offering' section will be similar to this:
      |vapps-deployment-opts.png|


Network interfaces
------------------

In case the template requires the virtual appliance to connect different network interfaces, these are displayed in the 'Networks' section, similar to this:

|vapps-networks.png|


Properties
----------

If the template contains properties that require the user input, those are being displayed on the 'Properties' section, similar to this:

|vapps-properties.png|


End-user license agreements
---------------------------

If the template contains one or more end-user license agreements, the user must accept them prior to deploy their virtual appliance.
If the license agreements are not accepted, then it is not possible to deploy a virtual appliance.

|vapps-eulas.png|
