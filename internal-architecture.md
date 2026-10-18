# Internal Architecture

https://web.archive.org/web/20180212163436/http://vjoystick.sourceforge.net/site/index.php/dev216/internal-architecture

## Overview

vJoy device driver is a Kernel Mode Driver Framework (KMDF) filter driver.

vJoy supports up to sixteen virtual joystick devices. Each device supports up to 128 buttons, up to 8 axes and up to 4 POV hat switches (Continuous or 5-state).

The type of each device is `hid_device_system_game` which represents a standard joystick device.

By default, the supplied installer installs the vJoy driver and one vJoy device (Device number 1) that is pre-configured to feature eight buttons and eight axes. Later, the number of devices, their serial number and their configuration can be changed. It is also possible to alter the installer to provide a different default set-up

## Who should read this article

This article assumes that you have a reasonable understanding of Windows device drivers. You may want to read this article in order to better understand the way vJoy works or if you intend to make changes in the code. If you are happy with the existing driver and you wish to write a feeder or modify the installer you can skip this article.

## installing or Enabling the Device Driver

The PNP manager always notifies vJoy driver when the driver is installed or enabled . This notification invokes a callback function (`vJoyEvtDeviceAdd`) that does the following:

1. Creates a filter device with compatible ID “hid_device_system_game”
2. Creates some queues to handle internal device control IRPs and read requests
3. Creates a Raw PDO device that will later handle sideband communication on behalf of the virtual devices.

Once the callback function returns, the system sends two internal IRPs (IOCTL_HID_GET_DEVICE_DESCRIPTOR & IOCTL_HID_GET_REPORT_DESCRIPTOR) to vJoy device driver. In reply to the first it returns the HID_DESCRIPTOR that tells the system very little besides the fact that this is an HID device. In reply to the second IRP the driver returns the updated HID_REPORT_DESCRIPTOR structure that hold the information about all virtual device: their number and their configuration.

The data in the HID_REPORT_DESCRIPTOR structure is updated when IRP IOCTL_HID_GET_REPORT_DESCRIPTOR is processed. The driver first searches the registry for data. If the registry does not contain valid data then the driver uses a hard-coded descriptor.

## Raw device

When the driver is installed, a Raw PDO device is created. The raw device acts as the driver's end in the sideband communication because Windows architecture prevents applications from directly communicate with a filter device.

The raw device is created with ID “vJoyRawPdo\0” and set as not exclusive (So that more than one feeder can access the devices). Once the raw device is created, sixteen (16) device interfaces to it are created. Every interface is of interface class GUID_DEVINTERFACE_VJOY (defined in file public.h) and each interface has a unique reference string: “Device_001” to “Device_016”.

The role of each of the 16 interfaces is to act as an interface for the corresponding virtual device. Using these interfaces the feeder can, through file vJoyInterface.dll, write position data to the corresponding virtual device.

Finally, the raw device is added as a static child of the FDO collection of children. It's siblings will later be the virtual devices.

![Two Virtual devices and one Raw device](<device manager - two vjoy devices.png>)

<sup>Two Virtual devices and one Raw device</sup>

## Communication

### internal IOCTLs

All standard system calls to a vJoy device such as HidD_GetAttributes, HidD_GetProductString and joyGetPosEx are translated by the system and the HID class driver to a set of HID Minidriver IOCTLs that are handled a callback function (vJoyEvtInternalDeviceControl) in source file hid.c.

The most important of these so-called internal IOCTLs is IOCTL_HID_READ_REPORT which represents the system request to get position data. On receiving this call, the request is re-queued and completes only when data is available. The completion of the request is done by the raw device in function vJoyCompleteReadReport().

It noteworthy to mention that this IOCTL is not aimed at a particular virtual device. Only in the return data the driver marks to which device the data corresponds.

Other internal IOCTLs such as IOCTL_HID_GET_DEVICE_DESCRIPTOR are treated locally by the FDO.

### Sideband

The position data of each virtual device is received from the feeder (via file vJoyInterface.dll). The virtual devices themselves are not part of the data path. Each device is represented by a corresponding device interface of the raw device.

Before starting any sideband communication between a feeder and one of the interfaces, a connection should be established. The feeder requests permission to create a file that corresponds to this interface. The request is granted if the corresponding device exists not in use already. The first condition prevents the feeder from writing to non-existing device while the latter ensures exclusive access to a device.

Once the connection was established, the feeder can send the position data in the form of JOYSTICK_POSITION structures. Every time the feeder needs to update the device, it sends an IOCTL with code LOAD_POSITIONS to the previously opened connection. The function that handles these requests (vJoy_EvtIoDeviceControlForRawPdo) extracts the destination virtual device from the file object associated with the request.

### Disabling the Device Driver

When disabling (or removing) the device driver must be accompanied by closing interfaces of the raw device. If the feeder fails to close its connections (in other words: close the corresponding files) the disabling process will fail.

One of the built-in features of device-interface is their ability to notify when they are about to go down. This feature is used by vJoyInterface.dll to detect cases that vJoy is disabling so it's interfaces are relinquished in time.