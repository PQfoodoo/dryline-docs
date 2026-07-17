---
title: Ride Simulation
---

# DryLine — ride simulation (test builds)

Test builds of DryLine have a **SIM** button on the map. It replays a route as
if you were riding it — real app, real weather, simulated GPS — so you can see
what DryLine does on a ride without leaving the couch.

## What it does

- Pick a route (Routes tab → tap one so it shows on the map), then tap
  **SIM**. Navigation starts and a simulated rider follows your GPX at
  several times riding speed.
- **Everything except the GPS is real.** Turn-by-turn guidance, voice, the
  live radar, the rain-colored route, the "rain on your track in ~N min"
  card, rain alerts, the ride notification — and, if connected, the Android
  Auto screen — all run exactly as on a real ride, driven by the simulated
  position against the **live weather right now**.
- That makes it the honest way to preview a ride's weather: pick tomorrow's
  route today, SIM it, and watch where the forecast paints rain and when the
  warnings would fire.

## Notes

- The **SIM button exists only in test builds** — it is a development and
  verification tool, not a production feature.
- The simulation moves fast (time-compressed), so spoken instructions and
  alerts come quicker than on a real ride — that's the speed-up, not the
  app being wrong.
- Distances, timings and rain verdicts are computed the same way as on a
  real ride; only the position is fake. Your actual location is not used
  while the simulation runs.
- Stop it like any navigation: the ✕ on the trip bar (and stop ride mode
  with the 🏍 button if you're done).
