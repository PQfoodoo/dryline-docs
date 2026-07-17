---
title: How DryLine handles your data
---

# DryLine — what it does with your data

Written after security audits of the full source code, build and APK, plus a
device-level check of the app's actual outbound connections. Short version:
**your location never reaches the developer, and never reaches any cloud of
ours — there is no "ours".**

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
three hosts and nothing else. The developer cannot see where you are, where
you ride, or whether you use the app at all.

**No Google in the map.** The map is MapLibre drawing OpenStreetMap-based
tiles from OpenFreeMap. Google Play services is not involved in rendering the
map, and no API key is needed anywhere in the app.

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

- Rain forecasts: MET Norway Nowcast 2.0 (NLOD / CC BY 4.0).
- Radar images: MET Norway thredds (NLOD / CC BY 4.0).
- Map: OpenFreeMap / OpenMapTiles / © OpenStreetMap contributors.
- Attribution is shown in the app under Settings → About, and behind the (i)
  next to the MapLibre logo on the map.

## The disclaimer that matters

DryLine is **advisory only**. Forecasts are probabilistic; the app says
"expected" and "may" and means it. It is a decision aid for gearing up
early — not a guarantee of dry roads. Ride by the sky and the road.

See also the formal [privacy policy](privacy.md). Contact: <foodoo@iki.fi>
