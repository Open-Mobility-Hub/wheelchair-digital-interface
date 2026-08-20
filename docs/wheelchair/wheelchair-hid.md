# Wheelchair HID

## Version
- Version 3.2
- May 20, 2026

## Description
- The Wheelchair HID is intended for bidirectional communication between a Wheelchair host Wheelchair Digital Interface (WDI) implementation and a Bluetooth LE or USB connected App or Device.
- A Wheelchair Control HID Descriptor is defined for an App or Device to send HID reports to the Wheelchair host WDI implementation.
- A Wheelchair Keepalive HID Descriptor is defined for an App or Device to send keepalive reports to the Wheelchair host WDI implementation.
- A Wheelchair Keepalive Response HID Descriptor is defined for the Wheelchair host WDI implementation to send a response to the App or Device upon receiving a Keepalive report.
- A Wheelchair Request Feedback HID Descriptor is defined for an App or Device to request that the Wheelchair host WDI implementation send a Wheelchair Feedback HID report.
- A Wheelchair Feedback HID Descriptor is defined for a Wheelchair host WDI implementation to send Wheelchair Feedback HID reports to an App or Device.

## Keepalive
- A mandatory Keepalive report shall be sent from an App or Device to the Wheelchair host WDI implementation. Apps and Devices must begin sending Keepalive reports after a stable connection is established. The App or Device shall send a Keepalive report every ~233ms. Sending a control report or request feedback report resets the keepalive timer. If a control report or request feedback report has been sent since the last keepalive timer reset, no keepalive report is required until 233ms after the most recent sent report (keepalive, control, or request feedback). Control reports and request feedback reports are not constrained by the 233ms keepalive interval. Control reports may be sent at any rate, subject to release report timing requirements (see Sending Release Reports). Request feedback reports have their own recommended interval (see Request Feedback Timing). This allows the App or Device to avoid transmit congestion by not sending unnecessary keepalive reports when control or request feedback reports are already being sent.
- The Wheelchair host WDI implementation shall handle the Keepalive reports. 
- The Wheelchair host WDI implementation shall check that a keepalive report, control report, or request feedback report is received at least every 257ms.
- The Wheelchair host WDI implementation shall send a Keepalive Response report to the App or Device upon receiving a Keepalive report. The Keepalive Response report contains a cryptographically unique host UUID (16 bytes). The first two bytes of the host UUID encode a 16-bit manufacturer ID identifying the wheelchair manufacturer (see Appendix F). The App or Device shall use the Keepalive Response report to identify the Wheelchair host WDI implementation, and may extract the manufacturer ID from the host UUID to identify the manufacturer.
- For Bluetooth LE connections, in the case of the first time an app or device is connected to a Wheelchair host WDI implementation, after receiving the first Keepalive Response report the app or device shall save the host ID for subsequent connection checks.
- For subsequent Bluetooth LE connections, after receiving the first Keepalive Response report the app or device shall compare the received host ID against the saved host ID. If the host IDs match proceed as normal. If the host IDs do not match then the app or device shall stop sending all reports (keepalive, control, and request feedback) in order to trigger a Wheelchair host WDI implementation disconnect. After this particular disconnect the app or device shall delay advertising for 15 seconds.
- The app or device shall provide a mechanism to clear a saved host ID.
- The app or device should provide a way for a user to see the host ID. The full 16-byte host UUID shall be displayed (e.g., in standard string form); displaying only a partial form (such as a truncated UUID, hash, or the manufacturer name alone) is not sufficient.
- For Bluetooth LE connections, the Wheelchair host WDI implementation shall disconnect the Bluetooth LE connection if three consecutive report timeouts occur (no keepalive, control, or request feedback report received within three consecutive 257ms windows). The Wheelchair host WDI implementation shall treat this as a Release Report and Disable Drive.
- For USB connections, if three consecutive report timeouts occur (no keepalive, control, or request feedback report received within three consecutive 257ms windows), the Wheelchair host WDI implementation shall treat this as a Release Report and Disable Drive.

## Disconnects
- The Wheelchair host WDI implementation shall handle every disconnect from Wheelchair HID or any other HID.
- For both Bluetooth LE and USB connections, the Wheelchair host WDI implementation shall treat HID disconnects as a Release Report and Disable Drive.

---

## Wheelchair Control HID

### Wheelchair Control HID Descriptor
- x coordinate SInt8  -127 left to 127 right
- y coordinate SInt8  -127 forward to 127 reverse
- WDI Standard1 UInt32  Bit flags
- WDI Standard2 UInt32  Bit flags
- WDI Vendor Specific1 UInt32  Bit flags
- WDI Vendor Specific2 UInt32  Bit flags

## Wheelchair Control HID Release Report
- x = 0
- y = 0
- Standard1 = 0
- Standard2 = 0
- Vendor1 = 0
- Vendor2 = 0

### WDI Standard1 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Modifier |
| 1 | Stop |
| 2 | Drive Enable |
| 3 | Cycle Profile |
| 4 | Hazards |
| 5 | Cycle Mode |
| 6 | Speed Down |
| 7 | Speed Up |
| 8 | Left Blinker |
| 9 | Right Blinker |
| 10 | Menu |
| 11 | Profile Up |
| 12 | Drive Disable |
| 13 | Headlights |
| 14 | Horn |
| 15 | Profile Down |
| 16 | Memory 1 |
| 17 | Memory 2 |
| 18 | Memory 3 |
| 19 | Memory 4 |
| 20 | Memory 5 |
| 21 | Memory 6 |
| 22 | Memory Home |
| 23 | Reserved for future use |
| 24 | Tilt Forward |
| 0+24 | Tilt Backward |
| 25 | Recline Forward |
| 0+25 | Recline Backward |
| 26 | Legs Up |
| 0+26 | Legs Down |
| 27 | Elevate Up |
| 0+27 | Elevate Down |
| 28 | Footplates Up |
| 0+28 | Footplates Down |
| 29 | Stand Up |
| 0+29 | Stand Down |
| 30 | Seat Reserved for future use1 Up |
| 0+30 | Seat Reserved for future use1 Down |
| 31 | Seat Reserved for future use2 Up |
| 0+31 | Seat Reserved for future use2 Down |


### WDI Standard2 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Modifier |
| 1 | Reserved for future use |
| 2 | Reserved for future use |
| 3 | Reserved for future use |
| 4 | Reserved for future use |
| 5 | Reserved for future use |
| 6 | Reserved for future use |
| 7 | Reserved for future use |
| 8 | Reserved for future use |
| 9 | Reserved for future use |
| 10 | Reserved for future use |
| 11 | Reserved for future use |
| 12 | Reserved for future use |
| 13 | Reserved for future use |
| 14 | Reserved for future use |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |


### WDI Vendor Specific Bit Interpretation
The `WDI Vendor Specific1` and `WDI Vendor Specific2` fields form a per-manufacturer namespace. Bit 0 is the Modifier bit; the Modifier convention itself ("modifier active") is shared at the spec level, but each manufacturer may pair the Modifier with its own bit assignments to define alternate functions, following the `0+X` notation used in Standard1. Each manufacturer defines bits 1–31 of these fields, and any Modifier-paired interpretations of them, independently — the same bit number, and the same Modifier-paired combination, may carry entirely different meanings for different manufacturers. This specification lists bits 1–31 as "Reserved for future use" because the main spec is manufacturer-agnostic; the actual definitions live in each manufacturer's own vendor document.

The 16-bit manufacturer ID at bytes 0–1 of the Host UUID in the Keepalive Response report (see Appendix F: Manufacturer IDs) identifies which manufacturer's vendor document applies for a given host. Vendor documents are maintained separately (see [Vendors](vendors/vendors.md)). An App or Device shall extract the manufacturer ID and apply that manufacturer's vendor document when interpreting (or generating) `WDI Vendor Specific1` and `WDI Vendor Specific2` for that host.

### WDI Vendor Specific1 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Modifier |
| 1 | Reserved for future use |
| 2 | Reserved for future use |
| 3 | Reserved for future use |
| 4 | Reserved for future use |
| 5 | Reserved for future use |
| 6 | Reserved for future use |
| 7 | Reserved for future use |
| 8 | Reserved for future use |
| 9 | Reserved for future use |
| 10 | Reserved for future use |
| 11 | Reserved for future use |
| 12 | Reserved for future use |
| 13 | Reserved for future use |
| 14 | Reserved for future use |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |


