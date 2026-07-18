---
title: Data fact sheet
---

# DryLine — fact sheet (what it does with your data)

Written after security audits of the full source code, build and APK (V1:
2026-07-09/10; V2 map migration: 2026-07-12; V2 navigation delta: 2026-07-13),
plus a device-level check of the app's actual outbound connections
(2026-07-14). Short version: **your location never reaches Pekka, and never
reaches any cloud of ours — there is no "ours".**

## What DryLine is

An app that overlays rain radar on a map, predicts rain along an imported
route, and — in ride mode — watches the nowcast around your GPS position and
alerts you ~10-30 minutes before rain reaches you.

## Where your data goes

| Data | Where it lives | Does it leave the phone? |
|---|---|---|
| Your GPS position | In memory while the app / ride mode runs — no track log is kept | Sent to **api.met.no** (Norwegian Meteorological Institute) to fetch the rain forecast for where you are, rounded to ~11 m precision — never more precise than the service needs. Nothing else receives your position. |
| Alert history (time + place of each rain alert) | On the phone, newest 200, Settings → Clear history | No |
| Imported routes (GPX) | On the phone until you delete them | No |
| Settings | On the phone | No |
| Crash log (technical stack traces, no location) | On the phone, 256 KB cap | No |

**Cloud backups: none.** The app opts out of Google's automatic app backup and
phone-to-phone transfer entirely, because routes and alert history are location
data (they can include your home). Uninstalling deletes everything.

**Telemetry: none.** No analytics, no crash reporting service, no backend. The
only servers the app ever talks to are `api.met.no` (forecast),
`thredds.met.no` (radar images) and `tiles.openfreemap.org` (the map itself).
This was verified on-device by inspecting the app's live connections — those
three hosts and nothing else. Pekka cannot see where you are, where you ride,
or whether you use the app at all.

**No Google in the map.** V2 dropped the Google Maps SDK entirely (ADR-0003):
the map is MapLibre drawing OpenStreetMap-based tiles from OpenFreeMap. Google
Play services is no longer involved in rendering the map, and no API key is
needed anywhere in the app.

**Everything is encrypted in transit.** All three endpoints are HTTPS, the app
contains no cleartext URLs, and it ships a network-security config that forbids
cleartext HTTP outright on every supported Android version.

**Radar and map requests** (`thredds.met.no`, `tiles.openfreemap.org`) ask for
the map *area you are looking at*, not your position, and carry no identifier —
the same as any map app.

## Permissions it asks for, and why

- **Location (while using the app)** — the map's follow-me and the
  rain-around-you forecast. There is no background-location permission
  in the app at all; ride mode works because of its visible
  notification, not background access.
- **Notifications** — the rain alerts.

(It also holds the non-prompted standard internet/network-state and
foreground-service permissions that the above require.)

## Weather sources and credit

- Rain forecasts: Based on data from
  [MET Norway](https://api.met.no/weatherapi/nowcast/2.0/documentation) —
  Nowcast 2.0.
- Radar images: Based on data from
  [MET Norway](https://thredds.met.no/thredds/catalog/remotesensing/reflectivity-nordic/catalog.html) —
  Nordic radar composite.
- Weather-data licence:
  [NLOD 2.0 / CC BY 4.0](https://www.met.no/en/free-meteorological-data/Licensing-and-crediting).
- Map: OpenFreeMap / OpenMapTiles / © OpenStreetMap contributors.
- Linked weather source/licence credits are under Settings → About. Map
  credits are there too and behind the (i) next to the MapLibre logo.

## The disclaimer that matters

DryLine is **advisory only**. Forecasts are probabilistic; the app says
"expected" and "may" and means it. It is a decision aid for gearing up
early — not a guarantee of dry roads. Ride by the sky and the road.
