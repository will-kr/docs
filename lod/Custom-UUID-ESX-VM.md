---
title: "Configure an ESX VM with a UUID"
description: "Assign a custom unique ID to a virtual machine hosted on an ESX host."
isPublished: false
---
# Configure an ESX VM with a UUID

If you would like to assign a custom unique ID to a virtual machine hosted on an ESX host, you can configure this on in the VM profile in Skillable Studio.

There are two types of unique IDs that can be configured:

- BIOS GUID
- UUID

## In this Article

- [Configure a BIOS GUID]
- [Configure a Custom UUID]
    - [Configuration in the VM Profile]



## BIOS GUID

This controls the BIOS GUID set within the virtual machine's configuration. The value should include the curly braces. 

An example BIOS GUI looks like 

```nocopy
{46486DC1-B2A6-456E-B091}
```

## Custom UUID

This controls the UUID set within the virtual machine's configuration. The UUID is a 128-bit integer. The 16 bytes of this value are separated by spaces, except for a dash between the eighth and ninth hexadecimal pairs.

An example UUID looks like

```nocopy
00 11 22 33 44 55 66 77 88 99 aa bb cc dd ee ff
```

## Configuration in the VM Profile

![](images/bios-guid-uuid.png)

To configure a BIOS GUID or a custom UUID:

1. Navigate to the VM profile you wish to configure.
1. Click **Edit** in the upper-right corner.
1. Click the **Advanced** tab.
1. Enter the BIOS GUID or UUID that you wish to use.
1. **Allow disk updates in lab console (enabled by default)**: This allows authors to access the Save Differencing Disks dialog, when using this virtual machine.
1. **Connect via remote desktop connection (external to lab console)**: You can supply an RDP file and have users connect directly to the VM using an RDP client instead of using our HTML5 controller. This requires public IP configurations.

## Best Practices

### VM has been Moved or Copied

When you power on a virtual machine that was moved or copied to a new location, the following message usually appears:

1. The virtual machine's configuration file has changed its location since its last poweron. Do you want to create a new unique identifier (UUID) for the virtual machine or keep the old one?
    - Create
    - Keep
    - Always Create
    - Always Keep
 
 2. Question (id = 0) : msg.uuid.altered: This virtual machine might have been moved or copied.

    In order to configure certain management and networking features, VMware ESXi needs to know if this virtual machine was moved or copied.

    If you don't know, answer "I copied it".

    - Cancel
    - I moved it
    - I copied it

If you moved this virtual machine, you can choose to keep the UUID. Select **Keep/I moved it**, then click **OK** to continue powering on the virtual machine.

If you copied this virtual machine to a new location, you should create a new UUID since the copy of the virtual machine is using the same UUID as the original virtual machine. Select **Create/I copied it**, then click **OK** to continue powering on the virtual machine.

If the original virtual machine is being used as a template for more virtual machines, you can choose to create a new UUID the first time you power on each copy. After you configure the virtual machine and are ready to make it a template, move it to a new location and power it on. When the message appears after you power on, select **Always Create**, then click **OK** to continue powering on the virtual machine. The virtual machine is set up to create a new UUID every time it is moved. Power off the virtual machine and begin using it as a template by copying the virtual machine files to other locations.

If you intend to move the virtual machine numerous times and want to keep the same UUID each time the virtual machine moves, select **Always Keep** and click **OK** to continue powering on the virtual machine.

**Note:** If you want to change the Always Keep or Always Create setting, power off the virtual machine and edit its configuration (.vmx) file. Delete the line that contains uuid.action = "create" or uuid.action = "keep".

For more information, see VMware's documentation on [editing a .vmx file.](https://kb.vmware.com/s/article/1714)