### WDI Vendor Specific2 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Modifier |
| 1 | Reserved for future use |
| 2 | Reserved for future use |
| 3 | Reserved for future use |
| 4 | Reserved for future use |
| 5 | Reserved for future use |
| 6 | Reserved for future use |
| 7 | Reserved for future use |
| 8 | Reserved for future use |
| 9 | Reserved for future use |
| 10 | Reserved for future use |
| 11 | Reserved for future use |
| 12 | Reserved for future use |
| 13 | Reserved for future use |
| 14 | Reserved for future use |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |

---

## Wheelchair Request Feedback HID

### Description
- The Wheelchair Request Feedback HID report is sent from an App or Device to request that the Wheelchair host WDI implementation send a full Wheelchair Feedback HID report in response.
- Sending this report is the only mechanism for an App or Device to request feedback.

### Request Feedback Timing
- For periodic request/response scenarios, a greater than 0.750 second (>750 milliseconds) interval is recommended.

### Wheelchair Request Feedback HID Descriptor
- Request UInt8  (shall be set to 0x01)

### Wheelchair Request Feedback HID Report
- Request = 0x01

---

## Wheelchair Keepalive HID

### Description
- The Wheelchair Keepalive HID report is sent from an App or Device to indicate to the Wheelchair host WDI implementation that the connection is active.
- Sending this report is mandatory.
- Keepalives shall be used over both Bluetooth LE and USB connections.

### Wheelchair Keepalive HID Descriptor
- Keepalive UInt8  (shall be set to 0x01)

### Wheelchair Keepalive HID Report
- Keepalive = 0x01

---

## Wheelchair Keepalive Response HID

### Description
- The Wheelchair Keepalive Response HID report is sent from the Wheelchair host WDI implementation to the App or Device in response to receiving a Keepalive report.
- Sending this report is mandatory upon receiving a Keepalive report.
- The report contains a cryptographically unique host UUID that identifies the Wheelchair host.
- The first two bytes of the host UUID encode a 16-bit manufacturer ID that identifies the wheelchair manufacturer (see Appendix F).
- The App or Device shall use the Keepalive Response report to identify the Wheelchair host WDI implementation.
- The App or Device may extract the manufacturer ID from the first two bytes of the host UUID to identify the wheelchair manufacturer.

### Wheelchair Keepalive Response HID Descriptor
- Host UUID UInt8[16]  (128-bit UUID, 16 bytes, transmitted in big-endian / network byte order)

### Wheelchair Keepalive Response HID Report
- Host UUID = 16-byte cryptographically unique identifier
  - Bytes 0–1: 16-bit manufacturer ID, big-endian (see Appendix F)
  - Bytes 2–15: cryptographically random, with RFC 4122 version 4 and variant markers preserved (see Host UUID Requirements)

### Host UUID Requirements
- The Host UUID shall be a valid RFC 4122 version 4 (random) UUID.
- The Host UUID shall be cryptographically unique to the Wheelchair host WDI implementation.
- The Host UUID shall remain constant for the lifetime of the Wheelchair host WDI implementation.
- The 16 bytes shall be transmitted in big-endian / network byte order. Byte 0 of the report corresponds to the leftmost hex pair of the UUID in standard string form (`xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`).
- Bytes 0–1 shall contain the 16-bit manufacturer ID in big-endian order (see Appendix F for assigned values).
- Bytes 2–15 shall be generated to ensure cryptographic uniqueness across hosts from the same manufacturer.
- The high nibble of byte 6 shall be `0x4` (UUID version 4 marker).
- The top two bits of byte 8 shall be `0b10` (RFC 4122 variant marker).
- A manufacturer that has not been assigned an ID shall use `0x0000` (unknown / unassigned, see Appendix F).

### Manufacturer ID Extraction
- Apps and Devices may parse bytes 0–1 of the host UUID as a big-endian 16-bit unsigned integer to obtain the manufacturer ID.
- Apps and Devices may use the manufacturer ID to display the manufacturer name, filter or categorize known hosts, or apply manufacturer-specific behavior.
- The full 16-byte host UUID, not the manufacturer ID alone, shall continue to be used for host identity (save / compare / display) per the Keepalive section.

---

## Wheelchair Feedback HID

### Wheelchair Feedback Frequency
- The Wheelchair host WDI implementation should decide when it is appropriate to send Wheelchair Feedback HID reports.
- A Wheelchair Request Feedback HID report is defined for a request/response scenario where the App or Device can send a Request Feedback HID report and the Wheelchair host WDI implementation should send a full Wheelchair Feedback HID report in response.
- The Wheelchair host WDI implementation shall always send a full Wheelchair Feedback HID report containing all fields. If any values are unknown or unavailable the corresponding bits or bytes shall be set to 0.
- If an App or Device has been receiving Wheelchair Feedback HID reports and the reports stop arriving, the App or Device should treat the previously received feedback data as stale and should not rely on it for decision-making or display purposes.

### Wheelchair Feedback HID Descriptor
- WDI Standard UInt32  Bit flags
- WDI Vendor Specific1 UInt32  Bit flags
- WDI Vendor Specific2 UInt32  Bit flags
- Speed/Profile UInt8  Packed nibbles
- Velocity UInt8  Packed nibbles
- Odometer UInt8
- Reserved for future use UInt8
- Reserved for future use UInt8
- Reserved for future use UInt8
- Reserved for future use UInt8

### Speed/Profile Byte

| Bits | Field | Description |
|------|-------|-------------|
| 7:4 | Speed | Speed setting; 0 = unknown, 1–15 = valid |
| 3:0 | Profile | Profile index; 0 = unknown, 1–15 = valid |

### Velocity Byte

| Bits | Field | Description |
|------|-------|-------------|
| 7:4 | Whole | Whole mph (0–15) |
| 3:0 | Fraction | Tenths of mph (0–9 valid) |

Velocity in mph = Whole + (Fraction ÷ 10)

Range: 0.0 to 15.9 mph

Note: Fraction values 10–15 (0xA–0xF) are reserved.

### WDI Standard Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Drive is Disabled |
| 1 | Drive is Enabled |
| 2 | Mode is Drive |
| 3 | Mode is Seating |
| 4 | Left Blinker is off |
| 5 | Left Blinker is on |
| 6 | Right Blinker is off |
| 7 | Right Blinker is on |
| 8 | Headlights are off|
| 9 | Headlights are on|
| 10 | Hazards are off |
| 11 | Hazards are on |
| 12 | No Movement Restriction |
| 13 | Limited Speed |
| 14 | No Movement |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |


### WDI Vendor Specific Bit Interpretation

The `WDI Vendor Specific1` and `WDI Vendor Specific2` fields of the Feedback report form a per-manufacturer namespace. All 32 bits of each field are fully available to every manufacturer independently — the same bit number may carry entirely different meanings for different manufacturers. This specification lists all bits as "Reserved for future use" because the main spec is manufacturer-agnostic; the actual definitions live in each manufacturer's own vendor document.

The 16-bit manufacturer ID at bytes 0–1 of the Host UUID in the Keepalive Response report (see Appendix F: Manufacturer IDs) identifies which manufacturer's vendor document applies for a given host. Vendor documents are maintained separately (see [Vendors](vendors/vendors.md)). An App or Device shall extract the manufacturer ID and apply that manufacturer's vendor document when interpreting `WDI Vendor Specific1` and `WDI Vendor Specific2` from that host's Feedback reports.

### WDI Vendor Specific1 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Reserved for future use |
| 1 | Reserved for future use |
| 2 | Reserved for future use |
| 3 | Reserved for future use |
| 4 | Reserved for future use |
| 5 | Reserved for future use |
| 6 | Reserved for future use |
| 7 | Reserved for future use |
| 8 | Reserved for future use |
| 9 | Reserved for future use |
| 10 | Reserved for future use |
| 11 | Reserved for future use |
| 12 | Reserved for future use |
| 13 | Reserved for future use |
| 14 | Reserved for future use |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |


### WDI Vendor Specific2 Bits

