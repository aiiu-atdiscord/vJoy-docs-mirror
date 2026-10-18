# vJoyConfig

https://web.archive.org/web/20180226075826/http://vjoystick.sourceforge.net/site/index.php/utilities-218/vjoyconfig

vJoyConfig is a command-line configuration utility.

It has all the capabilities that [vJoyConf](vjoyconf.md) has:

- Add a vJoy Device (Up to 16 devices)
- Remove a vJoy Device
- Disable vJoy devices (as bulk)
- Enable vJoy devices (as bulk)
- Configure an individual device:
    - Select which axes the device supports (Up to 8)
    - Set the number of buttons (Up to 128)
    - Set the number and type of POV Hats (Up to 4)
    - Select which FFB effects are supported (None to 11)

## Advantages

May be ran from batch file

Faster way to configure multiple devices.

## Disadvantages

Indication of device status - text mode only.

Unfriendly syntax.

## Operations

This section will guide you through the most useful operations. For full syntax go to this [page](vjoyconfig-syntax.md).

Open a command window (DOS Window) as **administrator** use vJoyConfig. 

### Getting Information

To learn which devices are already configured:

`vJoyConfig -t`

The output will list the devices and their statuses. The header will list some general information regarding the driver:

```
C:\Program Files\vJoy\x64>vJoyConfig -t

Product ID: vJoy - Virtual Joystick
Manufacturer ID: Shaul Eizikovich
Version Number: 2.1.6
(VendorID:0x1234 ProductID:0xBEAD VersionNumber:0x0216)
Device 1:       Status: BUSY
Device 2:       Status: MISSING
Device 3:       Status: FREE
Device 4:       Status: MISSING
Device 5:       Status: MISSING
Device 6:       Status: MISSING
Device 7:       Status: MISSING
Device 8:       Status: MISSING
Device 9:       Status: MISSING
Device 10:      Status: MISSING
Device 11:      Status: MISSING
Device 12:      Status: MISSING
Device 13:      Status: MISSING
Device 14:      Status: MISSING
Device 15:      Status: MISSING
Device 16:      Status: MISSING
```
_Example 1_

The above example shows a system where there are two devices:

Device #1 is BUSY - Meaning that it has been acquired by some feeder.\
Device #3 is FREE - Meaning that it has not been acquired.

---------------------------------------------------------------------------------------------------

To get the configuration of a device, indicate the device number:

`vJoyConfig -t  1 3`

The output will be a human-readable list of all controls that has been configured, per device:

```
C:\Program Files\vJoy\x64>vJoyConfig -t  1 3
 
========================================================================
Device:                 1
State:                  BUSY
Buttons:                2
Descrete POVs:          0
Continous POVs:         0
Axes:                   X - Z Rx Ry - - -
FFB Effects:            All Effects
========================================================================
 
========================================================================
Device:                 3
State:                  FREE
Buttons:                8
Descrete POVs:          0
Continous POVs:         0
Axes:                   X Y Z Rx Ry Rz Sl0 Sl1
FFB Effects:            None

========================================================================
```

_Example 2_

The above example shows information for devices #1 and #3:

Device #1 is busy, has 2 buttons, no POVs and supports only 4 axes. If addition it supports all FFB effects.\
Device #3 is free, has 8 buttons, no POVs and supports all 8 axes. It does not supportl FFB effects.



By adding flag `-c`, you can get this data in a format that can be reused for configuration purposes:

```

C:\Program Files\vJoy\x64>vJoyConfig -t -c  1 3

vJoyConfig 1 -f -a X  Z Rx Ry    -b 2  -e all

vJoyConfig 3 -f -a X Y Z Rx Ry Rz Sl0 Sl1 -b 8
```

_Example 3_

---------------------------------------------------------------------------------------------------

### Adding a Device

Use vJoyConfig to **add** or **replace** a vJoy device.\
It is impossible to modify a device (e.g. add a button while maintaining the other controls).\
Replacing a device is done by removing a device if exists, then adding a device.\
When adding a device, you may override all, some or none of the defaults:

- **Axes**: All
- **Buttons**: 8
- **POV Switches**: 0
- **FFB Effects**: None

The minimal command to add a device will be:

`vJoyConfig 2`

This command adds device #2 (if does not already exist) with the default controls:

```
C:\Program Files\vJoy\x64>vJoyConfig 2
C:\Program Files\vJoy\x64>vJoyConfig -t 2
 
========================================================================
Device:                 2
State:                  FREE
Buttons:                8
Descrete POVs:          0
Continous POVs:         0
Axes:                   X Y Z Rx Ry Rz Sl0 Sl1
FFB Effects:            None

========================================================================
```

_Example 4_

If now we wish to change the controls of this device we will have to force an addition (because the device already exists) and to indicate the controls that are to be different from the default:

```
C:\Program Files\vJoy\x64>vJoyConfig 2 -f -a x y z rx -b 32

C:\Program Files\vJoy\x64>vJoyConfig -t 2
========================================================================
Device:                 2
State:                  FREE
Buttons:                32
Descrete POVs:          0
Continous POVs:         0
Axes:                   X Y Z Rx - - - -
FFB Effects:            None

========================================================================
```

