# Utilities

https://web.archive.org/web/20180223073440/http://vjoystick.sourceforge.net/site/index.php/utilities-218


vJoy installation include several utilities that are meant to help configuring and testing vJoy devices.

## Configuration

To create or remove a device, to add or remove axes, buttons or POVs, to configure Force Feedback (FFB) options use one of the following applications:

- ***[vJoyConf](vjoyconf.md)***: User friendly graphical tool. Configuration done one device at a time.
- ***[vJoyConfig](vjoyconfig.md)***: Command-line version of vJoyConf. More efficient than vJoyConf as it may configure all devices at once.

## Listing

The fastest way to see which devices are configured (Exist), not configured (Missing) or owned by a feeder use _**[vJoyList](vjoylist.md)**_. It will also tell you which process owns which vJoy device.

## Feeder

To test your setup you can use _**[vJoyFeeder](vjoyfeeder.md)**_ to feed any vJoy device. Note that this is a standard feeder so it acquires the selected device (preventing other feeders from owning it) and it cannot acquire an already owned device.

## Monitoring

To test your feeder, you can use _**[Monitor](monitor.md)**_ that monitors feeder activity for the selected device. It is much better than the inbox "Game Controllers". It only monitors vJoy devices