| Bit | Function Name |
|-----|---------------|
| 0 | Reserved for future use |
| 1 | Reserved for future use |
| 2 | Reserved for future use |
| 3 | Reserved for future use |
| 4 | Reserved for future use |
| 5 | Reserved for future use |
| 6 | Reserved for future use |
| 7 | Reserved for future use |
| 8 | Reserved for future use |
| 9 | Reserved for future use |
| 10 | Reserved for future use |
| 11 | Reserved for future use |
| 12 | Reserved for future use |
| 13 | Reserved for future use |
| 14 | Reserved for future use |
| 15 | Reserved for future use |
| 16 | Reserved for future use |
| 17 | Reserved for future use |
| 18 | Reserved for future use |
| 19 | Reserved for future use |
| 20 | Reserved for future use |
| 21 | Reserved for future use |
| 22 | Reserved for future use |
| 23 | Reserved for future use |
| 24 | Reserved for future use |
| 25 | Reserved for future use |
| 26 | Reserved for future use |
| 27 | Reserved for future use |
| 28 | Reserved for future use |
| 29 | Reserved for future use |
| 30 | Reserved for future use |
| 31 | Reserved for future use |

---

## Appendix A: Wheelchair HID Descriptor
```
0x06, 0x00, 0xFF,        // Usage Page (Vendor Defined 0xFF00)
0x09, 0x01,              // Usage (Vendor Usage 0x01 - Wheelchair Control Device)
0xA1, 0x01,              // Collection (Application)

// ========== Report ID 0x01: Wheelchair Control (Input from App/Device) ==========
0x85, 0x01,              //   Report ID (1)
0x09, 0x10,              //   Usage (X Coordinate)
0x09, 0x11,              //   Usage (Y Coordinate)
0x15, 0x81,              //   Logical Minimum (-127)
0x25, 0x7F,              //   Logical Maximum (127)
0x75, 0x08,              //   Report Size (8 bits)
0x95, 0x02,              //   Report Count (2)
0x81, 0x02,              //   Input (Data, Variable, Absolute)

0x09, 0x20,              //   Usage (WDI Standard1)
0x09, 0x21,              //   Usage (WDI Standard2)
0x09, 0x22,              //   Usage (WDI Vendor Specific1)
0x09, 0x23,              //   Usage (WDI Vendor Specific2)
0x15, 0x00,              //   Logical Minimum (0)
0x27, 0xFF, 0xFF, 0xFF, 0x7F,  //   Logical Maximum (0x7FFFFFFF)
0x75, 0x20,              //   Report Size (32 bits)
0x95, 0x04,              //   Report Count (4)
0x81, 0x02,              //   Input (Data, Variable, Absolute)

// ========== Report ID 0x02: Wheelchair Feedback (Output to App/Device) ==========
0x85, 0x02,              //   Report ID (2)
0x09, 0x30,              //   Usage (WDI Feedback Standard)
0x09, 0x31,              //   Usage (WDI Feedback Vendor Specific1)
0x09, 0x32,              //   Usage (WDI Feedback Vendor Specific2)
0x15, 0x00,              //   Logical Minimum (0)
0x27, 0xFF, 0xFF, 0xFF, 0x7F,  //   Logical Maximum (0x7FFFFFFF)
0x75, 0x20,              //   Report Size (32 bits)
0x95, 0x03,              //   Report Count (3)
0x91, 0x02,              //   Output (Data, Variable, Absolute)

0x09, 0x33,              //   Usage (Speed/Profile)
0x09, 0x34,              //   Usage (Velocity)
0x09, 0x35,              //   Usage (Odometer)
0x09, 0x36,              //   Usage (Reserved1)
0x09, 0x37,              //   Usage (Reserved2)
0x09, 0x38,              //   Usage (Reserved3)
0x09, 0x39,              //   Usage (Reserved4)
0x15, 0x00,              //   Logical Minimum (0)
0x26, 0xFF, 0x00,        //   Logical Maximum (255)
0x75, 0x08,              //   Report Size (8 bits)
0x95, 0x07,              //   Report Count (7)
0x91, 0x02,              //   Output (Data, Variable, Absolute)

// ========== Report ID 0x03: Request Feedback (Input from App/Device) ==========
0x85, 0x03,              //   Report ID (3)
0x09, 0x40,              //   Usage (WDI Request Feedback)
0x15, 0x00,              //   Logical Minimum (0)
0x25, 0xFF,              //   Logical Maximum (255)
0x75, 0x08,              //   Report Size (8 bits)
0x95, 0x01,              //   Report Count (1)
0x81, 0x02,              //   Input (Data, Variable, Absolute)

// ========== Report ID 0x04: Keepalive (Input from App/Device) ==========
0x85, 0x04,              //   Report ID (4)
0x09, 0x50,              //   Usage (WDI Keepalive)
0x15, 0x00,              //   Logical Minimum (0)
0x25, 0xFF,              //   Logical Maximum (255)
0x75, 0x08,              //   Report Size (8 bits)
0x95, 0x01,              //   Report Count (1)
0x81, 0x02,              //   Input (Data, Variable, Absolute)

// ========== Report ID 0x05: Keepalive Response (Output to App/Device) ==========
0x85, 0x05,              //   Report ID (5)
0x09, 0x51,              //   Usage (WDI Keepalive Response Host UUID)
0x15, 0x00,              //   Logical Minimum (0)
0x26, 0xFF, 0x00,        //   Logical Maximum (255)
0x75, 0x08,              //   Report Size (8 bits)
0x95, 0x10,              //   Report Count (16)
0x91, 0x02,              //   Output (Data, Variable, Absolute)

0xC0                     // End Collection
```
---

## Appendix B: UUID Scheme

### Why Custom UUIDs

The standard Bluetooth HID Service UUID (0x1812) is restricted on mobile platforms. Applications cannot advertise or fully control GATT services using standard HID UUIDs. Custom UUIDs provide full control over the BLE stack while maintaining standard HID report formats.

### UUID Structure

All custom UUIDs share a cryptographically random base with structured increments:

```
10A5xxxx-C4EA-4B47-AE30-A7D9577FC3F9
    ^^^^
    Incrementing identifier (0001-000A)
```

### UUID Assignments

| Purpose | UUID | Replaces |
|---------|------|----------|
| Wheelchair HID Service | `10A50001-C4EA-4B47-AE30-A7D9577FC3F9` | 0x1812 |
| Report Map | `10A50002-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4B |
| HID Information | `10A50003-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4A |
| HID Control Point | `10A50004-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4C |
| Protocol Mode | `10A50005-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4E |
| Input Report (Control) | `10A50006-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4D |
| Output Report (Feedback) | `10A50007-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4D |
| Input Report (Request Feedback) | `10A50008-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4D |
| Input Report (Keepalive) | `10A50009-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4D |
| Output Report (Keepalive Response) | `10A5000A-C4EA-4B47-AE30-A7D9577FC3F9` | 0x2A4D |

### What Remains Standard

Despite custom UUIDs, the following adhere to Bluetooth HID specifications:

- **HID Descriptor format** - Standard USB HID descriptor in Report Map
- **Report data format** - 18-byte Control, 1-byte Request Feedback, 1-byte Keepalive, 16-byte Keepalive Response, 19-byte Feedback per spec
- **Descriptor UUIDs** - CCCD (0x2902) and Report Reference (0x2908). CoreBluetooth 0x2901 and 0x2904
- **HID Information value** - bcdHID 0x0111, flags per HOGP spec

### Coexistence with Standard HID

Custom UUIDs ensure complete isolation from standard HID handling. Standard BLE HID devices (keyboards, gamepads) using 0x1812 are handled by the operating system, while Wheelchair HID devices are handled exclusively by the custom application. Both can operate simultaneously without conflict.

---

## Appendix C: Scanning and Connection (Central)

### C.0 System Configuration

| Requirement | Level | Description |
|-------------|-------|-------------|
| Enable/Disable Option | **RECOMMENDED** | Wheelchair HID WDI implementations SHOULD provide a configuration option in their system settings to enable and disable BLE Wheelchair HID. |
| Default State | **RECOMMENDED** | If an enable/disable option is provided, BLE Wheelchair HID SHOULD be disabled by default. |
| Automatic Operation | **MANDATORY** | When BLE Wheelchair HID is enabled (or if no enable/disable option exists), the implementation SHALL automatically scan for and connect to apps and devices advertising the Wheelchair HID Service UUID. No additional user action should be required. |

**Rationale:** Providing an enable/disable option with a disabled default ensures users consciously choose to allow BLE control of their wheelchair, preventing unintended connections. The automatic scan-and-connect behavior when enabled provides a seamless user experience.

### C.1 Scanning Mode

