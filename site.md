# vJoy

<small>Original archived at: https://web.archive.org/web/20180313235110/http://vjoystick.sourceforge.net/site/</small>

## Overview

vJoy is a <ins>device driver</ins> that bridges the gap between any device that is **not** a joystick and an application that requires a joystick. If you develop an application for windows that requires user physical input you should consider incorporating vJoy into your product.

vJoy can be incorporated as-is or modified. vJoy can be used with fixed configuration or configurable. It also comes with tools and example code that feeds it with data and configure the virtual joystick.

vJoy is implemented as a joystick virtual-device driver for windows (XP and up) that does not represent an actual hardware device.

The vJoy device is seen by Windows as a standard joystick device. However, it receives its signals through a simple software interface. Coders can take advantage of this interface by modifying the provided sample code.

## Organization of this site

This site will guide you through the [Download](download-a-install.md), [Development](dev216.md) and support of vJoy.

1. **Deployment** includes instructions how and what to download. How to install vJoy and description of the organization of the download site.
2. **Development** Includes understanding the architecture of vJoy, acquainting with various parts project and the organization of the source code.
3. **Support** is currently given using the [Forum](https://vjoy.freeforums.net/) 🔗. In cases you need to call the author for other matter, please use the Contact Form.

## Which vJoy?

You can choose to use one of the off-the-shelf versions of vJoy, request a modification or modify vJoy yourself. It depends on your needs and your development skills. Taking the right decision is the first step in incorporating vJoy in your product.

There are a few flavours of vJoy that you can use.

### Current branch

The recommended branch of vJoy is the **Incompatible** (to PPJoy) branch. AKA vJoy 2.x. This is the most advanced branch that is fully configurable, secure and supports up to 16 virtual-devices. All documents on this site relate to this branch unless stated differently.

### Older branches

If you need a simple replacement to PPJoy you might consider taking the **Compatible/Fixed** (CF) branch of vJoy. This branch is stable and offers one device with 8 fixed axes and 32 buttons. It cannot be configured and its axes cannot be re-mapped.

If you need a configurable replacement to PPJoy you might consider taking the **Compatible/Configurable** (CC) branch of vJoy. Here you can set the number of buttons (up to 32) and select the needed axes. You cannot re-map the axes unless you are willing to make a small change in your code.

A comprehensive discussion is found under section [Architecture](vjoy-version-103.md).

## Example projects

- SmartPropoPlus: Controls flight simulators from your R/C transmitter.
- Mobimotion: Play your favourite Windows games using your mobile device.
- WeeWheel: You can play games by only moving your phone!
- steel-batallion-64: A Windows 7 64 bit "driver" for the Steel Batallion Controller
