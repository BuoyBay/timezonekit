---
title: "timezonekit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["NamedTimeZone", "ZonedDateTime"]
dependencies: []
symbols: ["NamedTimeZone", "ZonedDateTime"]
related: ["api.md", "getting-started.md", "index.md"]
---

# timezonekit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## TimeZoneKit functions

### TimeZoneDataVersion

`Public Function TimeZoneDataVersion() As String`

Pinned IANA timezone data version, independent of the OS database.

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### NamedTimeZones

`Public Function NamedTimeZones() As Array Of String`

Return an owned list of accepted IANA names and aliases in ordinal order.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### WindowsZoneMappingVersion

`Public Function WindowsZoneMappingVersion() As String`

Version of the pinned CLDR Windows-to-IANA mapping data.

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### WindowsTimeZoneIDs

`Public Function WindowsTimeZoneIDs() As Array Of String`

Fresh ordinally sorted array of exact Windows timezone identifiers.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### WindowsTimeZoneTerritories

`Public Function WindowsTimeZoneTerritories(windowsID As String) As Array Of String`

Available exact CLDR territory codes; 001 is the global default and ZZ is unknown territory.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `windowsID` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of String` |

### WindowsToIANAZones

`Public Function WindowsToIANAZones(windowsID As String, territory As String = "001") As Array Of String`

All IANA identifiers in CLDR preference order; no fallback for an unmapped territory.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `windowsID` | `String` | `ByVal` | Required |
| `territory` | `String` | `ByVal` | `"001"` |

#### Returns

| Type |
| --- |
| `Array Of String` |

### WindowsToIANA

`Public Function WindowsToIANA(windowsID As String, territory As String = "001") As String`

The first CLDR-preferred IANA identifier for the exact Windows ID and territory.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `windowsID` | `String` | `ByVal` | Required |
| `territory` | `String` | `ByVal` | `"001"` |

#### Returns

| Type |
| --- |
| `String` |

### NamedTimeZoneFromWindows

`Public Function NamedTimeZoneFromWindows(windowsID As String, territory As String = "001") As NamedTimeZone`

Construct the first CLDR-preferred named zone, retaining the mapped IANA identifier.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `windowsID` | `String` | `ByVal` | Required |
| `territory` | `String` | `ByVal` | `"001"` |

#### Returns

| Type |
| --- |
| `NamedTimeZone` |

## ZonedDateTime

`Public Class ZonedDateTime`

An instant and its portable named-zone presentation. All properties are read-only.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Instant` | `DateTime` | Yes | No | — | — |
| `ZoneName` | `String` | Yes | No | — | — |
| `OffsetSeconds` | `Integer` | Yes | No | — | — |
| `Abbreviation` | `String` | Yes | No | — | — |
| `IsDST` | `Boolean` | Yes | No | — | — |
| `Year` | `Integer` | Yes | No | — | — |
| `Month` | `Integer` | Yes | No | — | — |
| `Day` | `Integer` | Yes | No | — | — |
| `Hour` | `Integer` | Yes | No | — | — |
| `Minute` | `Integer` | Yes | No | — | — |
| `Second` | `Integer` | Yes | No | — | — |
| `Millisecond` | `Integer` | Yes | No | — | — |

### ToISO8601

`Public Function ToISO8601() As String`

No parameters.

#### Returns

| Type |
| --- |
| `String` |

## NamedTimeZone

`Public Class NamedTimeZone`

Named-zone lookups for instants in UTC years 1800 through 2500.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(name As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

Returns: no value.

### At

`Public Function At(instant As DateTime) As ZonedDateTime`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `instant` | `DateTime` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ZonedDateTime` |

### ResolveLocal

`Public Function ResolveLocal(year As Integer, month As Integer, day As Integer, hour As Integer = 0, minute As Integer = 0, second As Integer = 0, millisecond As Integer = 0, ambiguity As String = "reject") As ZonedDateTime`

Resolve a wall-clock time; reject gaps, and choose reject/earlier/later for overlaps.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `year` | `Integer` | `ByVal` | Required |
| `month` | `Integer` | `ByVal` | Required |
| `day` | `Integer` | `ByVal` | Required |
| `hour` | `Integer` | `ByVal` | `0` |
| `minute` | `Integer` | `ByVal` | `0` |
| `second` | `Integer` | `ByVal` | `0` |
| `millisecond` | `Integer` | `ByVal` | `0` |
| `ambiguity` | `String` | `ByVal` | `"reject"` |

#### Returns

| Type |
| --- |
| `ZonedDateTime` |
