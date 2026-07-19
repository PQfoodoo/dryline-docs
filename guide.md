---
title: User Guide
---

# DryLine — user guide

Three tabs: **Map**, **Routes**, **Settings**. Everything is sized for
gloves; the important stuff is big and high-contrast.

> **V2 note (2026-07-12):** the map is now OpenStreetMap-based
> (OpenFreeMap) and the radar comes straight from MET Norway — same
> features, slightly different look. Any screenshots floating around
> from V1 show the old Google map; they'll be regenerated.

## Map tab

- **Rain radar overlay** (☂ button): recent radar over the map. The
  small bar bottom-left shows how old the image is ("Radar 3 min ago")
  and turns red if it goes stale — the app never pretends old data is
  fresh. Refresh happens automatically every 5 minutes; the ⟳ button
  forces it.
- **Follow-me + course-up**: the map follows your position and rotates
  to your direction of travel (it holds its heading at traffic lights
  instead of spinning). The **N compass** rotates with the map: tap it
  on a rotated map to snap north-up; tap it when upright to re-engage
  course-up. Panning by hand pauses following — the ◎ button brings it
  back.
- **Clean map**: the chevron handle collapses all controls to a single
  button for a distraction-free riding view. Warning banners and rain
  alerts always stay visible.
- **Banners** at the top tell you honestly when something is off: no
  GPS fix, no network, radar unavailable. No banner = everything live.
- **Attribution**: the small (i) next to the MapLibre logo lists the map
  providers. MET Norway weather credit is under **Settings → About**.

## Routes tab

DryLine does not plan routes — plan in **stegra.io** (or anything that
exports GPX), then:

1. Export/download the route as a **GPX file** to your phone.
2. Get it into DryLine any of three ways: **tap the downloaded file**
   and choose DryLine ("Open with"), **Share → DryLine** from any app,
   or Routes tab → import and pick the file. All three land in the
   same place; a file that isn't valid GPX is refused with an error —
   it can't break anything.
3. Tap the route: the Map colors it by expected rain **at the time
   you would be there** (departing now, ~80 km/h average). Purple =
   dry, blue = light rain, amber = moderate, red = heavy. **Gray
   dashed = no forecast for that stretch** — it's beyond the ~2 h
   horizon, or a spot the forecast service can't see. Unknown is never
   painted dry: for a gray stretch, check the radar picture yourself.
   Tapping the highlighted route again removes it from the map.
   Waypoints show as purple dots with their names always visible — no
   tapping needed on the move.
4. The timeline card gives the verdict in words ("Rain (light)
   expected in ~25 min" — or "No rain expected where forecast is
   available — 1 stretch unknown" when part of the route has no
   forecast). Green pin = start, red pin = end; the riding direction
   is the direction your GPX was drawn.

**Two different times on one map.** The radar overlay shows where rain
is *right now* (the age chip says how fresh). The route colors show
where rain **will be when you pass each point**. So a rain cell
sitting on the far end of your route can honestly show purple — the
forecast expects it to move off before you arrive, and you'd ride in
behind the rain. The reverse also happens: a road that looks clear now
can color blue for later. The picture assumes you depart *now*; it
refreshes with the radar while the map is open, so glance at it once
more right before you actually set off.

## Navigate — turn-by-turn along your route (V2)

With a route shown on the map, tap the **🧭 button**:

- Turn-by-turn guidance along **exactly the GPX you imported** — no
  rerouting, ever. If you leave the track, a red **"Off route"** chip
  tells you how far off you are and counts down as you ride back; the
  route never changes underneath you. The track is the truth.
