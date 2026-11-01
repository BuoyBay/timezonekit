---
title: "Windows timezone mappings"
summary: "Map exact Windows identifiers and CLDR territories to IANA names."
category: "Reference"
order: 25
keywords: ["timezone", "Windows", "CLDR", "territory", "IANA"]
symbols: ["WindowsZoneMappingVersion", "WindowsTimeZoneIDs", "WindowsTimeZoneTerritories", "WindowsToIANAZones", "WindowsToIANA", "NamedTimeZoneFromWindows"]
related: ["index.md", "api.md"]
---

# Windows timezone mappings

Import timezonekit. Its mapping APIs work
on macOS, Windows and Linux using pinned CLDR 49 data rather than OS registry
lookups. English Windows key identifiers and territory codes are matched exactly,
case sensitively, with no whitespace trimming.

| Function | Contract |
| --- | --- |
| WindowsZoneMappingVersion() | String `49` |
| WindowsTimeZoneIDs() | Fresh sorted Array Of String containing all 142 identifiers |
| WindowsTimeZoneTerritories(windowsID As String) | Fresh sorted list of available CLDR territory codes |
| WindowsToIANAZones(windowsID As String, territory As String = "001") | Fresh array of every IANA alternative in CLDR order |
| WindowsToIANA(windowsID As String, territory As String = "001") | First CLDR-preferred IANA identifier |
| NamedTimeZoneFromWindows(windowsID As String, territory As String = "001") | NamedTimeZone constructed from the preferred identifier |

001 is the global CLDR default. ZZ is CLDR's unknown-territory entry where one
exists. Neither is an implicit fallback for a missing requested territory. Unknown
Windows IDs or unavailable territories throw InvalidArgumentException. Returned
arrays may be changed without affecting later queries.

Mountain Standard Time defaults to America/Denver; its US list contains
America/Denver and America/Boise. WindowsToIANA chooses the first intentionally;
use WindowsToIANAZones when every alternative matters. No location inference or
reverse mapping is supplied. Localized display labels are not identifiers.

All 505 source rows are preserved, including IANA aliases. Every one of the 445
distinct target names is supported by the separate IANA 2026f transition tables.
CLDR mapping updates and IANA rule updates are independent. NamedTimeZone's
1800–2500 UTC range and gap/overlap rules still apply to constructed zones.

[Overview](index.md) · [Named-zone API](api.md)
