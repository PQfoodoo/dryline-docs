---
title: Privacy Policy
---

# DryLine — Privacy Policy

_Last updated: 17 July 2026_

DryLine is an Android app that overlays rain radar on a map, navigates your
own GPX route, and warns motorcycle riders when rain is likely on their
route. **It has no user accounts, no ads, no analytics, and no backend
server.** There is no server of ours for your data to go to.

## Data DryLine collects about you

**None.** The developer receives no data from this app. There is no telemetry,
no crash-reporting service, no advertising SDK, and no account system. The
developer cannot see where you are, where you ride, or whether you use the app
at all.

## Data DryLine uses on your device

| Data | Where it lives | Leaves the phone? |
|---|---|---|
| GPS position | In memory while the app or ride mode runs; no track log is kept | Only as coordinates sent to `api.met.no` to fetch the rain forecast for your area, rounded to roughly 11 m — never more precise than the forecast needs |
| Imported routes (GPX) | On the phone until you delete them | No |
| Alert history (time + place of each alert) | On the phone, newest 200; clearable in Settings | No |
| Settings | On the phone | No |
| Crash log (technical traces, no location) | On the phone, capped at 256 KB | No |

## Third-party services DryLine contacts

DryLine talks to exactly three services, none of which receive an identity or
an account:

- **MET Norway Nowcast** (`api.met.no`) — rain forecasts. Receives approximate
  coordinates.
- **MET Norway thredds** (`thredds.met.no`) — weather-radar imagery. Receives
  the map area being viewed.
- **OpenFreeMap** (`openfreemap.org`) — background map tiles. Receives the map
  area being viewed.

These requests reveal the geographic area you are viewing, as any map or
weather app must. They carry no identifier, no account, and no profile. Their
own handling of requests is governed by their respective privacy terms.

## Voice guidance and Android Auto

Voice guidance is spoken by **your phone's own text-to-speech engine** (a
system service). DryLine hands it only the instruction text — for example
"Turn left in 300 meters" or "Light rain on your route in about 10 minutes" —
never your position. On **Android Auto**, DryLine projects the same
navigation and weather view to the car screen; this adds no data collection
and no new network services.

## Backups

**None.** DryLine opts out of Android's automatic app backup and phone-to-phone
transfer entirely, because routes and alert history are location data and can
reveal your home. **Uninstalling the app deletes everything.**

## Permissions

- **Location (while using the app)** — the map's follow-me and the
  rain-around-you forecast. The app holds **no background-location
  permission**; ride mode works via its visible notification, not background
  access.
- **Notifications** — rain alerts.

## Children

DryLine is not directed at children and collects nothing from anyone.

## Advisory only

DryLine is **advisory only**. Forecasts are probabilistic; the app says
"expected" and "may" and means it. It is a decision aid for gearing up early —
not a guarantee of dry roads. Ride by the sky and the road.

## Contact

foodoo@iki.fi
