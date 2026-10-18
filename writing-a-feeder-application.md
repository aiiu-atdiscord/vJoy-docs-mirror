# Writing a feeder application

https://web.archive.org/web/20180223095629/http://vjoystick.sourceforge.net/site/index.php/dev216/writing-a-feeder-application

## What is a Feeder

While an application sees a vJoy device as just another standard joystick device, it is the role of the feeder to feed the device with meaningful data.

A common scenario is when you have a computer game that can be controlled by a single joystick device. However, you want  to control it from two physical joysticks. By writing a feeder you can accomplish this task as follows:

You write a feeder that reads information from both physical joysticks and feed the combined data to the vJoy device. The game sees only a single device, vJoy. However, this device hides behind it the two physical devices.

Other common scenarios are when a vJoy device passes position information created by devices that are not joysticks such a mouse, the keyboard or a stearing wheel. You can also write a feeder that gets its data over the internet or WiFi.

## Feeder Basics

Your feeder should be able to:

- Get (or create) position data. Position data may support position for up to 8 Axis, up to 4 POV hats and up to 128 buttons. You may use all or only a small part of these controls. A feeder that controls Axis X, Axis Y and four buttons is a very common feeder.
- Send the position data to one (or more) vJoy devices.

It is recommended that you feeder be able to:

- Detect that a vJoy deriver is installed.
- Detect the ID numbers of the available vJoy devices.
- Detect the controls that are configured (per vJoy device).

In addition, you may want your feeder to support FFB. If so, you will be required to write a **Receptor** unit inside your feeder. This unit deals with data packets sent to the vJoy device from the application (Usually a computer game). The receptor should deal with these FFB packets. They are usually just passed on to a physical device.

The vJoy API is fully implemented as a single C-language dynamic library (dll) that is a part of the SDK and is also distributed with the vJoy installation. 

## Feeder SDK

The [Feeder SDK](https://sourceforge.net/projects/vjoystick/files/Beta%202.x/2.1.9.1-160719/SDK.zip/download "Feeder SDK for vJoy version 2.x") is contains a C/C++ section and a C# section.

### C/C++

The API is exposed by file _vJoyInterface.dll_. Both amd64 and x86 versions of this file are included in the SDK. An import library _vJoyInterface.lib_ is also included. These files are located in folder _lib_ and its sub folders.

You will also need a few header files that are located under folder _inc_.

Under folder _src_ you will find an example project. Use it as a starting point for your feeder.

The most recent SDK manual is packed with the SDK.

### C#

The API is exposed by a C-language file _vJoyInterface.dll_ Wrapped by a C# file _vJoyInterfaceWrap.dll_. Both amd64 and x86 versions of the former file are includeded in the SDK. An import These files are located in folder c#/x86 and c#/x64.

Under folder _FeederDemoCS_ you will find an example project. Use it as a starting point for your feeder.

The most recent SDK manual is packed with the SDK (under c#).