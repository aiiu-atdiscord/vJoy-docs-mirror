# vJoyConfig Syntax

<small>Original archived at: https://web.archive.org/web/20180310075705/http://vjoystick.sourceforge.net/site/index.php/utilities-218/vjoyconfig/88-uncategorized/130-vjoyconfig-syntax</small>

### `vJoyConfig`

Launch GUI

Note: This requires vJoyConfig to be copied into the vJoy directory, and for the system to be configured correctly.

### `vJoyConfig -h`

Help text

### `vJoyConfig -t [[-c] Di...]`

Report current vJoy Configuration

Without any additional flags - list of vJoy device and their respective statuses.

- `-c` – The configuration report is in vJoyConfig command-line format. To be reused in batch file.
- `Di` – List of devices for which the command will print configuration information.

Note: <ins>Not</ins> using flag `-c` will result in a human-readable output format.

### `vJoyConfig -v`

Version information

### `vJoyConfig -r`

Reset vJoy to default configuration

Note: This operation is equivalent to deleting all configurations. vJoy will fall back into its default state which is Device #1 with 8 Axes and 8 Buttons.

### `vJoyConfig Enable [on | off]`

Enable or Disable vJoy <ins>driver</ins>. Default is `on`

Note: This operation is useful if you need to disable all vJoy devices and then to enable them.

### `vJoyConfig -d Dn [Dn+1...]`

Delete one or more devices - devices are in the 1-16 range

Note 1: This operation may be applied to no-existing devices.

Note 2: If all devices are removed - the operation is equivalent to `vJoyConfig -r`.

### `vJoyConfig Dn [-f][-l][-a Ai [Ai+1 …]] [-bn] {[-pm] | [-sj]} [-e [{all | Ei ...}]]`

Create or replace a joystick device

- `Dn` – The index of the target joystick device in the range of 1-16
- `-f` – Force creation even if device exists. This will delete the current device before creating a new one.
- `-l` – Defer creation of device until the next operation that enables the driver. See Notes.
- `-a Ai` – Define axes (one or more).
    - Possible values are (Case insensitive): `x`, `y`, `z`, `rx`, `ry`, `rz`, `sl0`, `sl1`
    - In the absence of this flag the default will be used (Default = all axes)
- `-b n` – Set the number of buttons (Possible values are 0 to 128; Default = 8 buttons)
- `-p m` – Set the number of analog POV Switches (Possible values are 0 to 4; Default = 0)
- `-s j` – Set the number of discrete POV Switches (Possible values are 0 to 4; Default = 0)
- `-e Ei` – Define the required FFB Effect. Possible Effect Values are (Case Insensitive):

| | |
| --- | --- |
| `Const` | Constant Force |
| `Ramp` | Ramp Force |
| `Sq` | Square Wave Force |
| `Sine` | Sine Wave Force |
| `Tr` | Triangular Wave Force |
| `StUp` | Sawtooth (Up) Wave Force |
| `StDn` | Sawtooth (Down) Wave Force |
| `Spr` | Spring |
| `Dm` | Damper |
| `Inr` | Inertia |
| `Fric` | Friction |
| `All` | All above FFB effects |

Note 1: This operation never modifies an existing device. It either leave it unchanged or override its configuration.

Note 2: Use flag `-f` to overwrite an existing device configuration

Note 3: To create a new device only if absent - do not use flag `-f`

Note 4: A device can include either  **Analog** or  **Discrete** POV switches

Note 5: Omitting flag `-e` will result in a device that does not support FFB

Note6:  `-e all` is equivalent to `-e const ramp sq sine tr stup stdn spr dm inr fric`

## How to Deploy

**vJoyConfig** is now part of the vJoy installation.

(Usually located in `C:\Program Files\vJoy\x64` or `C:\Program Files\vJoy\x86`).
