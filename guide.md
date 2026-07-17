---
title: User Guide
---

# DryLine — user guide

Three tabs: **Map**, **Routes**, **Settings**. Everything is sized for
gloves; the important stuff is big and high-contrast.

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
- **Attribution**: the small (i) next to the MapLibre logo
  (bottom-left) lists the map and weather data providers.

## Routes tab

DryLine does not plan routes — plan in **stegra.io** (or anything that
exports GPX), then:

1. Export/download the route as a **GPX file** to your phone.
2. Routes tab → import, pick the file.
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

## Navigate — turn-by-turn along your route

With a route shown on the map, tap the **🧭 button**:

- Turn-by-turn guidance along **exactly the GPX you imported** — no
  rerouting, ever. If you leave the track, a red **"Off route"** chip
  tells you how far off you are and counts down as you ride back; the
  route never changes underneath you. The track is the truth.
- Banners announce turns synthesized from the route shape ("Turn left
  in 700 m"), with a "continue" reminder every ~2 km on straights.
  Distances are always metric. Voice speaks each instruction ~300 m
  out — the speaker button on the nav screen mutes it.
- **The weather rides with you.** The nav map shows the live rain
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

## Settings tab

- **Radar opacity** — how strongly radar paints over the map.
- **Alert threshold** — what counts as rain worth an alert: drizzle /
  light (default) / moderate. Changes apply from the next check, even
  mid-ride.
- **Night map style** — dark map for night rides (day style is the
  sunlight-readable default).
- **Alert history** — the last 200 alerts, with a Clear button.
- **About** — data sources, attribution, version.

## Good to know

- No account, no cloud: everything stays on the phone — see
  [how DryLine handles your data](data.md) and the
  [privacy policy](privacy.md).
- The app is **advisory only** — it says "expected" and "may" because
  that is what a forecast is. Gear up on the alert, but ride by the sky.
- Found a bug or a wrong forecast? Email <foodoo@iki.fi> with the time
  it happened — the alert history helps reconstruct it.