| Requirement | Level | Description |
|-------------|-------|-------------|
| Active Scanning | **MANDATORY** | The 128-bit service UUID (16 bytes) typically cannot fit in the 31-byte advertising packet alongside other required data. Peripherals commonly place the service UUID in the scan response. Active scanning is required to receive scan response data. |
| Service UUID Filter | **MANDATORY** | Filter for the Wheelchair HID Service UUID (`10A50001-C4EA-4B47-AE30-A7D9577FC3F9`) to avoid connecting to unrelated devices. |

### C.2 Scanning Parameters

| Parameter | Reference Value | Recommended Range | Rationale |
|-----------|-----------------|-------------------|-----------|
| Scan Window | 150ms | ≥150ms | Should be large enough to catch at least one advertisement from slow advertisers. iOS background apps advertise every 1-2 seconds; a 150ms window with 200ms interval (~75% duty) will reliably catch these within a few scan cycles. |
| Scan Interval | 200ms | ≤200ms | Combined with 150ms window, provides ~75% duty cycle during active scanning. Scan Interval must be ≥ Scan Window per the BLE spec. |
| Scan Duration | 5 seconds | 3-10 seconds | Long enough to catch slow advertisers even with 1-2 second advertising intervals. |
| Pause Duration | 3 seconds | 2-5 seconds | Reduces power consumption and RF congestion between scan cycles. |

### C.3 Reconnection

| Requirement | Level | Description |
|-------------|-------|-------------|
| Auto-Restart on Disconnect | **RECOMMENDED** | Resume scanning immediately after an unexpected disconnect for quick reconnection. |
| Resume Scanning on Discovery Failure | **MANDATORY** | If service or characteristic discovery fails after connecting, disconnect and resume scanning to find a valid peripheral. |

### C.4 Pairing and Bonding

| Requirement | Level | Description |
|-------------|-------|-------------|
| No Bonding Required | **MANDATORY** | The Central SHALL NOT require bonding. Many peripherals (especially mobile apps) do not support or want bonding for this use case. |
| Accept Unencrypted Connections | **MANDATORY** | The Central SHALL accept unencrypted connections. |
| Just Works Pairing | **MANDATORY** | The Central SHALL support and initiate Just Works BLE pairing. |
| Other Pairing Methods | **MANDATORY** | The Central SHALL NOT require other forms of pairing. The Central MAY respond to peripheral-initiated pairing. |

---

## Appendix D: Bluetooth LE Protocol Details (Central)

### D.1 Service and Characteristic Discovery

| Requirement | Level | Description |
|-------------|-------|-------------|
| Discover Wheelchair HID Service | **MANDATORY** | Discover service UUID `10A50001-C4EA-4B47-AE30-A7D9577FC3F9`. If not found, disconnect and resume scanning. |
| Discover Input Report Characteristic | **MANDATORY** | Discover characteristic UUID `10A50006-C4EA-4B47-AE30-A7D9577FC3F9`. This is required for receiving Control reports. If not found, disconnect and resume scanning. |
| Discover Output Report Characteristic | **RECOMMENDED** | Discover characteristic UUID `10A50007-C4EA-4B47-AE30-A7D9577FC3F9`. This is optional; some simple peripherals may not implement feedback. If not found, continue without feedback capability. |
| Discover Request Feedback Characteristic | **RECOMMENDED** | Discover characteristic UUID `10A50008-C4EA-4B47-AE30-A7D9577FC3F9`. This is optional; some simple peripherals may not implement request feedback. If not found, continue without request feedback capability. |
| Discover Keepalive Characteristic | **MANDATORY** | Discover characteristic UUID `10A50009-C4EA-4B47-AE30-A7D9577FC3F9`. This is required for receiving Keepalive reports. If not found, disconnect and resume scanning. |
| Discover Keepalive Response Characteristic | **MANDATORY** | Discover characteristic UUID `10A5000A-C4EA-4B47-AE30-A7D9577FC3F9`. This is required for sending Keepalive Response reports. If not found, disconnect and resume scanning. |
| Enable Notifications on Input Report | **MANDATORY** | If this fails, disconnect and resume scanning. |
| Enable Notifications on Request Feedback | **RECOMMENDED** | If the Request Feedback characteristic is discovered, enable notifications to receive feedback requests. If this fails, continue without request feedback capability. |
| Enable Notifications on Keepalive | **MANDATORY** | Enable notifications on the Keepalive characteristic to receive keepalive reports. If this fails, disconnect and resume scanning. |

### D.2 Characteristic Properties

| Characteristic | UUID | Required Properties |
|----------------|------|---------------------|
| Input Report (Control) | `10A50006-...` | Read, Notify |
| Output Report (Feedback) | `10A50007-...` | Read, Write Without Response |
| Input Report (Request Feedback) | `10A50008-...` | Read, Notify |
| Input Report (Keepalive) | `10A50009-...` | Read, Notify |
| Output Report (Keepalive Response) | `10A5000A-...` | Read, Write Without Response |

### D.3 Data Transfer

| Requirement | Level | Description |
|-------------|-------|-------------|
| Receive Notifications | **MANDATORY** | Control reports (18 bytes) arrive as notifications on the Input Report characteristic. Receiving a Control report resets the keepalive timeout timer. |
| Receive Request Feedback Notifications | **RECOMMENDED** | Request Feedback reports (1 byte) arrive as notifications on the Request Feedback characteristic. Upon receipt, the Central should send a full Wheelchair Feedback HID report. Receiving a Request Feedback report resets the keepalive timeout timer. |
| Receive Keepalive Notifications | **MANDATORY** | Keepalive reports (1 byte) arrive as notifications on the Keepalive characteristic. Upon receipt, the Central shall reset its keepalive timeout timer and send a Keepalive Response report. |
| Send Keepalive Response | **MANDATORY** | Upon receiving a Keepalive report, send a Keepalive Response report (16 bytes) containing the host UUID using Write Without Response on the Keepalive Response characteristic. |
| Write Without Response | **MANDATORY** | Send Feedback reports (19 bytes) using Write Without Response for lowest latency. Do not use Write With Response. |
| Validate Report Size | **RECOMMENDED** | Discard Control reports that are not exactly 18 bytes. Discard Request Feedback reports that are not exactly 1 byte. Discard Keepalive reports that are not exactly 1 byte. |

### D.4 Connection Parameters

| Requirement | Level | Description |
|-------------|-------|-------------|
| Do Not Request Parameters | **RECOMMENDED** | The Central SHOULD NOT request specific connection parameters. Mobile peripherals (iOS, Android) manage connection parameters and will request their preferred values. Conflicting requests can cause connection instability. |
| Accept Parameter Updates | **MANDATORY** | The Central SHALL accept connection parameter update requests from the peripheral. |
| Supervision Timeout | **RECOMMENDED** | Accept supervision timeouts of 2-6 seconds as typically requested by mobile devices. |

### D.5 MTU Considerations

| Requirement | Level | Description |
|-------------|-------|-------------|
| Default MTU Sufficient | **INFORMATIONAL** | The default BLE MTU (23 bytes, 20 byte payload) is sufficient for Control (18 bytes), Request Feedback (1 byte), Keepalive (1 byte), Keepalive Response (16 bytes), and Feedback (19 bytes) reports. MTU negotiation is not required. |
| Accept MTU Exchange | **RECOMMENDED** | If the peripheral initiates MTU exchange, accept it. Larger MTU does not affect report sizes but may improve throughput for other characteristics. |

### D.6 Keepalive Handling

Per the main specification (Section: Keepalive), keepalive is mandatory:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Monitor Keepalive After First Received | **MANDATORY** | Begin keepalive monitoring only after receiving the first Keepalive report (Report ID 4) on the Keepalive characteristic. |
| Check Interval | **MANDATORY** | Check that a keepalive, control, or request feedback report is received at least every 257ms after monitoring begins. |
| Send Keepalive Response | **MANDATORY** | Upon receiving a Keepalive report, immediately send a Keepalive Response report (Report ID 5) containing the host UUID (16 bytes, with the 16-bit manufacturer ID in bytes 0–1 — see Appendix F) on the Keepalive Response characteristic. |
| Disconnect on Missed Reports | **MANDATORY** | Disconnect the BLE connection if 3 consecutive report timeouts occur (no keepalive, control, or request feedback report received within three consecutive 257ms windows). |
| Grace Period Before First Keepalive | **MANDATORY** | Do not enforce keepalive timeout until the first Keepalive report is received. This allows time for connection setup. |

### D.7 Disconnect Handling

Per the main specification (Section: Disconnects):

