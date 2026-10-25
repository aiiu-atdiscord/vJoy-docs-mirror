# Initial Values

<small>Original archived at: https://web.archive.org/web/20180118155900/http://vjoystick.sourceforge.net/site/index.php/download-a-install/deployment216/86-deployment-216-1/126-initial-values</small>

## What are Initial Values

When a vJoy device is first created (either after installation or after it has been configured) its controls are in a predefined initial position. This position is stable until the first time a feeder starts feeding the device.

The default Initial Values of each of the device's controls are hardcoded in the vJoy driver code. However, you can override this configuration to set your own Initial Values.

## Default Values

Unless overridden, vJoy Device initial values are as follows:

|  Control | Value | Notes |
| --- | --- | --- |
| X Axis | 50% | Stick is centered |
| Y Axis | 50% | Stick is centered |
| Z Axis | 50% | Stick is centered |
| Other Axes | 0% | Stick Down |
| POV Hats | -1 | Neutral Position |
| Buttons | 0 | Not Pressed |

## Overriding Default Values

When a vJoy device is loaded (either after initialization or after being enabled), it reads certain registry entries to acquire its initial values.

### Cascading Initialization

For each control you can override the default initial value for the entire set of vJoy devices by setting a master value. You may also override this master value for individual vJoy devices. A control can be an axis (e.g. X), a POV Hat (POV1) or the entire set of buttons.

Example 1:

Assuming we set the following **master** values:

- Axis Z = 0%
- Axis RX = 25%
- Axis RY = 50%
-  POV3 = 90°

Also, we set the following values for **Device #3**:

- Axis Z = 30%
- Axis RZ = 60%

Now we add vJoy **Device #2** which has 8 axes and 4 POV Hats. The initial values of its controls will be:

- Axis X = 50% (Default value, not overridden)
- Axis Y = 50% (Default value, not overridden)
- Axis Z = 0% (From master values)
- Axis RX = 25% (From master values)
- Axis RY = 50% (From master values)
- Axis RZ = 0% (Default value, not overridden)
- Axis SL1 = 0% (Default value, not overridden)
- Axis SL2 = 0% (Default value, not overridden)
- POV1 = Neutral (Default value, not overridden)
- POV2 = Neutral (Default value, not overridden)
- POV3 = 90° (From master values)
- POV4 = Neutral (Default value, not overridden)

Now we add vJoy **Device #3** which has 8 axes and 4 POV Hats. The initial values of its controls will be:

- Axis X = 50% (Default value, not overridden)
- Axis Y = 50% (Default value, not overridden)
- Axis Z = 30% (From device #3 initialization values) ⬅️
- Axis RX = 25% (From master values)
- Axis RY = 50% (From master values)
- Axis RZ = 60% (From device #3 initialization values) ⬅️
- Axis SL1 = 0% (Default value, not overridden)
- Axis SL2 = 0% (Default value, not overridden)
- POV1 = Neutral (Default value, not overridden)
- POV2 = Neutral (Default value, not overridden)
- POV3 = 90° (From master values)
- POV4 = Neutral (Default value, not overridden)

### Registry

All new entries are under registry key `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\vjoy\Parameters`

Let’s call it `%vJoyParam%`



The initialization key for device **nn** (01 to 16) is `%vJoyParam%\Devicenn\Init`

The master control key is `%vJoyParam%\Device00\Init`

All of the above initialization <ins>keys</ins> are optional.

The specific initialization values are under the above keys. All initialization <ins>values</ins> are optional.

### Values in Registry

#### Axes

The value names are “X", "Y", "Z", "RX", "RY", "RZ", "SL1", "SL2”.\
The value data range is 0 to 100 (0x00 - 0x64).\
Data type is REG_BINARY - one byte.

#### POV Hats

The value names are “POV1", "POV2", "POV3", "POV4"\
**Continuous**: The value data range is 0 to 100 (0x00 - 0x64) or -1 (0xFF) for neutral state.\
**Discrete**: Possible values are: 0x80 (Up/North), 0x81 (Right/East),  0x82 (Down/South), 0x83 (Left/West) and 0x8F for neutral state.\
Data type is REG_BINARY - one byte

Notes:\
If you mix vJoy devices that include **Continuous** POVs with vJoy devices that include **Discrete** POVs it is advisable not to use the master entry (Init00) for initialization of POVs. In such a case, always resort to a per-device initialization policy.

#### Buttons

The value name is “BTNS" - Initialization values for all buttons are set in a single key.\
Data type is REG_BINARY - 16 bytes summing up to 128 bits.\
Each one of the 128 bits represents a button.

### Registry Examples

#### Example 1: Master Initialization

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\vjoy\Parameters\Device00\Init]
"X"=hex:00
"Y"=hex:32
"Z"=hex:64
"RX"=hex:0a
"RY"=hex:14
"RZ"=hex:1e
"SL1"=hex:28
"SL2"=hex:32
"POV1"=hex:00
"POV2"=hex:32
"POV3"=hex:28
"POV4"=hex:ff
"BTNS"=hex:80,70,00,00,00,00,00,00,00,00,00,00,00,00,00,00
```

Example 1 sets all controls for vJoy devices.\
Axis X is set to bottom (0%), axis Y to centre (50%), and axis Z to top (100%).\
POV1 is set to “North” - 0%.\
POV2 is set to “South” - 50%.\
POV4 is set to neutral point (-1).\
Button 8 is set - Only the 8th bit in the first byte is ‘1’.\
Buttons 13, 14, 15, are set - bits 5, 6, 7 in the second byte are ‘1’.\
The rest of the buttons are not set.

#### Example 2: Initialization of device 3

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\vjoy\Parameters\Device03\Init]
"X"=hex:00
"Y"=hex:00
"Z"=hex:00
""BTNS"=hex:01,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00
```

Example 2 sets some controls for vJoy device 3.\
Axis X, Y and Z are set to bottom (0%).\
Button 1 is set; all other buttons are not set.\
All other initial control values are taken from the master initialization (if it exists).

### Applying Initialization

The initialization values are read by the driver when a device is loaded and when an API function `ResetVJD()` is called. In order for the device to not show glitchy behaviour, the registry values should be already in place before vJoy devices are loaded.

This could be done manually by calling **regedit** or be adding an initialization file to the **installer**.

#### Installer Default

If you place a registry file named vJoyInit.reg in the folder where the installer resides, the installer will merge this registry file into the registry.

> [!WARNING]
> vJoy Installer does not verify the validity of the file. Be very careful with what you supply to your users.

#### Installer Command Line

You may force vJoy installer to merge a specific registry file by specifying the filename in the installer command line.

Example: `vJoySetup.exe -initreg myinit.reg`

> [!WARNING]
> vJoy Installer does not verify the validity of the file. Be very careful with what you supply to your users.
