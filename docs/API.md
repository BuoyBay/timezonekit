# TimeZoneKit 0.1.0

Named IANA timezones for Buoy with bundled **2026f** data and 64-bit transition
lookups. Copy `packages/timezonekit-0.1.0.buipkg` into a consumer's packages
directory, then `Import timezonekit`. No native package or OS timezone database
is required at runtime.

| API | Contract |
| --- | --- |
| `TimeZoneDataVersion()` | Returns `2026f` |
| `NamedTimeZones()` | Fresh sorted array of all 597 accepted names and aliases |
| `New NamedTimeZone(name)` | Exact, case-sensitive IANA identifier; unknown names throw |
| `zone.Name` | Requested identifier, retaining aliases |
| `zone.At(instant)` | Read-only ZonedDateTime presentation of a Buoy DateTime instant |
| `zone.ResolveLocal(year, month, day, hour = 0, minute = 0, second = 0, millisecond = 0, ambiguity = "reject")` | Convert local components to an instant; reject gaps and resolve overlaps explicitly |

ZonedDateTime exposes read-only `Instant` (UTC DateTime), `ZoneName`,
`OffsetSeconds`, `Abbreviation`, `IsDST`, `Year`, `Month`, `Day`, `Hour`, `Minute`,
`Second`, `Millisecond` and `ToISO8601()`. Presentation preserves the instant.
Historical second-level offsets are retained and included in ISO output when needed.

## Range and daylight saving

The supported **UTC interval is 1800-01-01 inclusive through 2501-01-01 exclusive**.
Out-of-range/Nil instants and unknown zone names throw InvalidArgumentException.
Transition times use signed 64-bit seconds, including dates beyond 2038. Future
transitions are predictions from the pinned data release and need updating when
governments change their rules.

ResolveLocal rejects nonexistent wall times during a forward clock change.
During backward changes, the default `ambiguity: "reject"` throws; explicit
`"earlier"`/`"later"` choose the earliest/latest matching UTC instant. This handles
changes of arbitrary size, including non-hour transitions. Gaps always throw.
Calendar fields, ISO formatting and local-time validation use portable Gregorian
arithmetic, including pre-1970 dates where Windows' native DateTime presentation
can fail. Instant retains its exact numeric DateTime value; use ZonedDateTime's
calendar properties for zone presentation. At range edges, a resolution
succeeds only if its UTC instant is inside the supported interval.

This package owns NamedTimeZone/ZonedDateTime types; built-in TimeZone factories
are unchanged. Windows registry identifiers can be mapped through the package APIs
described below. Host-zone discovery, localized display names
and leap-second arithmetic are not supplied. Instants
use POSIX/Unix time, consistent with Buoy DateTime.

## Windows identifiers and territories

`Import timezonekit` also exposes pinned **CLDR 49** Windows-to-IANA mappings.
The mapping APIs work on every target;
it does not query the Windows registry or guess the host's location. It accepts
Windows key identifiers such as `Mountain Standard Time`, not localized display
names. Identifiers and territory codes are exact and case sensitive; surrounding
whitespace is not trimmed.

| API | Contract |
| --- | --- |
| `WindowsZoneMappingVersion()` | Returns `49` |
| `WindowsTimeZoneIDs()` | Fresh sorted array of all 142 Windows identifiers |
| `WindowsTimeZoneTerritories(windowsID)` | Fresh sorted array of available CLDR territory codes for that ID |
| `WindowsToIANAZones(windowsID, territory = "001")` | Every mapped IANA identifier in CLDR preference order |
| `WindowsToIANA(windowsID, territory = "001")` | First CLDR-preferred identifier for that exact ID/territory |
| `NamedTimeZoneFromWindows(windowsID, territory = "001")` | Construct the preferred mapped NamedTimeZone |

`001` is CLDR's global default. Specify an available territory such as `US` when
regional mapping matters. `ZZ`, when present for an ID, is CLDR's unknown-territory
entry; it is not an automatic fallback. Unknown IDs and unavailable territories
throw InvalidArgumentException rather than silently falling back to `001`.

For example, Mountain Standard Time defaults to America/Denver. Its US mapping
contains America/Denver followed by America/Boise. WindowsToIANA deliberately
returns the first; use WindowsToIANAZones to retain all alternatives. Mapping is
one-way and does not infer a user's actual location. Historical IANA aliases are
preserved verbatim rather than renamed. All 445 distinct targets in the 505 CLDR
rows are supported by the package's pinned IANA data.

The CLDR 49 XML and license are checked in under data/cldr-49, pinned to commit
96e54b273d2da4ec6fbad350ba19ff23fa24a588 with SHA-256 hashes. Updating this mapping
does not update the separate IANA transition database. Its XML typeVersion field
is source metadata, not the version of TimeZoneKit's runtime rules.

## Reproduction and verification

The IANA source archive, URL and SHA-256 are under data/. The generator compiles
standard geographic sources plus backward aliases using `zic -b fat`, a bounded
range and explicit future transitions. Optional backzone history and leap-second
zones are excluded. Identical transition tables are shared across aliases.
data/generated.json records the zic version, counts, range and table hash.

```sh
/usr/bin/buoy pkg seal . -o packages/timezonekit-0.1.0.buipkg
```

Regeneration requires `zic`. Preserve transition boundaries, gap/overlap policies, historical offsets and retained instants when updating the pinned tables. `BUOY` and `BPM_PACKAGER` select the toolchain commands.

Independent implementation; no declaresub code is copied. The
[public-domain IANA notice](../resources/IANA-LICENSE.txt) is bundled in the archive.