| Requirement | Level | Description |
|-------------|-------|-------------|
| Process Release Report | **MANDATORY** | Upon any BLE disconnect, the Central shall immediately process a Release Report (all zeros) internally.  |
| Process Drive Disable | **MANDATORY** | After the Release Report internal processing, Disable Drive. |
| Resume Scanning | **MANDATORY** | After handling disconnect, resume scanning for a new peripheral. |
| Clear State | **MANDATORY** | Reset keepalive monitoring state and any cached report data on disconnect. |

### D.8 Error Recovery

| Scenario | Required Action |
|----------|-----------------|
| Service not found after connect | Disconnect, resume scanning |
| Input Report characteristic not found | Disconnect, resume scanning |
| Notification enable fails | Disconnect, resume scanning |
| Output Report characteristic not found | Continue without feedback (log warning) |
| Request Feedback characteristic not found | Continue without request feedback (log warning) |
| Keepalive characteristic not found | Disconnect, resume scanning |
| Keepalive Response characteristic not found | Disconnect, resume scanning |
| Write to Output Report fails | Log warning, continue operation |
| Write to Keepalive Response fails | Log warning, continue operation |
| Notification received with wrong size | Discard report, log warning, continue |
| BLE disconnect (any reason) | Process Release Report, process Drive Disable, resume scanning |
| Report timeout (3 consecutive misses) | Disconnect BLE, process Release Report, process Drive Disable, resume scanning |

### D.9 UUID Byte Order

This section addresses two distinct UUID byte-order conventions in the spec. They apply to different layers and should not be conflated.

**1. BLE service and characteristic UUIDs (framing layer):** little-endian on the wire.

**2. Application-payload UUIDs (e.g., the Host UUID in the Keepalive Response report):** canonical RFC 4122 byte order (big-endian / network order). Byte 0 of the payload corresponds to the leftmost hex pair of the UUID string form, matching the in-memory representation expected by standard UUID libraries (`CBUUID`, `java.util.UUID`, `uuid.UUID(bytes=...)`, `System.Guid`, etc.). See the Wheelchair Keepalive Response HID section for the Host UUID definition, including the 16-bit manufacturer ID at bytes 0–1 (see Appendix F).

The remainder of this section describes convention (1) — BLE framing UUIDs.

BLE UUIDs are transmitted and stored in little-endian byte order. The Wheelchair HID Service UUID in various formats:

| Format | Value |
|--------|-------|
| Standard (big-endian) | `10A50001-C4EA-4B47-AE30-A7D9577FC3F9` |
| Byte array (little-endian) | `F9 C3 7F 57 D9 A7 30 AE 47 4B EA C4 01 00 A5 10` |

To derive other UUIDs, replace bytes 12-13 (positions counting from 0) with the short UUID in little-endian:

| Short UUID | Bytes 12-13 | Full UUID |
|------------|-------------|-----------|
| 0x0001 | `01 00` | Service |
| 0x0002 | `02 00` | Report Map |
| 0x0003 | `03 00` | HID Information |
| 0x0004 | `04 00` | HID Control Point |
| 0x0005 | `05 00` | Protocol Mode |
| 0x0006 | `06 00` | Input Report (Control) |
| 0x0007 | `07 00` | Output Report (Feedback) |
| 0x0008 | `08 00` | Input Report (Request Feedback) |
| 0x0009 | `09 00` | Input Report (Keepalive) |
| 0x000A | `0A 00` | Output Report (Keepalive Response) |

### D.10 Summary of Mandatory Requirements (Central)

A compliant Wheelchair HID BLE Central implementation MUST:

1. When BLE Wheelchair HID is active, automatically scan for and connect to peripherals advertising the service UUID
2. Use active scanning with service UUID filtering
3. Not require bonding or pairing other than Just Works BLE pairing
4. Accept unencrypted connections
5. Discover the Wheelchair HID Service
6. Discover and enable notifications on the Input Report characteristic
7. Accept connection parameter updates from the peripheral
8. Monitor keepalive timing only after first Keepalive report is received
9. Disconnect after 3 consecutive report timeouts (257ms windows with no keepalive, control, or request feedback report)
10. Process a Release Report (all zeros) internally on any BLE disconnect
11. Disable Drive internally after the Release Report on disconnect
12. Resume scanning after disconnect or discovery failure
13. Discover and enable notifications on the Keepalive characteristic
14. Discover the Keepalive Response characteristic
15. Send a Keepalive Response report (16-byte host UUID, with the 16-bit manufacturer ID in bytes 0–1 per Appendix F) upon receiving each Keepalive report
16. Reset the keepalive timeout timer upon receiving a control report or request feedback report, in addition to keepalive reports

A compliant implementation SHOULD:

17. Provide a system configuration option to enable/disable BLE Wheelchair HID
18. Default to BLE Wheelchair HID disabled if such an option is provided
19. Implement Request Feedback characteristic to receive feedback requests and respond with a full Wheelchair Feedback HID report

---

## Appendix E: Peripheral Implementation Guidelines

### E.1 Advertising

#### E.1.1 Advertising Data

| Requirement | Level | Description |
|-------------|-------|-------------|
| Advertise Service UUID | **MANDATORY** | Include the Wheelchair HID Service UUID (`10A50001-C4EA-4B47-AE30-A7D9577FC3F9`) in advertising data or scan response. |
| Connectable Advertising | **MANDATORY** | Use connectable undirected advertising (ADV_IND). |
| General Discoverable | **RECOMMENDED** | Set the General Discoverable flag in advertising data. |

#### E.1.2 Advertising Packet Structure

The 31-byte advertising packet limit typically requires splitting data:

**Advertising Packet (ADV_IND):**
| Field | Size | Content |
|-------|------|---------|
| Flags | 3 bytes | `02 01 06` (General Discoverable, BR/EDR Not Supported) |
| Local Name | variable | Short or complete local name |
| TX Power (optional) | 3 bytes | Transmission power level |

**Scan Response:**
| Field | Size | Content |
|-------|------|---------|
| Complete 128-bit Service UUID | 18 bytes | `11 07` + 16-byte UUID (little-endian) |
| Additional data (optional) | remaining | Manufacturer data, etc. |

#### E.1.3 Advertising Intervals

| Platform | Foreground | Background |
|----------|------------|------------|
| iOS | 20-100ms | 1000-2000ms (iOS controlled) |
| Android | 100-1000ms (app controlled) | varies by manufacturer |
| Embedded | 100-500ms recommended | N/A |

| Requirement | Level | Description |
|-------------|-------|-------------|
| Foreground Interval | **RECOMMENDED** | Use 100-200ms for reasonable discovery time when app is active. |
| Background Advertising | **RECOMMENDED** | Continue advertising in background if platform allows. iOS automatically reduces to ~1 second intervals. |

### E.2 GATT Service Structure

#### E.2.1 Service Definition

| Requirement | Level | Description |
|-------------|-------|-------------|
| Primary Service | **MANDATORY** | Implement as a primary service with UUID `10A50001-C4EA-4B47-AE30-A7D9577FC3F9`. |

#### E.2.2 Characteristic Requirements

| Characteristic | UUID | Properties | Requirement |
|----------------|------|------------|-------------|
| Input Report (Control) | `10A50006-...` | Read, Notify | **MANDATORY** |
| Input Report (Request Feedback) | `10A50008-...` | Read, Notify | **RECOMMENDED** |
| Input Report (Keepalive) | `10A50009-...` | Read, Notify | **MANDATORY** |
| Output Report (Feedback) | `10A50007-...` | Read, Write Without Response | **RECOMMENDED** |
| Output Report (Keepalive Response) | `10A5000A-...` | Read, Write Without Response | **MANDATORY** |
| Report Map | `10A50002-...` | Read | OPTIONAL |
| HID Information | `10A50003-...` | Read | OPTIONAL |
| HID Control Point | `10A50004-...` | Write Without Response | OPTIONAL |
| Protocol Mode | `10A50005-...` | Read, Write Without Response | OPTIONAL |

#### E.2.3 Input Report Characteristic (Control)

| Requirement | Level | Description |
|-------------|-------|-------------|
| Read Property | **MANDATORY** | Support reads so the Central can poll the current report value. |
| Notify Property | **MANDATORY** | Support notifications for sending Control reports. |
| CCCD | **MANDATORY** | Include Client Characteristic Configuration Descriptor (UUID `0x2902`) to allow Central to enable notifications. On iOS (CoreBluetooth), the CCCD is added automatically for `.notify` characteristics. |
| Report Size | **MANDATORY** | Send exactly 18 bytes per notification. |

