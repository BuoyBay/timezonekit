---
title: "TimeZoneKit API"
summary: "Zone construction, instant presentation and local-time resolution."
category: "Reference"
order: 20
keywords: ["timezone", "offset", "ambiguity"]
symbols: ["TimeZoneDataVersion", "NamedTimeZones", "NamedTimeZone", "NamedTimeZone.At", "NamedTimeZone.ResolveLocal", "ZonedDateTime", "ZonedDateTime.ToISO8601"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

| Symbol | Behavior |
| --- | --- |
| TimeZoneDataVersion() | Returns 2026f |
| NamedTimeZones() | Fresh sorted array of exact names and aliases |
| NamedTimeZone(name) | Case-sensitive identifier; reject unknown names |
| At(instant As DateTime) | Immutable presentation; reject Nil or out-of-range instants |
| ResolveLocal(year, month, day, hour = 0, minute = 0, second = 0, millisecond = 0, ambiguity = "reject") | Gaps always throw; overlaps use reject/earlier/later |

ZonedDateTime has read-only Instant, ZoneName, OffsetSeconds, Abbreviation, IsDST,
Year, Month, Day, Hour, Minute, Second and Millisecond. Instant retains the UTC
instant; ToISO8601() renders local fields and numeric offset, including historical
offset seconds when nonzero.

Supported UTC interval: [-5364662400000, 16756761600000) Unix milliseconds.
Invalid inputs, gaps and rejected overlaps throw InvalidArgumentException.
Calendar validation, presentation and ISO output use portable Gregorian arithmetic,
including historical/pre-epoch dates on Windows. The same package supplies
[Windows-name mappings](windows-mappings.md). Localized names, host-zone detection
and leap seconds are not supplied.

[Overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
