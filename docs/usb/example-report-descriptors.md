# Examples of Generic USB HID Report Descriptors

## Basic Gamepad
Basic gamepad - has 1 joystick and all basic buttons.

```
0x05, 0x01,        // Usage Page (Generic Desktop Ctrls)
0x09, 0x05,        // Usage (Gamepad)
0xA1, 0x01,        // Collection (Application)
0x15, 0x81,        //   Logical Minimum (-127)
0x25, 0x7F,        //   Logical Maximum (127)
0x09, 0x01,        //   Usage (Pointer)
0xA1, 0x00,        //   Collection (Physical)
0x09, 0x30,        //     Usage (X)
0x09, 0x31,        //     Usage (Y)
0x75, 0x08,        //     Report Size (8)
0x95, 0x02,        //     Report Count (2)
0x81, 0x02,        //     Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)
0xC0,              //   End Collection
0x05, 0x09,        //   Usage Page (Button)
0x19, 0x01,        //   Usage Minimum (0x01)
0x29, 0x0f,        //   Usage Maximum (0x0f)
0x15, 0x00,        //   Logical Minimum (0)
0x25, 0x01,        //   Logical Maximum (1)
0x75, 0x01,        //   Report Size (1)
0x95, 0x0f,        //   Report Count (f)
0x81, 0x02,        //   Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)
0xC0,              // End Collection
```

## Joystick
Taken from a thrustmaster joystick
```
device 0:0
0x05, 0x01,                    // Usage Page (Generic Desktop)        0
0x09, 0x04,                    // Usage (Joystick)                    2
0xa1, 0x01,                    // Collection (Application)            4
0x09, 0x01,                    //  Usage (Pointer)                    6
0xa1, 0x00,                    //  Collection (Physical)              8
0x09, 0x30,                    //   Usage (X)                         10
0x09, 0x31,                    //   Usage (Y)                         12
0x09, 0x32,                    //   Usage (Z)                         14
0x09, 0xbb,                    //   Usage (Vendor Usage 0xbb)         16
0x15, 0x80,                    //   Logical Minimum (-128)            18
0x25, 0x7f,                    //   Logical Maximum (127)             20
0x46, 0xff, 0x00,              //   Physical Maximum (255)            22
0x66, 0x00, 0x00,              //   Unit (None)                       25
0x66, 0x00, 0x00,              //   Unit (None)                       28
0x75, 0x08,                    //   Report Size (8)                   31
0x95, 0x04,                    //   Report Count (4)                  33
0x81, 0x02,                    //   Input (Data,Var,Abs)              35
0xc0,                          //  End Collection                     37
0x09, 0x39,                    //  Usage (Hat switch)                 38
0x15, 0x01,                    //  Logical Minimum (1)                40
0x25, 0x08,                    //  Logical Maximum (8)                42
0x35, 0x00,                    //  Physical Minimum (0)               44
0x46, 0x3b, 0x01,              //  Physical Maximum (315)             46
0x65, 0x14,                    //  Unit (EnglishRotation: deg)        49
0x75, 0x04,                    //  Report Size (4)                    51
0x95, 0x01,                    //  Report Count (1)                   53
0x81, 0x02,                    //  Input (Data,Var,Abs)               55
0x05, 0x09,                    //  Usage Page (Button)                57
0x19, 0x01,                    //  Usage Minimum (1)                  59
0x29, 0x04,                    //  Usage Maximum (4)                  61
0x15, 0x00,                    //  Logical Minimum (0)                63
0x25, 0x01,                    //  Logical Maximum (1)                65
0x75, 0x01,                    //  Report Size (1)                    67
0x95, 0x04,                    //  Report Count (4)                   69
0x81, 0x02,                    //  Input (Data,Var,Abs)               71
0x95, 0x08,                    //  Report Count (8)                   73
0x81, 0x01,                    //  Input (Cnst,Arr,Abs)               75
0x05, 0x08,                    //  Usage Page (LEDs)                  77
0x09, 0x43,                    //  Usage (Slow Blink On Time)         79
0x15, 0x00,                    //  Logical Minimum (0)                81
0x26, 0xff, 0x00,              //  Logical Maximum (255)              83
0x35, 0x00,                    //  Physical Minimum (0)               86
0x46, 0xff, 0x00,              //  Physical Maximum (255)             88
0x75, 0x08,                    //  Report Size (8)                    91
0x95, 0x04,                    //  Report Count (4)                   93
0x91, 0x82,                    //  Output (Data,Var,Abs,Vol)          95
0x55, 0x00,                    //  Unit Exponent (0)                  97
0x65, 0x00,                    //  Unit (None)                        99
0x55, 0x00,                    //  Unit Exponent (0)                  101
0x65, 0x00,                    //  Unit (None)                        103
0x55, 0x00,                    //  Unit Exponent (0)                  105
0xc0,                          // End Collection                      107
```

## Keyboard
```
0x05, 0x01,                        // Usage Page (Generic Desktop)
0x09, 0x06,                        // Usage (Keyboard)
0xA1, 0x01,                        // Collection (Application)
0x05, 0x07,                        // Usage Page (Key Codes)
0x19, 0xE0,                        // Usage Minimum (224)
0x29, 0xE7,                        // Usage Maximum (231)
0x15, 0x00,                        // Logical Minimum (0)
0x25, 0x01,                        // Logical Maximum (1)
0x75, 0x01,                        // Report Size (1)
0x95, 0x08,                        // Report Count (8)
0x81, 0x02,                        // Input (Data, Variable, Absolute) -- Modifier byte
0x95, 0x01,                        // Report Count (1)
0x75, 0x08,                        // Report Size (8)
0x81, 0x03,                        // (81 01) Input (Constant) -- Reserved byte
0x95, 0x05,                        // Report Count (5)
0x75, 0x01,                        // Report Size (1)
0x05, 0x08,                        // Usage Page (Page# for LEDs)
0x19, 0x01,                        // Usage Minimum (1)
0x29, 0x05,                        // Usage Maximum (5)
0x91, 0x02,                        // Output (Data, Variable, Absolute) -- LED report
0x95, 0x01,                        // Report Count (1)
0x75, 0x03,                        // Report Size (3)
0x91, 0x03,                        // (91 03) Output (Constant) -- LED report padding
0x95, 0x06,                        // Report Count (6)
0x75, 0x08,                        // Report Size (8)
0x15, 0x00,                        // Logical Minimum (0)
0x25, 0x66,                        // Logical Maximum(102)  // was 0x65
0x05, 0x07,                        // Usage Page (Key Codes)
0x19, 0x00,                        // Usage Minimum (0)
0x29, 0x66,                        // Usage Maximum (102) // was 0x65
0x81, 0x00,                        // Input (Data, Array) -- Key arrays (6 bytes)
0xC0                               // End Collection
```