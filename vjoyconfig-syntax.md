# vJoyConfig Syntax

<small>Original archived at: https://web.archive.org/web/20180310075705/http://vjoystick.sourceforge.net/site/index.php/utilities-218/vjoyconfig/88-uncategorized/130-vjoyconfig-syntax</small>

## `vJoyConfig`

Launch GUI

Without any additional flags, `vJoyConfig` launches the _vJoyConf_ graphical tool.

Note: This requires vJoyConfig to be copied into the vJoy directory, and the system to be configured correctly.

## `vJoyConfig -h`

Print the vJoyConfig help

## `vJoyConfig -t [[-c] Dn...]`

Print a report of the current vJoy Configuration

Without any additional flags, `vJoyConfig -t` lists all vJoy devices and their respective statuses.


###### Arguments:

- `Dn` – One or more devices for which the command will print configuration information.

###### Options:

- `-c` – The configuration report will be in vJoyConfig command-line format, to be reused in a batch file.

Note: <ins>Not</ins> using flag `-c` will result in a human-readable output format.


## `vJoyConfig -v`

Display version information

## `vJoyConfig -r`

Reset vJoy configuration to its default state

Note: This operation is equivalent to deleting all configurations. vJoy will fall back into its default state which is «Device #1 with 8 Axes and 8 Buttons».

## `vJoyConfig Enable [on | off]`

Enable or disable the vJoy <ins>driver</ins>

Note: This operation is useful if you need to disable all vJoy devices and then enable them.

###### Options:

- `on` – Enables the vJoy driver
- `off` – Disables the vJoy driver

Default is `on`


## `vJoyConfig -d [Dn]...`

Delete one or more devices

Note 1: This operation can be applied to already deleted devices.

Note 2: If all devices are deleted, this operation does the equivalent to `vJoyConfig -r`.

###### Arguments:

- `Dn` – One or more devices to remove. Devices are in the 1-16 range.


## `vJoyConfig Dn [-f] [-l] [-a Ai...] [-b N] [-p M | -s J] [-e Ei...]]`

Create or replace a joystick device

Note 1: This operation never modifies an existing device. It either leaves it unchanged or overwrites its configuration.

###### Arguments:

- `Dn` – The index of the target joystick device in the range of 1-16

###### Options:

- `-f` – Force creation even if device exists. This will delete the current device before creating a new one.
- `-l` – Defer creation of device until the next operation that enables the driver.
- `-a Ai` – Define axes (one or more).
    - Possible values are (Case insensitive): `x`, `y`, `z`, `rx`, `ry`, `rz`, `sl0`, `sl1`
    - In the absence of this flag the default will be used (Default = all axes)
- `-b N` – Set the number of buttons (Possible values are 0 to 128; Default = 8 buttons)
- `-p M` – Set the number of analog POV Switches (Possible values are 0 to 4; Default = 0)
- `-s J` – Set the number of discrete POV Switches (Possible values are 0 to 4; Default = 0)
- `-e Ei` – Define the required FFB Effect. Possible effect values are (case-insensitive):

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


Note 2: Use flag `-f` to overwrite an existing device configuration.

Note 3: To create a new device only if previously absent, avoid using flag `-f`.

Note 4: A device can include either  **Analog** or  **Discrete** POV switches, meaning that options `-p` and `-s` exclude each other.

Note 5: Omitting flag `-e` will result in a device that does not support FFB.

Note 6: `-e all` is equivalent to `-e const ramp sq sine tr stup stdn spr dm inr fric`.

## How to Deploy

**vJoyConfig** is now part of the vJoy installation.

(Usually located in `C:\Program Files\vJoy\x64` or `C:\Program Files\vJoy\x86`).
