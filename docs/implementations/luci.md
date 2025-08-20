# LUCI Implementation
LUCI implements the WDI for USB via the LuciLink Hub. Devices plugged into the LuciLink USB hub on LUCI will control your wheelchair per the WDI spec, with the additional custom mappings and limitations described on this page. 

**Last upated for LuciCore 3.0.1**

## General Notes
* LUCI collision avoidance and drop-off protection is active when the chair is controlled via the WDI.
* LUCI plays a sound when a device becomes the active controller and a different sound when the device is deactivated for clarity.
* Unplugging any active device deactivates the device and returns control to the wheelchair electronics.

## Custom Button Mappings
| Action | Keyboard | Gamepad |
|-----|---|---|
| Override | caps lock | BTN_EAST |
| Reset changes | Home | None |
| Profile decrement | matches main spec | ABS_HAT0Y = 1 (temporarily implemented until mode switching is implemented) |
| Power/Sleep toggle | None (Escape temporarily mapped to emergency stop until power controls implemented) | None |
| Switch mode | None (Tab temporarily mapped to emergency stop until mode controls implemented) | None |

## Limitations and Known Issues
### General
1. LUCI turns off when the wheelchair does, so a WDI input device cannot be used to turn the wheelchair on through LUCI. This also means WDI devices powered through the LuciLink USB connection to LUCI are off when LUCI is off.
1. The mapping of HID commands to seating axis is not consistent across chair manufacturers or between Power Platform and legacy Permobil wheelchairs. LUCI is expected to work for standard seating axes on most chair models, but it may not match on every chair out there due to wheelchair manufacturer customizations. Seating commands should initially be tested without a person in the chair to ensure correct operation.
1. Speed setting adjustments made through the WDI by LUCI are not remembered by the wheelchair electronics. This means that the previously set speed setting will come back if the profile is changed or the the chair is rebooted, and that any changes made to speed setting through the normal joystick interface will change based on what the speed setting was before LUCI changed it (e.g. speed 5 -> LUCI changes to speed 1 -> speed setting decrease through JSM leads to speed 4).
1. LUCI does not know how many profiles are enabled on the chair and currently assumes there are 4. On chairs with fewer than 4, incrementing to a disabled profile is a no-op on the chair, and incrementing continues to be no-ops until wrapping back around to profile 1. On chairs with more than 4 enabled profiles, there is no way to access the additional profiles via the WDI currently.

### Legacy Permobil Chairs with Tracking (ESP)
This includes most Permobil chairs made between 2020-2024 (before Power Platform). When the chair is being controlled via the WDI:
1. Programmed RNET settings do not affect drive behavior.
1. Speed settings 4 and 5 do not affect drive behavior and are functionally equivalent to speed 3.
1. Profile does not affect drive behavior.
1. Chair may drive differently through the WDI than with the standard joystick due to tracking interaction with the WDI.
1. Seating position cannot be moved using the drive commands on the input device through LUCI.
1. The wheelchair user menu cannot be navigated using a WDI input device through LUCI.


### Xbox Controllers
Notes on interfacing with Xbox controllers specifically (including Xbox Adaptive Controller)
1. Xbox controllers plugged into the LUCILink Hub before the chair/LUCI is turned on will **not** turn on and connect automatically. The controller has to be plugged in after LUCI is powered. This is not an issue if the device is plugged directly into one of the MPU USB ports.