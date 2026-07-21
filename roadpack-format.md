---
title: Road pack format
---

# DryLine road pack format — v1

This is the specification for the `.dlrp` speed-limit packs published in
the [roadpacks-latest release](https://github.com/PQfoodoo/dryline-docs/releases/tag/roadpacks-latest)
of this repository. It is published so the packs — a derivative database
of OpenStreetMap — are usable by anyone without reverse engineering.

Status: **FROZEN 2026-07-20**. Frozen means v1's layout and field
meanings no longer change. A hosted pack can only be superseded by a new
`formatVersion`, and readers reject versions they do not know rather than
guessing — so an older app meets a newer pack with an honest error
instead of misreported limits. Growth goes into the space already
reserved here: way ids and endpoint node ids, header flag bits, and
appended `RoadClass` values, which older builds read as `OTHER`.

A pack answers one question fast, on a phone, offline: *what are the
speed limits along this corridor?* Everything here serves that and
nothing else — it is deliberately not a routing graph (DryLine does not
route).

## Data source and licence

Packs contain data extracted from **OpenStreetMap** (way geometry,
`highway` class, numeric `maxspeed`), obtained via
[Geofabrik](https://download.geofabrik.de/) country extracts.

- Data **© OpenStreetMap contributors**, licensed under the
  [Open Database License 1.0 (ODbL)](https://opendatacommons.org/licenses/odbl/1-0/)
  — see [osm.org/copyright](https://www.openstreetmap.org/copyright).
- A `.dlrp` pack is a *derivative database* of OSM and is itself offered
  under the **ODbL**. You may copy, redistribute and adapt it under the
  same terms.
- Packs carry no personal data: only road geometry and speed limits.

## Conventions

- All fixed-width integers are **little-endian**.
- `uvarint` is unsigned LEB128. `svarint` is the same with zigzag
  encoding (`(n << 1) xor (n >> 63)`).
- Coordinates are **1e-5 degrees** (~1.1 m at the equator, better with
  latitude) stored as `int32`.
- Offsets are byte offsets from the start of the file.
- Packs are served and stored **uncompressed**; varint-delta geometry is
  already dense enough that gzip saved only ~25 % on the first real
  packs, not worth the extra step.

## Layout

    ┌────────────────┐
    │ header (32 B)  │
    ├────────────────┤
    │ way records    │  variable, packed back to back
    ├────────────────┤
    │ way-ref table  │  u32 offsets, grouped per tile
    ├────────────────┤
    │ tile index     │  fixed 16 B per tile, sorted
    └────────────────┘

Ways are stored **once**; the tile index points at them through the
way-ref table. A way crossing several tiles is referenced from each,
never duplicated.

### Header (32 bytes)

| Offset | Size | Field | Notes |
|---|---|---|---|
| 0 | 4 | magic | ASCII `DLRP` |
| 4 | 2 | formatVersion | u16, currently `1` |
| 6 | 2 | flags | u16, all bits reserved (must be 0) |
| 8 | 2 | country | 2× ASCII, ISO 3166-1 alpha-2 (`FI`, `SE`, `NO`, `DK`, `EE`) |
| 10 | 2 | tileMilliDeg | u16, tile edge in millidegrees (100 = 0.1°) |
| 12 | 4 | osmDataDays | u32, days since 1970-01-01 — the "data date" |
| 16 | 4 | packVersion | u32, monotonic build number for update checks |
| 20 | 4 | wayCount | u32 |
| 24 | 4 | tileCount | u32 |
| 28 | 4 | tileIndexOffset | u32 |

A reader must reject a file whose magic or version it does not know,
and must treat any offset or count that runs past the end of the file as
corruption.

### Way record

| Field | Type | Notes |
|---|---|---|
| flags | u8 | bit0 explicit maxspeed present · bit1 way id present · bit2 endpoint node ids present · bits 3–7 reserved (0) |
| highwayClass | u8 | see table below |
| maxspeedDiv5 | u8 | only when bit0; limit in km/h ÷ 5, so 1–51 covers 5–255 km/h |
| pointCount | uvarint | ≥ 2 |
| lat0, lon0 | int32 ×2 | first point, 1e-5° |
| deltas | svarint ×2×(pointCount−1) | successive differences, 1e-5° |
| wayId | svarint | only when bit1 — delta against the previous way's id |
| nodeStart, nodeEnd | svarint ×2 | only when bit2 |

`wayId` and the endpoint node ids are reserved grow-room; nothing in the
app reads them yet.

Only a **numeric** `maxspeed` becomes bit0 + `maxspeedDiv5`. Values the
pipeline cannot resolve to a number in km/h — `walk`, zone references,
conditional and directional variants — are dropped to "no explicit
limit", which the app then treats as estimated from the road class,
never presented as a signed limit.

### Highway classes

| Value | OSM `highway` |
|---|---|
| 0 | other / unrecognised |
| 1 | motorway |
| 2 | trunk |
| 3 | primary |
| 4 | secondary |
| 5 | tertiary |
| 6 | unclassified |
| 7 | residential |
| 8 | living_street |
| 9 | service |
| 10 | track |
| 11 | motorway_link |
| 12 | trunk_link |
| 13 | primary_link |
| 14 | secondary_link |
| 15 | tertiary_link |

An unrecognised value must read as `0`, never fail the parse: a newer
pipeline may add classes, and an older reader should degrade rather
than refuse the pack.

### Way-ref table and tile index

The way-ref table is a flat array of `u32` way offsets. Each tile owns a
contiguous run of it.

Tile index entries are 16 bytes, **sorted ascending by (latIndex,
lonIndex)** so a reader can binary-search:

| Offset | Size | Field |
|---|---|---|
| 0 | 4 | latIndex (int32) |
| 4 | 4 | lonIndex (int32) |
| 8 | 4 | wayRefOffset (u32) |
| 12 | 4 | wayRefCount (u32) |

Tile indices are `floor(degrees × 1000 / tileMilliDeg)`, so they are
negative south of the equator and west of Greenwich. At the default
0.1° a tile is ~11 km north–south and ~5.5 km east–west at 60°N.

## What a reader must do

1. Validate magic, version, and that every offset lies inside the file.
2. Binary-search the tile index for each tile the query box touches.
3. Collect way offsets from those tiles, **deduplicating** — a way
   referenced from three tiles must be parsed once.
4. Parse each way lazily; a malformed record ends that way, and the
   pack, with a clear failure rather than a partial result.

## Deliberate non-goals

- No connectivity, turn restrictions, or one-way flags — DryLine does
  not route.
- No names, surfaces, or anything else not needed to time a ride.
- No per-way updates: packs are replaced wholesale.
