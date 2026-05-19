# Wheelchair Digital Interface
The Wheelchair Digital Interface (WDI) is an open, modern communication standard for power wheelchairs built on widely accepted HID protocols. It gives wheelchair users more choice in how they drive and interact with their chair, and gives makers, researchers, and clinicians a shared, open foundation to build on.

You can view the documents as [Source Code](https://github.com/Open-Mobility-Hub/wheelchair-digital-interface) or browse as a [Doc Site](https://open-mobility-hub.github.io/wheelchair-digital-interface/).

## Purpose
The purpose of the open WDI standard is: 
1. to allow faster development of new accessible wheelchair alternative controls by removing the need for 9-pin printer cable adapter circuits currently required to adapt to today's proprietary TRACE/DB-9 wheelchair alternative drive inputs, 
2. to make current, commercially available adaptive gaming and computer interfaces available to power wheelchair users for wheelchair control, and, 
3. to allow two-direction communication between the power wheelchair and the controller to provide enhanced user feedback. 

## Quick Start — Choose Your Interface

WDI currently offers multiple complementary interface paths. Pick the path that matches what you're building.

| Interface | Best for | Typical builder | Spec |
|-----------|----------| ----------------|------|
| **USB HID** | Adapting off-the-shelf gamepads, keyboards, and existing accessible input devices to drive a wheelchair | Accessible-tech makers, gaming-controller adapters, clinicians evaluating drive options | [USB mapping](/docs/usb/wdi-usb-interface.md) |
| **BLE HID** | Same use cases as USB, but wireless | Wireless input device makers | [BLE mapping](/docs/ble/wdi-ble-interface.md) |
| **Wheelchair HID** | Purpose-built apps and devices that want **two-way** communication — sending control input *and* receiving wheelchair state | App developers building wheelchair-aware experiences, researchers needing telemetry, advanced control devices | [Wheelchair HID spec](/docs/wheelchair/wheelchair-hid.md) |

Use USB or BLE HID when you want a commercial gamepad, adaptive switch, or keyboard to control a chair. Use Wheelchair HID when you're building an app or device that needs the wheelchair to talk back — for richer user feedback, smarter UIs, or research data.

### Get Started in 5 Minutes
* Try the [Compatibility Tester](/tester-util/standard-hid-tester.html) with a USB or BLE gamepad you already own — see live HID events translated into wheelchair commands.
* Skim [What is Controlled on a Wheelchair](#what-is-controlled-on-a-wheelchair) to see the WDI command surface.
* Pick your spec from the table above.
* Check the [list of known host-side implementations](/docs/implementations/implementations.md) to see which chairs you can target today.
* Read [CONTRIBUTING.md](CONTRIBUTING.md) and the [Code of Conduct](CODE_OF_CONDUCT.md) if you want to contribute.

## Background
The WDI was initially conceived and developed as part of the National Science Foundation (NSF) Convergence Accelerator Track H project "Mobility Independence through Accelerated Wheelchair Intelligence" (NSF SP0076554) with input from a wide range of stakeholders. 

WDI is intended to fill a gap in current power wheelchair standards. RESNA WC-2 and ISO 7176 do not define or provide guidance on power wheelchair interfaces for third party input devices, and previous attempts to provide a standard for power wheelchair interfaces and accessories (such as the M3S standard) failed due to lack of industry adoption.

Prior to the WDI, the state-of-the-art in power wheelchair controls was to communicate with the wheelchair through a proprietary third-party interface module using a 9-pin D-Sub (DB-9) connector. This interface was commonly referred to as "TRACE", was an input only/one-way interface, and was defined slightly differently by each wheelchair electronics manufacturer. TRACE is not a published or maintained industry standard. See your wheelchair manufacturer's technical documents for more details if attempting to use TRACE. 

## Stakeholders
The stakeholders originally involved in WDI development are represented below. They do not cover every use case, but they cover the primary use cases that the WDI seeks to address.

### 1. Wheelchair Users with Progressive or Changing Conditions
* The drive method that works best may change over time as physical capabilities change
* Today's funding model can take long enough that the prescribed solution no longer matches the user's current needs by the time it arrives. As a result, users sometimes settle for a future-proof drive method (such as eye drive) before they actually need it, rather than the one best suited to them right now. WDI shortens that loop by letting users and clinicians try input options quickly
* Wants to add additional inputs and options to their primary control method

### 2. Tech Savvy Wheelchair User
* Uses computer, smartphone, plays video games, tinkers with technology
* Wants to tinker with using other things to drive their wheelchair, like phone or game controller, so they can get the best setup for themselves
* Would like to use wheelchair control device to control other technology (or vice versa)
* Wants ability to play with configuration/button mapping to best fit their needs

### 3. Wheelchair Clinician/ATP
* Wants to be able to quickly and easily test multiple drive options to find what best fits user needs
* Wants to spend less time writing/justifying devices to insurance/funding sources

### 4. Accessible Technology Maker
* Makes a device for controlling computers in an alternative way
* Wants to adapt device to control a wheelchair to increase addressable market without designing additional hardware
* Does not want to learn about proprietary wheelchair electronics

### 5. Researcher
* Wants to be able to rapidly iterate/prototype devices for wheelchair control
* Wants data to come back from the wheelchair for feedback to the user (e.g. lights, sounds, haptics)

## Requirements
* WDI shall allow for devices to control all aspects of a power wheelchair that the user can currently control.
* WDI shall interface with off-the-shelf computer control devices such as gaming controllers, keyboards, and other computer peripherals.
* WDI shall allow for bi-directional communication with the input device for providing feedback such as haptics, lights, or sounds.
* WDI shall allow for devices to self-report their capabilities and bounds (e.g. joystick ranges).
* WDI shall allow for multiple complementary devices to be used simultaneously.
* WDI shall require a specific input before allowing a device to drive the wheelchair.
* WDI shall stop the wheelchair and return control to the default wheelchair control device upon losing connection to an input.

## What is Controlled on a Wheelchair
\* May optionally be adjusted/actuated within a menu that is controlled via normal driving directional commands.

| Action | Notes |
| -------------|---------|
| Power/sleep toggle* | Distinct but functionally equivalent |
| Move forward | Proportional or digital |
| Move backward | Proportional or digital |
| Turn left | Proportional or digital |
| Turn right | Proportional or digital |
| Adjust maximum speed* | Up/down |
| Change profile* | Includes switching to attendant control |
| Switch mode* | Mainly between drive/seating control |
| Emergency stop | Typically used with latch drive mode |
| Seating controls | Matches movement controls, left/right select actuator, up/down moves actuator |
| Open user menu | Usually a digital switch, can be input sequence |
| Navigate user menu | Matches movement controls |
| Headlight toggle* | |
| Hazard lights toggle* | |
| Left/right blinker toggles* | |
| Horn* | |

### Seating Control
This is the list of anticipated, possible parts of a wheelchair seating system that can be controlled. Not every chair is equipped with every actuator.

The specific actuators that can be adjusted up and down are:
* Tilt
* Recline
* Legs
* Elevate
* Footplates
* Stand

In addition to the specific actuators, chairs may be programmed with a number of set positions (i.e. memory positions) that the seating system can be automatically positioned to.

### Anticipated Future Needs
* Silence sounds
* Enable/disable airplane mode/communications
* Wheelchair specific optional commands (e.g. triggering of automated features)

## WDI Device Implementer Guidance
The WDI builds upon existing specifications for using [Human Interface Devices (HID)](https://en.wikipedia.org/wiki/Human_interface_device).

### Compatibility Tester
There are two separate compatibility testers depending on whether you are using standard keyboard/gamepad HID or Wheelchair HID. 

[A web-based testing tool for verifying device compatibility with the WDI gamepad/keyboard mappings](/tester-util/standard-hid-tester.html) 

[A web-based testing tool for verifying compatibility with the WDI wheelchair HID](/tester-util/wheelchair-hid-tester.html) 

Both testers display raw HID events from alongside the translated wheelchair commands they would produce. They have been tested with devices connected via USB and BLE. This site uses additional libraries on top of HID so off-the-shelf gamepads and keyboards work correctly.

### USB
For making commercial gaming controllers, keyboards, and other accessible input devices control a wheelchair over USB. [USB mapping and implementation guidance](/docs/usb/wdi-usb-interface.md)

### Bluetooth
The same use cases as USB, wirelessly over Bluetooth Low Energy. [BLE mapping and implementation guidance](/docs/ble/wdi-ble-interface.md)

### Wheelchair HID (Bidirectional)
The Wheelchair HID is a specification for **bidirectional** communication between a wheelchair host and a Bluetooth LE or USB connected app or device. It defines HID descriptors for apps and devices to send control input, request feedback, and exchange keepalive messages with a wheelchair host, and for the host to report wheelchair state — including speed setting, profile, mode (drive/seating), velocity in mph, blinker/headlight/hazard state, and movement-restriction state — back to connected apps and devices.

It is purpose-built for power wheelchairs and extends WDI beyond what USB/BLE HID alone offer:
* **Two-way data** — apps can show the user what the chair is doing, and adapt their UI to chair state.
* **Host identification** — a cryptographically unique host UUID is exchanged via keepalive responses so an app can recognize a specific chair across reconnections.
* **Mandatory keepalive** — defined timing ensures the chair safely stops driving if an app or device goes silent.

There are no current host implementations of this spec. [Read the full Wheelchair HID spec](/docs/wheelchair/wheelchair-hid.md)

### Other Physical Interfaces
Expansion of the WDI definition to cover other physical interfaces is anticipated. HID is also supported on the following interfaces:
* I2C
* CAN

### Devices That Require Custom Drivers
Some common input devices require a driver or may work differently with a driver installed as it relates to WDI functionality. For the devices listed below, the host device will need to implement the manufacturer's custom driver. This is not a complete list, but simply notes common, known devices. 

| Controller | Notes |
|------|-----|
| Xbox | Requires driver (xpad) |
| Playstation 5 (DualSense) | Can work generically, but has right stick axes and buttons mapped differently with driver. Motion and touchpad capabilities require driver |

## WDI User Guidance (Known Implementers)
Implementations may have their own additions and limitations, which are captured here in the
[list of known host-side implementations](/docs/implementations/implementations.md)

## License
The WDI is open for use under an Apache 2.0 License.

## Versioning
Versioning is handled on a major.minor.patch method. All official releases will be tagged.

## List of Current Support
The companies and organizations listed support the open, inclusive future provided by the WDI.

| Organization | Description |
| -------------|---------|
| [Argallab at Northwestern University](https://www.argallab.northwestern.edu) | Founding Member |
| [The A Team](https://teamgleason.org/a-team/) | Founding Member, with special thanks to Daniel Vance and Kevin Rowland. |
| [LUCI](https://www.luci.com) | Founding Member, LUCI units with LuciCore 2.0 and newer software are compatible with USB WDI controllers. |
| [LifeDrive](https://www.lifedrivemobility.com/) | Contributing Member, with special thanks to Shawn Sexton. |
| [Shirley Ryan AbilityLab](https://www.sralab.org) | Founding Member |