# Resolve IANA timezones and daylight-saving transitions

Named IANA timezones for Buoy with bundled **2026f** data and 64-bit transition
lookups. Copy `packages/timezonekit-0.1.0.buipkg` into a consumer's packages
directory, then `Import timezonekit`. No native package or OS timezone database
is required at runtime.

ZonedDateTime exposes read-only `Instant` (UTC DateTime), `ZoneName`,
`OffsetSeconds`, `Abbreviation`, `IsDST`, `Year`, `Month`, `Day`, `Hour`, `Minute`,
`Second`, `Millisecond` and `ToISO8601()`. Presentation preserves the instant.
Historical second-level offsets are retained and included in ISO output when needed.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add timezonekit --git https://github.com/BuoyBay/timezonekit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API entrypoints

- `Import timezonekit`
- `TimeZoneDataVersion()`
- `NamedTimeZones()`
- `New NamedTimeZone(name)`
- `zone.At(instant)`

## Platform and scope

Uses pinned IANA data and makes ambiguous or nonexistent local times explicit. Check the documented supported date range.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer timezonekit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

The generated agent files and editor settings stay local and are ignored by Git.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