#### E.2.4 Input Report Characteristic (Request Feedback)

If the Request Feedback Input Report characteristic is implemented (recommended), it MUST meet these requirements:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Read Property | **MANDATORY** | Support reads so the Central can poll the current report value. |
| Notify Property | **MANDATORY** | Support notifications for sending Request Feedback reports. |
| CCCD | **MANDATORY** | Include Client Characteristic Configuration Descriptor (UUID `0x2902`) to allow Central to enable notifications. On iOS (CoreBluetooth), the CCCD is added automatically for `.notify` characteristics. |
| Report Size | **MANDATORY** | Send exactly 1 byte per notification. |

#### E.2.5 Input Report Characteristic (Keepalive)

The Keepalive Input Report characteristic MUST meet these requirements:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Read Property | **MANDATORY** | Support reads so the Central can poll the current report value. |
| Notify Property | **MANDATORY** | Support notifications for sending Keepalive reports. |
| CCCD | **MANDATORY** | Include Client Characteristic Configuration Descriptor (UUID `0x2902`) to allow Central to enable notifications. On iOS (CoreBluetooth), the CCCD is added automatically for `.notify` characteristics. |
| Report Size | **MANDATORY** | Send exactly 1 byte per notification. |

#### E.2.6 Output Report Characteristic (Feedback)

If the Output Report characteristic is implemented (recommended), it MUST meet these requirements:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Read Property | **MANDATORY** | Support reads so the Central can poll the last feedback value. |
| Write Without Response | **MANDATORY** | Accept writes without response for lowest latency. |
| Report Size | **RECOMMENDED** | Validate incoming writes are exactly 19 bytes. |
| No Write With Response | **RECOMMENDED** | Do not require Write With Response; Centrals will use Write Without Response. |

#### E.2.7 Output Report Characteristic (Keepalive Response)

The Keepalive Response Output Report characteristic MUST meet these requirements:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Read Property | **MANDATORY** | Support reads so the Central can poll the last keepalive response value. |
| Write Without Response | **MANDATORY** | Accept writes without response for lowest latency. |
| Report Size | **MANDATORY** | Validate incoming writes are exactly 16 bytes (host UUID). |
| No Write With Response | **RECOMMENDED** | Do not require Write With Response; Centrals will use Write Without Response. |

### E.3 Data Transmission

#### E.3.1 Sending Control Reports

| Requirement | Level | Description |
|-------------|-------|-------------|
| Use Notifications | **MANDATORY** | Send Control reports as notifications on the Input Report characteristic. |
| Report Format | **MANDATORY** | Send exactly 18 bytes: 2 bytes (x, y) + 16 bytes (4 × uint32 bitfields). |
| Byte Order | **MANDATORY** | Use little-endian byte order for all packed multi-byte numeric fields in HID reports (e.g., the four `UInt32` bitfields in the Control report and the three `UInt32` bitfields in the Feedback report). This rule does not apply to opaque byte arrays such as the Host UUID in the Keepalive Response report, which has its own canonical byte order (see the Wheelchair Keepalive Response HID section and Appendix D.9). |
| Wait for CCCD Enable | **MANDATORY** | Do not send notifications until the Central has written `0x0001` to the CCCD. |

#### E.3.2 Sending Request Feedback Reports

| Requirement | Level | Description |
|-------------|-------|-------------|
| Use Notifications | **MANDATORY** | Send Request Feedback reports as notifications on the Request Feedback characteristic. |
| Report Format | **MANDATORY** | Send exactly 1 byte with value `0x01`. |
| Wait for CCCD Enable | **MANDATORY** | Do not send notifications until the Central has written `0x0001` to the CCCD. |

#### E.3.3 Sending Keepalive Reports

| Requirement | Level | Description |
|-------------|-------|-------------|
| Use Notifications | **MANDATORY** | Send Keepalive reports as notifications on the Keepalive characteristic. |
| Report Format | **MANDATORY** | Send exactly 1 byte with value `0x01`. |
| Wait for CCCD Enable | **MANDATORY** | Do not send notifications until the Central has written `0x0001` to the CCCD. |

#### E.3.4 Sending Release Reports

| Requirement | Level | Description |
|-------------|-------|-------------|
| Release Timing | **MANDATORY** | A minimum of 100ms must elapse after sending a Control report before sending a Release report. |

#### E.3.5 Receiving Feedback Reports

If the Output Report characteristic is implemented:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Accept Write Without Response | **MANDATORY** | Process incoming writes on the Output Report characteristic. |
| Report Format | **MANDATORY** | Expect exactly 19 bytes: 3 × uint32 bitfields + 7 × uint8 fields. |
| Byte Order | **MANDATORY** | Parse multi-byte fields as little-endian. |
| Stale Feedback Handling | **RECOMMENDED** | If the App or Device has been receiving Feedback reports and the reports stop arriving, it should treat the previously received feedback data as stale and should not rely on it for decision-making or display purposes. |

#### E.3.6 Receiving Keepalive Response Reports

The Keepalive Response Output Report characteristic is mandatory:

| Requirement | Level | Description |
|-------------|-------|-------------|
| Accept Write Without Response | **MANDATORY** | Process incoming writes on the Keepalive Response characteristic. |
| Report Format | **MANDATORY** | Expect exactly 16 bytes containing the host UUID. |
| Host Identification | **MANDATORY** | The Peripheral shall use the host UUID from the Keepalive Response report to identify the Wheelchair host WDI implementation. |
| Save Host ID (First Connection) | **MANDATORY** | On first-time connection to a Wheelchair host WDI implementation, after receiving the first Keepalive Response report, save the host ID for subsequent connection checks. |
| Verify Host ID (Subsequent Connections) | **MANDATORY** | On subsequent connections, after receiving the first Keepalive Response report, compare the received host ID against the saved host ID. If the host IDs match, proceed as normal. If they do not match, stop sending all reports (keepalive, control, and request feedback) to trigger a Wheelchair host WDI implementation disconnect. After this particular disconnect delay advertising for 15 seconds. |
| Clear Host ID Mechanism | **MANDATORY** | Provide a mechanism to clear a saved host ID. |
| Display Host ID | **RECOMMENDED** | Provide a way for a user to see the host ID. The full 16-byte host UUID shall be displayed (e.g., in standard string form); displaying only a partial form (such as a truncated UUID, hash, or the manufacturer name alone) is not sufficient. |
| Manufacturer ID Extraction | OPTIONAL | The Peripheral may parse bytes 0–1 of the host UUID as a big-endian 16-bit unsigned integer to obtain the manufacturer ID (see Appendix F). |
| Display Manufacturer | **RECOMMENDED** | If a manufacturer ID is recognized, the Peripheral may display the manufacturer name in addition to the host ID. The manufacturer name shall not be used as a substitute for displaying the host ID. Treat `0x0000` and unrecognized IDs as "unknown manufacturer" rather than as an error. |

### E.4 Keepalive Transmission

Keepalive is mandatory. It allows the Central to detect peripheral failures and stop the wheelchair.

| Requirement | Level | Description |
|-------------|-------|-------------|
| Keepalive Report | **MANDATORY** | Send Keepalive reports (Report ID 4) on the Keepalive characteristic to indicate the connection is active. |
| Transmission Rate | **MANDATORY** | The App or Device shall send a Keepalive report every ~233ms. Sending a control report or request feedback report resets the keepalive timer. If a control report or request feedback report has been sent since the last keepalive timer reset, no keepalive report is required until 233ms after the most recent sent report (keepalive, control, or request feedback). Control reports and request feedback reports are not constrained by the 233ms keepalive interval. Control reports may be sent at any rate, subject to release report timing requirements (see Sending Release Reports). Request feedback reports have their own recommended interval (see Request Feedback Timing). (Provides 24ms margin before 257ms Central timeout.) |
| Continuous Liveness | **MANDATORY** | The App or Device shall ensure the host receives at least one report (keepalive, control, or request feedback) every 233ms. If no control or request feedback report is being sent, send Keepalive reports to maintain the connection. |
| Expect Keepalive Response | **MANDATORY** | Upon sending a Keepalive report, expect to receive a Keepalive Response report (16-byte host UUID) from the Central. |

