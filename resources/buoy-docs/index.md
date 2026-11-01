---
title: "TimeZoneKit"
summary: "IANA named timezones with explicit gap and overlap resolution."
category: "Overview"
order: 0
keywords: ["timezone", "IANA", "DST", "calendar"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# TimeZoneKit

Import timezonekit for 597 names and aliases from bundled IANA 2026f data.
Lookup uses 64-bit transitions and does not consult the OS timezone database.
UTC years 1800 through 2500 are supported.

NamedTimeZone.At presents an instant in a zone. ResolveLocal converts local
calendar components to an instant: gaps throw, and overlaps require an explicit
earlier/later choice unless default rejection is desired. Future rules are
predictions from the pinned release and need updating when laws change.

These package types do not modify built-in TimeZone factories. See the
[API reference](api.md).

The same `timezonekit` import maps 142 Windows timezone key
identifiers through pinned CLDR 49 data. Territory selection is explicit, multiple
IANA alternatives are preserved, and unavailable mappings throw rather than guess.
See [Windows mappings](windows-mappings.md).
