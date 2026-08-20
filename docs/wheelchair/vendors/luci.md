# Wheelchair HID — LUCI Vendor Extensions

## Version
- Version 0.1
- May 20, 2026

## Scope

**LUCI does not currently have a wheelchair HID implementation, all information in this document should be considered pre-release**

This document defines LUCI's bit assignments within the `WDI Vendor Specific1` fields of the Wheelchair HID specification. It is a vendor-specific extension to the [Wheelchair HID specification ](../wheelchair-hid.md).

A Wheelchair host WDI implementation produced by LUCI Mobility, Inc. identifies itself via the assigned manufacturer ID `0x000B` at bytes 0–1 of the Host UUID in the Keepalive Response report (see Wheelchair HID Appendix F: Manufacturer IDs for the authoritative registry).

The `WDI Vendor Specific1` and `WDI Vendor Specific2` fields form a per-manufacturer namespace. Bit 0 of Control's Vendor Specific fields is the Modifier bit; the Modifier convention itself is shared at the spec level, but LUCI — like any manufacturer — may pair the Modifier with its own bit assignments to define alternate functions, following the `0+X` notation used in Standard1, and LUCI defines what those pairings mean. All other Vendor Specific bits (including all 32 bits of Feedback's Vendor Specific fields) are LUCI's to define here. Bits not listed below are unused by LUCI today. Other manufacturers have the same full independent access to their own per-manufacturer namespace and may use the same bit numbers (and Modifier pairings) for entirely different functions; the manufacturer ID at bytes 0–1 of the Host UUID disambiguates which manufacturer's vendor document an App or Device should apply.

## Control Report — WDI Vendor Specific1 Bits

LUCI uses the following bits in the Control report's `WDI Vendor Specific1` `UInt32` field (sent from App or Device to the Wheelchair host).

| Bit | Function Name |
|-----|---------------|
| 1 | LUCI Override |
| 2 | Future LUCI feature |

## Feedback Report — WDI Vendor Specific1 Bits

LUCI uses the following bits in the Feedback report's `WDI Vendor Specific1` `UInt32` field (sent from the Wheelchair host to the App or Device).

| Bit | Function Name |
|-----|---------------|
| 0 | LUCI Override is off |
| 1 | LUCI Override is on |
| 2 | Future LUCI feature is off |
| 3 | Future LUCI feature is on |

## Version History
- 0.1 Initial version. Extracted LUCI bit assignments from the [Wheelchair HID specification ](../wheelchair-hid.md) (formerly listed in the `WDI Vendor Specific1` tables of the Wheelchair Control HID and Wheelchair Feedback HID descriptors in Wheelchair HID 3.1 and earlier).