**Keepalive Timing Example (no control reports being sent):**
```
0ms    - Send Keepalive report (0x01)
        - Receive Keepalive Response (16-byte host UUID)
233ms  - Send Keepalive report (0x01)
        - Receive Keepalive Response (16-byte host UUID)
466ms  - Send Keepalive report (0x01)
        - Receive Keepalive Response (16-byte host UUID)
...
```

**Keepalive Timing Example (control reports resetting the timer):**
```
0ms    - Send Keepalive report (0x01)
        - Receive Keepalive Response (16-byte host UUID)
100ms  - Send Control report (resets keepalive timer)
300ms  - Send Control report (resets keepalive timer)
500ms  - Send Control report (resets keepalive timer)
...    - No Keepalive needed while Control reports are sent less than 233ms apart
733ms  - No Control report sent for 233ms, send Keepalive report (0x01)
        - Receive Keepalive Response (16-byte host UUID)
```

### E.5 Connection Parameters

#### E.5.1 Parameter Requests

| Requirement | Level | Description |
|-------------|-------|-------------|
| Request Appropriate Interval | **RECOMMENDED** | Request connection interval of 15-30ms for responsive HID control. |
| Accept Central's Decision | **MANDATORY** | The Central may accept or reject parameter requests. Continue operation regardless. |

#### E.5.2 Recommended Parameters

| Parameter | Recommended Value | Rationale |
|-----------|-------------------|-----------|
| Connection Interval | 15-30ms | Low latency for joystick responsiveness |
| Slave Latency | 0 | No skipped events for real-time control |
| Supervision Timeout | 2000-4000ms | Tolerates brief interference |

#### E.5.3 iOS-Specific Considerations

iOS enforces strict connection parameter requirements. Requests outside these bounds will be rejected:

| Parameter | iOS Requirement |
|-----------|-----------------|
| Interval Min | ≥15ms (12 × 1.25ms) |
| Interval Max | ≥Interval Min; for low-latency HID, use ≤30ms |
| Slave Latency | ≤30 |
| Supervision Timeout | 2-6 seconds |
| Timeout Constraint | Supervision Timeout > Interval Max × (Slave Latency + 1) × 2 |

**Recommended iOS-compatible parameters:**
- Interval Min: 15ms
- Interval Max: 30ms  
- Slave Latency: 0
- Supervision Timeout: 4 seconds

### E.6 Pairing and Security

| Requirement | Level | Description |
|-------------|-------|-------------|
| No Pairing Required | **MANDATORY** | The Peripheral SHALL NOT require pairing or bonding to function other than Just Works BLE pairing. |
| Support Just Works Pairing | **MANDATORY** | The Peripheral SHALL support Just Works BLE pairing. |
| May Request Pairing | OPTIONAL | The Peripheral MAY request other forms of pairing, but SHALL function with Just Works BLE pairing. |
| No Encryption Required | **MANDATORY** | The Peripheral SHALL NOT require encryption on the Input or Output Report characteristics. |

### E.7 Disconnect Handling

| Requirement | Level | Description |
|-------------|-------|-------------|
| Resume Advertising | **MANDATORY** | Upon disconnect, resume advertising to allow reconnection. |
| Host ID Mismatch Advertising Delay | **MANDATORY** | After a disconnect triggered by a host ID mismatch, delay advertising for 15 seconds before resuming. |
| Clear CCCD State | **RECOMMENDED** | Reset notification enable state on disconnect; wait for Central to re-enable after reconnection. |
| Persist User State | **RECOMMENDED** | Maintain application state (e.g., joystick calibration) across disconnects if appropriate. |

### E.8 Error Handling

| Scenario | Required Action |
|----------|-----------------|
| CCCD not enabled | Do not send notifications; wait for Central to enable |
| Write received with wrong size | Discard, optionally log warning |
| Connection lost | Resume advertising |
| Notification send fails | Log warning, retry on next report cycle |
| Central disconnects during operation | Resume advertising immediately |

### E.9 Summary of Mandatory Requirements (Peripheral)

A compliant Wheelchair HID BLE Peripheral implementation MUST:

1. Advertise the Wheelchair HID Service UUID (in advertising packet or scan response)
2. Use connectable undirected advertising
3. Implement the Input Report characteristic with Notify property and CCCD
4. Send Control reports as exactly 18 bytes in little-endian format
5. Send Request Feedback reports as exactly 1 byte (if implemented)
6. Send Keepalive reports as exactly 1 byte
7. Wait for CCCD enable before sending notifications
8. Not require pairing, bonding, or encryption other than Just Works BLE pairing
9. Accept Write Without Response on Output Report characteristic (if implemented)
10. Resume advertising upon disconnect
11. A minimum of 100ms must elapse after sending a Control report before sending a Release report
12. Implement Keepalive Input Report characteristic
13. Send a Keepalive report every ~233ms; sending a control or request feedback report resets the keepalive timer (control reports and request feedback reports are not constrained by the 233ms keepalive interval; control reports may be sent at any rate subject to release report timing requirements and request feedback reports have their own recommended interval)
14. Implement Keepalive Response Output Report characteristic
15. Accept Keepalive Response reports (16-byte host UUID) from the Central
16. Use the host UUID from the Keepalive Response to identify the Wheelchair host WDI implementation
17. On first-time connection, save the host ID after receiving the first Keepalive Response report
18. On subsequent connections, compare received host ID against saved host ID; if mismatch, stop sending all reports to trigger disconnect
19. After a host ID mismatch disconnect, delay advertising for 15 seconds
20. Provide a mechanism to clear a saved host ID

A compliant implementation SHOULD:

21. Implement Output Report characteristic to receive feedback
22. Implement Request Feedback Input Report characteristic to request feedback from the Central
23. Provide a way for a user to see the host ID; the full 16-byte host UUID shall be displayed (the manufacturer name alone is not sufficient)
24. If feedback reports have been received and stop arriving, treat previously received feedback data as stale
25. If a recognized manufacturer ID is present in bytes 0–1 of the host UUID, display the manufacturer name in addition to the host ID (the manufacturer name shall not be used in place of the host ID) (see Appendix F)

---

## Appendix F: Manufacturer IDs

### Description

The first two bytes of the host UUID (bytes 0–1 of the Keepalive Response report payload) encode a 16-bit manufacturer ID in big-endian order. This identifies the wheelchair manufacturer that produced the Wheelchair host WDI implementation. Apps and Devices may extract this value to display the manufacturer name, filter known hosts, or apply manufacturer-specific behavior.

The remaining 14 bytes of the host UUID provide cryptographic uniqueness across hosts from the same manufacturer, while preserving the RFC 4122 version 4 and variant markers (see Host UUID Requirements in the Wheelchair Keepalive Response HID section).

### Format

| Field | Size | Position | Encoding |
|-------|------|----------|----------|
| Manufacturer ID | 2 bytes (16 bits) | Bytes 0–1 of host UUID | Big-endian unsigned integer |

In standard UUID string form (`xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`), the manufacturer ID appears as the first four hex digits. For example, a host UUID of `1234ABCD-EF01-4567-89AB-CDEF01234567` encodes manufacturer ID `0x1234`.

### Reserved Values

| ID / Range | Purpose |
|------------|---------|
| `0x0000` | Unknown / unassigned manufacturer |
| `0x0001` – `0x000A` | Reserved for testers and development use |
| `0x10A5` | Reserved (matches the first two bytes of the Wheelchair HID Service UUID base `10A50001-C4EA-4B47-AE30-A7D9577FC3F9`; reserved to avoid visual confusion between host UUIDs and service UUIDs) |

Manufacturers shall not be assigned any reserved value.

### Assigned Manufacturer IDs

| ID | Manufacturer |
|----|--------------|
| `0x000B` | LUCI Mobility, Inc. |
| `0x000C` | LifeDrive Mobility, LLC |

### Registry

This appendix maintains the authoritative registry of Wheelchair HID manufacturer IDs. The registry is intentionally separate from existing 16-bit registries (such as Bluetooth SIG Company Identifiers and USB-IF Vendor IDs) because Wheelchair HID hosts may support Bluetooth LE, USB, or both, and a transport-specific registry would not cover all implementations.

Requests for assignment of a manufacturer ID may be submitted to the maintainers of this specification. At most one manufacturer ID shall be assigned per manufacturer. Assigned IDs shall be stable for the lifetime of the manufacturer.

### App and Device Behavior

