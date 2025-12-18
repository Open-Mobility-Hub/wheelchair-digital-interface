# Wheelchair Digital Interface
The Wheelchair Digital Interface (WDI) API detailed in this project is a modern, two-way communication standard for power wheelchairs built on widely accepted HID protocols.

## Purpose
The purpose of the open WDI standard is: 
1. to allow faster development of new accessible wheelchair alternative controls by removing the need for 9-pin printer cable adapter circuits currently required to adapt to today's proprietary TRACE/DB-9 wheelchair alternative drive inputs, 
2. to make current, commercially available adaptive gaming and computer interfaces available to power wheelchair users for wheelchair control, and, 
3. to allow two-direction communication between the power wheelchair and the controller to provide user feedback. 

## Background
The WDI was initially conceived and developed as part of the National Science Foundation (NSF) Convergence Accelerator Track H project "Mobility Independence through Accelerated Wheelchair Intelligence" (NSF SP0076554) with input from a wide range of stakeholders. 

WDI is intended to fill a gap in current power wheelchair standards. RESNA WC-2 and ISO 7176 do not define or provide guidance on power wheelchair interfaces for third party input devices, and previous attempts to provide a standard for power wheelchair interfaces and accessories (such as the M3S standard) failed due to lack of industry adoption.

Prior to the WDI, the state-of-the-art in power wheelchair controls was to communicate with the wheelchair through a proprietary third-party interface module using a 9-pin D-Sub (DB-9) connector. This interface was commonly referred to as "TRACE", was an input only/one-way interface, and was defined slightly differently by each wheelchair electronics manufacturer. TRACE is not a published or maintained industry standard. See your wheelchair manufacturer's technical documents for more details if attempting to use TRACE. 

## Stakeholders
The stakeholders originally involved in WDI development are represented below. They do not cover every use case, but they cover the primary use cases that the WDI seeks to address.

### 1. Wheelchair Users with Progressive or Changing Conditions
* User's physical capabilities change rapidly, and therefore, so does the functional drive method
* Cannot get new drive methods quickly enough to keep up with changing conditions, so often times users skip to the end use case (eye drive). This leads to situations where the drive method is not chosen based on the user's current ability. The reimbursement model is challenging and time-consuming in such a way that by the time a funded solution arrives and is setup, the user's condition may have progressed and that is no longer an applicable solution
* Wants to add additional inputs and options to their primary control method

### 2. Tech Savvy Wheelchair User
* Uses computer, smartphone, plays video games, tinkers with technology
* Very comfortable with current drive method
* Wants to tinker with using other things to drive their wheelchair, like phone or game controller, so they can get the best setup for themselves
* Would like to use wheelchair control device to control other technology (or vice versa)
* Wants ability to play with configuration/button mapping to best fit their needs

### 3. Wheelchair Clinician/ATP
* Wants to be able to quickly and easily test multiple drive options quickly to find what best fits users needs
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
* WDI shall allow for multiple complimentary devices to be used simultaneously.
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
[A web-based testing tool for verifying input device compatibility with the WDI standard](/tester-util/index.html) 

It displays raw HID events from gamepads, joysticks, and keyboards alongside the translated wheelchair commands they would produce. It has been tested with devices connected via USB and BLE. This site uses additional libraries on top of HID so off-the-shelf gamepads and keyboards work correctly.

### USB
[USB mapping and implementation guidance](/docs/usb/wdi-usb-interface.md)

### Bluetooth
[BLE mapping and implementation guidance](/docs/ble/wdi-ble-interface.md)

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
**THE WDI IS CURRENTLY PRE-RELEASE.**

<i>Versioning is handled on a major.minor.patch method, until the official WDI is released all developers will be using a version < 1.0.0. All official releases will be tagged.</i>

## List of Current Support
The companies and organizations listed support the open, inclusive future provided by the WDI.

| Organization | Description |
| -------------|---------|
| [Argallab at Northwestern University](https://www.argallab.northwestern.edu) | Founding Member |
| [The A Team](https://teamgleason.org/a-team/) | Founding Member, with special thanks to Daniel Vance and Kevin Rowland. |
| [LUCI](https://www.luci.com) | Founding Member, LUCI units with LuciCore 2.0 and newer software are compatible with USB WDI controllers. |
| [LifeDrive](https://www.lifedrivemobility.com/) | Contributing Member, with special thanks to Shawn Sexton. |
| [Shirley Ryan AbilityLab](https://www.sralab.org) | Founding Member |