# LUCI Implementation
LUCI implements the WDI for USB via the LuciLink Hub and for BLE via the Setup Tool. Devices plugged into the LuciLink USB hub on LUCI will control your wheelchair per the WDI spec, with the additional custom mappings and limitations described on this page. 

**Last upated for pre-release LuciCore 3.1.1**

## General Notes
* LUCI collision avoidance and drop-off protection is active when the chair is controlled via the WDI.
* LUCI plays a sound when a device becomes the active controller and a different sound when the device is deactivated for clarity.
* Unplugging/disconnecting any active device deactivates the device and returns control to the wheelchair electronics.

## Custom Button Mappings

| Action | Keyboard | Gamepad |
|-----|---|---|
| Override | caps lock | BTN_EAST |
| Reset changes | Home | None |
| Power/Sleep toggle | None (Escape temporarily mapped to emergency stop until power controls implemented) | None |

## BLE
Instructions for pairing/connecting devices to LUCI can be found in the User Guide.

For devices to know they are connecting to LUCI, they can look for the following information in the advertisement:
* `luci` in the name
* In the standard Device Info service, the "Manufacturer Name String" characteristic is "LUCI Mobility, Inc."
* Has a service with UUID "a8736e1c-f48e-4c4d-b6f2-3dadef41dd47"

## Limitations and Known Issues
### General
1. LUCI turns off when the wheelchair does, so a WDI input device cannot be used to turn the wheelchair on through LUCI. This also means WDI devices powered through the LuciLink USB connection to LUCI are off when LUCI is off.
1. The mapping of HID commands to seating axis is not consistent across chair manufacturers or between Power Platform and legacy Permobil wheelchairs. LUCI is expected to work for standard seating axes on most chair models, but it may not match on every chair out there due to wheelchair manufacturer customizations. Seating commands should initially be tested without a person in the chair to ensure correct operation.
1. Speed setting adjustments made through the WDI by LUCI are not remembered by the wheelchair electronics. This means that the previously set speed setting will come back if the profile is changed or the the chair is rebooted, and that any changes made to speed setting through the normal joystick interface will change based on what the speed setting was before LUCI changed it (e.g. speed 5 -> LUCI changes to speed 1 -> speed setting decrease through JSM leads to speed 4).
1. On Permobil chairs, the first time a device cycles through the modes (specifically when going to the next modes after Seating), an R-Net error will be triggered on the chair and a reboot will be required. The error should not happen on subsequent boots.


### Legacy Permobil Chairs with Tracking (ESP)
This includes most Permobil chairs made between 2020-2024 (before Power Platform). When the chair is being controlled via the WDI:
1. Programmed RNET settings do not affect drive behavior.
1. Speed settings 4 and 5 do not affect drive behavior and are functionally equivalent to speed 3.
1. Profile does not affect drive behavior.
1. Chair may drive differently through the WDI than with the standard joystick due to tracking interaction with the WDI.
1. Seating position cannot be moved using the drive commands on the input device through LUCI.
1. The wheelchair user menu cannot be navigated using a WDI input device through LUCI.