| Requirement | Level | Description |
|-------------|-------|-------------|
| Parse Manufacturer ID | OPTIONAL | Apps and Devices may parse bytes 0–1 of the host UUID as a big-endian 16-bit unsigned integer to obtain the manufacturer ID. |
| Display Manufacturer | **RECOMMENDED** | When a recognized manufacturer ID is present, Apps and Devices should display the manufacturer name in addition to the host ID. The manufacturer name shall not be used as a substitute for displaying the host ID. |
| Handle Unknown IDs | **MANDATORY** | Apps and Devices shall treat `0x0000` and any unrecognized manufacturer ID as "unknown manufacturer" rather than as an error. The registry may grow over time, so unrecognized IDs are expected. |
| Do Not Use For Identity | **MANDATORY** | Apps and Devices shall continue to use the full 16-byte host UUID, not the manufacturer ID alone, for host identity (save / compare per the Keepalive section). |

### Wheelchair Host WDI Implementation Behavior

| Requirement | Level | Description |
|-------------|-------|-------------|
| Use Assigned ID | **MANDATORY** | A Wheelchair host WDI implementation from a manufacturer that has been assigned a manufacturer ID shall use that ID in bytes 0–1 of its host UUID. |
| Use 0x0000 If Unassigned | **MANDATORY** | A Wheelchair host WDI implementation from a manufacturer that has not been assigned a manufacturer ID shall use `0x0000` in bytes 0–1 of its host UUID. |
| Stable ID | **MANDATORY** | The manufacturer ID shall remain constant for the lifetime of the Wheelchair host WDI implementation (consistent with the Host UUID being constant for the lifetime of the implementation). |

---

## Version History
- 3.2 The first two bytes of the host UUID in the Keepalive Response report now encode a 16-bit manufacturer ID (big-endian). The remaining 14 bytes continue to provide cryptographic uniqueness. Clarified that the host UUID is transmitted in big-endian / network byte order. The Host UUID remains a valid RFC 4122 version 4 UUID. Apps and Devices may extract the manufacturer ID to identify the wheelchair manufacturer. Added Appendix F: Manufacturer IDs, with reserved values (`0x0000` unknown, `0x0001`–`0x000A` testers, `0x10A5` reserved due to conflict with the service UUID base), an assignment registry, and initial assignments (`0x000B` LUCI Mobility, Inc.; `0x000C` LifeDrive Mobility, LLC). Clarified throughout that the manufacturer name shall not be used as a substitute for displaying the host ID — Apps and Devices should display the full 16-byte host UUID, and may display the manufacturer name in addition. Updated Keepalive section, Wheelchair Keepalive Response HID section, and Appendices D and E. Scoped the "little-endian for multi-byte fields" rule in E.3.1 to packed numeric fields, and revised Appendix D.9 to distinguish BLE framing UUIDs (little-endian) from application-payload UUIDs (big-endian / canonical RFC 4122). Extracted LUCI vendor-specific bit assignments (Control `WDI Vendor Specific1` bits 1–2 and Feedback `WDI Vendor Specific1` bits 0–3) into a separate vendor document (`luci.md`); the corresponding bit positions in the main spec are now Reserved for future use. Added a `### WDI Vendor Specific Bit Interpretation` subsection to both the Wheelchair Control HID and Wheelchair Feedback HID sections, clarifying that Vendor Specific bits form a per-manufacturer namespace — every manufacturer has full independent access, including pairing the Modifier bit (in Control) with their own bit assignments per the `0+X` convention used in Standard1, with the manufacturer defining what those pairings mean — and that the 16-bit manufacturer ID in the Host UUID identifies which manufacturer's vendor document applies.
- 3.1 Revised recommended Request Feedback Report interval to greater than 0.750 seconds.
- 3.0 Control reports and request feedback reports now reset the host's 257ms keepalive timeout timer, in addition to keepalive reports. On the app/device side, sending a control report or request feedback report resets the 233ms keepalive transmission timer, reducing unnecessary keepalive transmissions during active control. Changed disconnect threshold from 2 consecutive missed keepalives to 3 consecutive report timeouts. On host ID mismatch, the app or device shall now stop sending all reports (keepalive, control, and request feedback), not just keepalive reports. Added recommendation that apps and devices should treat feedback data as stale if feedback reports stop arriving. Updated Keepalive section, Wheelchair Feedback HID section, and Appendices D and E.
- 2.9 Added Profile Up (bit 11) and Profile Down (bit 15) to Control report Standard1.
- 2.8 Added Bluetooth LE host ID handling requirements for apps and devices. For first-time connections, apps/devices shall save the host ID after receiving the first Keepalive Response. For subsequent connections, apps/devices shall compare the received host ID against the saved host ID; if mismatch, stop sending Keepalives to trigger disconnect, then delay advertising for 15 seconds. Apps/devices shall provide a mechanism to clear a saved host ID and should provide a way for users to see some form of the host ID. Added Just Works BLE pairing requirement. Updated Appendices C, D and E.
- 2.7 Changed host Keepalive check interval from 260ms to 257ms (24ms margin from 233ms transmission rate). Added Wheelchair Keepalive Response HID report (Report ID 5). The host shall send a Keepalive Response containing a cryptographically unique 16-byte host UUID in response to receiving a Keepalive report. The App or Device shall use the Keepalive Response to identify the Wheelchair host WDI implementation. Added UUID 10A5000A for Keepalive Response Output Report characteristic. Updated Appendices D and E with Keepalive Response requirements.
- 2.6 Clarified that Apps and Devices must begin sending Keepalive reports after a stable connection is established. Clarified that for both Bluetooth LE and USB connections, disconnects shall be treated as a Release Report and Disable Drive. Clarified that for Bluetooth LE missed Keepalives, the behavior is also Release Report and Disable Drive (consistent with USB). Updated Central implementation language in Appendix D to clarify internal processing of Release Report and Drive Disable on disconnect.
- 2.5 Changed Keepalive from optional to mandatory. Apps and Devices shall send Keepalive reports every ~233ms; host timeout changed to 260ms (provides 27ms margin). Added recommended 1.17s interval for periodic Request Feedback reports. Timing values chosen to avoid transmission collisions. Centrals and Peripherals shall implement the Keepalive characteristic. Updated requirements in Appendices D and E accordingly.
- 2.4 Combined Profile and Speed UInt8 fields into single Speed/Profile packed byte (high nibble = speed, low nibble = profile; 0 = unknown, 1–15 = valid). Defined Velocity byte encoding (high nibble = whole mph, low nibble = tenths of mph; 0–9 valid, 0xA–0xF reserved; range 0.0–15.9 mph). Reordered fields: Speed/Profile, Velocity, Odometer. Added one additional reserved byte. Report size unchanged at 19 bytes.
- 2.3 Extended Keepalive support to USB connections. If Keepalives are used over USB and two consecutive keepalives are missed, the host shall treat this as a Release Report and Disable Drive.
- 2.2 Revised Wheelchair Feedback HID Descriptor format. Changed from 4×UInt32 (16 bytes) to 3×UInt32 + 7×UInt8 (19 bytes): WDI Standard, WDI Vendor Specific1, WDI Vendor Specific2, Profile, Speed, Odometer, Velocity, and 3 reserved bytes. Consolidated WDI Standard1 and Standard2 into single WDI Standard. Removed Profile and Speed bit flags (now UInt8 fields). Added Standard bits 12-14: No Movement Restriction, Limited Speed, No Movement.
- 2.1 Added Wheelchair Keepalive HID report (Report ID 4). Moved Keepalive from Control Standard1 bit 11 to its own report. Control Standard1 bit 11 is now reserved for future use.
- 2.0 Feedback reports shall always be full reports. Unknown or unavailable bits shall be set to 0.
- 1.9 Added Wheelchair Request Feedback HID report (Report ID 3). Moved Request Feedback from Control Standard1 bit 15 to its own report. Control Standard1 bit 15 is now reserved for future use.
- 1.8 Added Release Report requirement to Appendix E.
- 1.7 Updated Disconnect section. Added Appendix C, D and E.
- 1.6 Fixed typo.
- 1.5 Added Bluetooth LE UUID Appendix B.
- 1.4 Removed modifiers from Feedback bit flags and revised entries that used them.
- 1.3 added LUCI temporary mapping.
- 1.2 initial attempt at a Wheelchair HID Descriptor.
- 1.1 removed vendor id. Vendor specific will be assigned unique bits and modifier can also be used. Revised the Wheelchair Feedback Frequency section.
- 1.0 initial version.