_Example 5_

In the above example we forced (`-f`) replacement of an existing device #2 and we overridden the axis default (X Y Z Rx) and the button default to 32 buttons.

 

It is also possible to add FFB effects to the device.\
You can either activate all effects or a subset of the effect list.\
In the following example we modify device #2 to support all FFB effects:

```
C:\Program Files\vJoy\x64>vJoyConfig 2 -f -a x y z rx -b 32 -e all

C:\Program Files\vJoy\x64>vJoyConfig -t 2
========================================================================
Device:                 2
State:                  FREE
Buttons:                32
Descrete POVs:          0
Continous POVs:         0
Axes:                   X Y Z Rx - - - -
FFB Effects:            All Effects

========================================================================
```

_Example 6_

### Postponing Operation

Every addition or replacement of a vJoy device requires a restart of the vJoy Driver.

This is a lengthy operation.

You may postpone the restart to the last command by adding flag `-l` to all addition operations but the last one:

```
C:\Program Files\vJoy\x64>vJoyConfig 2 -l -f -a x y z rx -b 32

C:\Program Files\vJoy\x64>vJoyConfig 3 -l -f -a x y z rx -b 32

C:\Program Files\vJoy\x64>vJoyConfig 4    -f -a x y z rx -b 32
```

_Example 7_

### Removing Devices

Use vJoyConfig to **remove** a vJoy device, or even to reset the vJoy system to its default state:

To reset enter:

`vJoyConfig -r`

To remove one or more device, use flag `-d` and list the devices to remove. Removing all devices has the effect of reset.

```
Device 1:       Status: MISSING
Device 2:       Status: BUSY
Device 3:       Status: FREE
Device 4:       Status: FREE
Device 5:       Status: MISSING
Device 6:       Status: MISSING
Device 7:       Status: MISSING
Device 8:       Status: MISSING
Device 9:       Status: MISSING
Device 10:      Status: MISSING
Device 11:      Status: MISSING
Device 12:      Status: MISSING
Device 13:      Status: MISSING
Device 14:      Status: MISSING
Device 15:      Status: MISSING
Device 16:      Status: MISSING
C:\Program Files\vJoy\x64>vJoyConfig -d 23

C:\Program Files\vJoy\x64>vJoyConfig -t
Product ID: vJoy - Virtual Joystick
Manufacturer ID: Shaul Eizikovich
Version Number: 2.1.6
(VendorID:0x1234 ProductID:0xBEAD VersionNumber:0x0216)
Device 1:       Status: MISSING
Device 2:       Status: MISSING
Device 3:       Status: MISSING
Device 4:       Status: BUSY
Device 5:       Status: MISSING
Device 6:       Status: MISSING
Device 7:       Status: MISSING
Device 8:       Status: MISSING
Device 9:       Status: MISSING
Device 10:      Status: MISSING
Device 11:      Status: MISSING
Device 12:      Status: MISSING
Device 13:      Status: MISSING
Device 14:      Status: MISSING
Device 15:      Status: MISSING
Device 16:      Status: MISSING
```

_Example 8_

### Enable/Disable vJoy
It is sometimes useful to disable vJoy driver and the whole vJoy system altogether. Either if vJoy interfere with other components on your system or in order to speed up the configuration by eliminating unneeded settings.

Naturally, you also need to enable the vJoy driver.

To disable vJoy driver:

`vJoyConfig enable off`

to enable vJoy driver:

`vJoyConfig enable on`

## Common usage

It is useful to create a batch file that sets your system to a known state. One of the methods to do this is to configure vJoy devices using _vJoyConf_ (The graphical tool), record the setup using _vJoyConfig_ into a batch file and modify the batch file.

### Getting the current status:

The most effective way to do it is to log all devices into a batch file:

`vJoyConfig -t -c 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 > A.BAT`

A .BAT will be:

```batch
vJoyConfig 4 -f -a X Y Z Rx     -b 32 
vJoyConfig 5 -f -a X Y Z Rx     -b 32 
vJoyConfig 8 -f -a X Y Z Rx     -b 32 
vJoyConfig 9 -f -a X Y Z Rx     -b 32 
```

These are the state of the current system. You may edit this output as you wish. Then you can run the modified batch file on your target machine.

You may want to **duplicate** your system on the target machine, removing all other devices from the target machine or you may want to **replace** the above devices on the target machine leaving other devices untouched.

### Duplication

To duplicate you need first to reset the the configuration on the target machine then duplicate the current configuration. For efficiency reasons, diable vJoy before resetting and enable vJoy when done:

```batch
vjoyconfig   -r
vJoyConfig 4 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 5 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 8 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 9 -f    -a X Y Z Rx     -b 32
```

### Replacing

If you do not use `vJoyConfig -r` you will modify or add only the devices explicitly accessed:

```batch
vJoyConfig 4 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 5 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 8 -f -l -a X Y Z Rx     -b 32 
vJoyConfig 9 -f    -a X Y Z Rx     -b 32
```