# NEO CIVITAS — DEVELOPMENT_ROADMAP.md
Version 0.1

Milestone rule: every milestone ends in a build that RUNS and is saved as a git tag.

## Phase 1 — Playable Foundation
**1a — Ground & Camera** (target: first week of work)
- Godot project boots, flat terrain grid (128x128 cells) + one river strip
- Camera: pan (WASD/edge), zoom (wheel), rotate (Q/E), tilt
- Grid hover highlight, cell coordinates in debug label
- DONE WHEN: you can fly around a green map and see which cell the mouse is on.

**1b — Roads & Zones**
- Road placement tool (drag straight segments), road graph in SimCore
- Zoning brush: Residential / Commercial / Industrial (low density only)
- Buildings auto-spawn on zoned cells adjacent to a road (placeholder boxes: green/blue/yellow)
- DONE WHEN: draw a road, paint zones, watch boxes appear.

**1c — People & Money**
- Population cohorts grow if housing + jobs available; demand bars R/C/I
- Jobs: commercial/industrial buildings offer jobs; unemployment tracked
- Monthly tax income, running balance, building costs deduct money
- Simulation speed: pause / 1x / 3x / 10x
- DONE WHEN: city grows on its own, money goes up/down believably.

**1d — Utilities, UI, Save**
- Power plant + water tower placeables, coverage radius; unpowered buildings stall
- Top bar UI: money, income, population, demand, date, speed controls
- Building click -> info panel; Save / Load / Autosave, 3 city slots
- DONE WHEN: full loop — new city -> build -> grow -> save -> quit -> load -> continue.

**Phase 1 exit criteria:** 30 minutes of play with no crash; save/load lossless; SimCore tests green.

## Phase 2 — Services & Living City v1
Traffic flow model (district matrix + cosmetic vehicles), schools/hospitals/police/fire/garbage, districts with named stats, property values, household cohorts, first individual-citizen promotion (click a building -> see a generated resident profile backed by cohort data), aggregated company records.

## Phase 3 — Deep Economy & Memory
Production chains (3 chains to start: food, steel->machinery, consumer goods), logistics, bank loans + city bonds, economic cycles, startups, research tree v1, City Chronicle UI, politics-lite (approval, issue weights), advanced events.

## Phase 4 — Spectacle
Weather + day/night polish, disasters interacting with infrastructure, airport/port/rail, mega-projects, future tech tier, external world trade.

## Phase 5 — Scale
Profile first. Then benchmark ladder: 10k -> 50k -> 100k -> 250k -> 500k -> 1M cohort-residents. No target promised until measured.

## Testing (starts Phase 1c)
xUnit tests in /simtests: tax math, demand model, building growth rules, save/load round-trip. Debug overlay (F3): tick rate, cohort table, money flows.

## Git Discipline
- main = always runs; feature branches per milestone; tag at each DONE (v0.1a, v0.1b, ...)
- Commit message format: `[1b] roads: drag placement + graph`