- Banners announce turns synthesized from the route shape ("Turn left
  in 700 m"), and between turns the banner counts one unbroken distance
  down to the **next real turn** — "Turn right · 33 km" ticking down,
  no filler steps. Distances are always metric. Voice speaks each
  instruction ~300 m out — the speaker button on the nav screen mutes it.
- **The weather rides with you (V2).** The nav map shows the live rain
  radar and your route colored by expected rain, the same as the Routes
  tab — you don't leave navigation to see what's coming. When rain sits
  on the track ahead, a card tells you how soon and how far: "Rain
  (light) on your track in ~15 min · ~12 km ahead", with how long it
  may last. A dry road ahead shows no card; a gray (unknown) stretch is
  never called dry. Same advisory-only rule as everywhere else.
- **Spoken rain warnings.** A short weather briefing when the ride
  starts, and a spoken "rain on your route in about N minutes" callout
  as rain approaches — with a rider-adjustable lead time. The same
  speaker button mutes all voice.
- Starting navigation also starts **ride mode**: rain alerts and the
  persistent notification run through your whole navigation session.
  Exiting navigation keeps ride mode on — stop it with the 🏍 button
  when you're done riding.
- At the destination, "You have arrived 🏁" takes you back to the map.

## Ride mode — the alerts

Tap the **🏍 button** on the map when you start riding:

- A persistent notification shows a live outlook every ~5 minutes:
  "Rain (moderate) expected in ~18 min", "No rain expected for the
  next ~115 min", or — if the forecast can't be fetched — "Rain
  forecast unavailable — watch the sky".
- When rain is expected within **~30 minutes** of your position, you
  get a loud alert: what severity, how many minutes out, and roughly
  how long it may last ("heavy for ~5 min" vs "light for an hour" is
  the difference between waiting it out and gearing up).
- It won't spam: repeat alerts only after ~20 min, and once you're
  already riding in the rain it stays quiet unless the rain gets
  **heavier**.
- Works with the screen off. Battery cost is small (~1 %/h of the
  app's own doing; a riding phone burns more on the cell radio).
- Tap the notification to open the map; stop the ride from the map
  button or the notification. **Remember to stop it** when you're done.

## Android Auto — DryLine on the car screen

Connect the phone to an Android Auto head unit and DryLine appears among
the car's apps. Start navigation **on the phone** — the car mirrors it:

- A course-up map with your route, the live rain radar, and the route
  colored by expected rain — the same picture as the phone, built for a
  glance.
- The next turn rides on the map as a pill: **"Turn right · 1.5 km"**,
  counting down to the real maneuver. When rain sits on your track, a
  second pill appears under it: **"Rain in ~7 min"** with a severity
  dot. Dry road and fresh radar = no pills besides the turn — nothing
  to worry about is shown as nothing.
- If the radar image gets old (no coverage, bad network), a **"Radar N
  min old"** note appears instead of silently showing stale rain — the
  same honesty rule as the phone.
- A small next-turn readout also lives in the car's app rail, and rain
  warnings pop up as car notifications.
- **Off route?** The car keeps the map on you and shows "Off route" —
  it never reroutes; the track is the truth. The phone shows how far
  off you are as you ride back.
- The phone stays in charge: voice, ride-mode alerts and the session
  itself all run on the phone; the car is a second screen. Locking the
  phone is fine.

If DryLine doesn't show up in the car: make sure it was installed from
Play (sideloaded builds are rejected by Android Auto), and check it
isn't caught in a phone focus/digital-detox mode that suspends apps. If
the car system's own turn card is missing while DryLine's pills work,
setting the phone to 24-hour time and restarting Android Auto has
helped — a known Android Auto quirk, not a DryLine setting.

## Settings tab

- **Radar opacity** — how strongly radar paints over the map.
- **Alert threshold** — what counts as rain worth an alert: drizzle /
  light (default) / moderate. Changes apply from the next check, even
  mid-ride.
- **Night map style** — dark map for night rides (day style is the
  sunlight-readable default).
- **Alert history** — the last 200 alerts, with a Clear button.
- **About** — linked weather data and licence credits, map attribution,
  version, and a generated list of third-party software licences.

## Where DryLine works

DryLine's rain forecast comes from the Nordic weather-radar network
(MET Norway's nowcast), so the honest answer area is **the Nordics —
Finland, Sweden, Norway and Denmark**. Outside that footprint there is no
forecast data, and DryLine says so instead of guessing:

- A route outside coverage shows **"No forecast for this route"** on the
  timeline, and the spoken ride-start briefing says **"No rain forecast
  is available for this route."** DryLine never claims "no rain" without
  data behind the claim.
- The **radar picture can reach a little farther than the forecast**:
  radar beams don't stop at borders, so rain may be painted just beyond
  the coverage edge — northern Estonia across the Gulf of Finland, for
  example. Treat that fringe as a glimpse, not a forecast: at long range
  radars both miss rain and exaggerate it.
- Riding **into** coverage works: a route that starts outside the Nordics
  but enters them gets real rain information for the covered part.

## Good to know

- No account, no cloud: everything stays on the phone (see fact sheet).
- The app is **advisory only** — it says "expected" and "may" because
  that is what a forecast is. Gear up on the alert, but ride by the sky.
- Found a bug or a wrong forecast? Tell Pekka what time it happened —
  the alert history helps reconstruct it.
