# vJoy Installer

<small>Original archived at: https://web.archive.org/web/20180331222811/http://vjoystick.sourceforge.net/site/index.php/download-a-install/deployment216/vjoy-installer</small>

The vJoy Installer has a set of default features.

You can override these default features:

- through the installer's command line.
- by introducing file **vJoyInit.reg** to the installer's folder.

Let's assume the installer is **vJoySetup.exe** (it is named differently for every release).

## Selective Installation

By default, vJoy includes a few additional utilities:

- **vJoyFeeder**: Demo Feeder that demonstrates the capabilities of vJoy.
- **vJoyMon**: Monitors the vJoy controls. Useful for testing a feeder.
- **vJoyConf**: To configure vJoy devices and enable/disable the driver.

You can select only part of these utilities or none. Here are a few examples:

`vJoySetup /COMPONENTS="Apps\vJoyFeeder,Apps\vJoyConf"`\
The above command will install only vJoyFeeder and vJoyConf

`vJoySetup /COMPONENTS="Apps\vJoyMon"`\
The above command will install only vJoyMon

`vJoySetup /COMPONENTS="!Apps"`\
The above command will not install any of the utilities

## Customized Installation

The default vJoy installation will configure your system with one vJoy device (#1) that is equipped with all eight axes, eight buttons, none of the POVs and all FFB effects.

In addition to that, the initial positions of all controls are set to default values.

While you can configure your vJoy devices after the installation (add devices, change control availability, add/remove FFB effects) using [vJoyConf](vjoyconf.md) (or [vJoyConfig](vjoyconfig.md)), you cannot change the default control values after installation.

You can also run **vJoyConfig** in a batch file immediatly after the installation of vJoy.

Customizing the installation is done by placing a registry file (.reg) in the installer folder. The installer will by default read file **vJoyInit.reg** if it exists. If you prefer naming your reg file to some other file name (e.g. myInit.reg) you need to use the following command line syntax:

`vJoySetup -initreg myInit.reg`

> [!WARNING]
> The installer does not parse the given reg file so if you place an error in the file you might inflict serious damage to your Windows system.

Preparing the configuration part of the registry file should be done using vJoyConf (or vJoyConfig) on another system.

The Initialization part of the registry file is prepared manually according to [rules](initial-values.md).
