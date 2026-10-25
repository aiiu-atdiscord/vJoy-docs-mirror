# vJoyConf

<small>Original archived at: https://web.archive.org/web/20180226075826/http://vjoystick.sourceforge.net/site/index.php/utilities-218/vjoyconf</small>

vJoyConf enables you to:

- Add a vJoy Device (Up to 16 devices)
- Remove a vJoy Device
- Disable vJoy devices (as bulk)
- Enable vJoy devices (as bulk)
- Configure an individual device:
    - Select which axes the device supports (Up to 8)
    - Set the number of buttons (Up to 128)
    - Set the number and type of POV Hats (Up to 4)
    - Select which FFB effects are supported (None to 11)

## Operations

### Device Status

By selecting a tab you can get information about the selected device and about the vJoy driver.

The tab background tells you if the device exists or may be added.

![](<vJoyConf Status.png>)

### Add/Remove Device

You can **add** a new device by selecting a tab (white background) and press button "Add Device". A new device will be created, the tab’s background will become green once the device is ready for use.

You can **delete** an existing device selecting a tab (green background) and press button "Delete Device". The device will be removed from the system,  the tab’s background will become white once the device is finally removed.

### Enable/Disable vJoy

It is sometimes useful to temporarily remove all vJoy devices then restore the original vJoy configuration. This is done by disabling and enabling vJoy driver. Use checkbox "Enable vJoy".

### Reset All

You can always reset vJoy configuration to its initial state - Device #1 configured to default configuration by pressing button "Reset All".

> [!CAUTION]
> All device configurations will be lost.

### Configure an individual device

Once a device has been created, you may change its configuration. The changes will take place only after pressing button "Apply". Once pressed, the device will be disabled then enabled in order for the changes to take effect.

#### Add/Remove buttons

Any number between 0 and 128 may be entered.

![](<vJoyConf buttons.jpg>)

#### Add/Remove Axes

Any of the 8 axes can be added or removed from the device.

![](<vJoyConf - axes.jpg>)

#### Add/Remove POV hat switches

You can set up to 4 switches. You should select which type of POV hat switches you need:

- 4 Directions - This type of switch can point to all 4 directions (North, East, South, West) or to be in neutral state.
- Continuous - This type of switch can point to all directions (360 degrees) or to be in neutral state.

Note: You cannot mix between types.

![](<vJoyConf - pov.jpg>)

#### FFB Support

If you want a vJoy device to support FFB effects you have to select checkbox "Enable Effects" and to select the required effects.

In most cases, support for FFB is not required. However, by selecting an FFB effect to render device #16 unusable (See tab).

![](<vJoyConf - FFB.jpg>)
