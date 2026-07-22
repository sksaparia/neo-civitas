# NEO CIVITAS — ARCHITECTURE.md
Version 0.1 — Phase 0 (approved baseline)

## 1. Core Principle
Two worlds, strictly separated:

- **SimCore** — pure C# class library. No Godot references. Owns all game state and rules. Can run headless (for automated tests and benchmarks).
- **GameShell** — Godot 4 (.NET) project. Rendering, camera, input, UI, audio. Reads read-only snapshots from SimCore and sends Commands to it.

Rule: GameShell never mutates simulation state directly. All changes go through `SimCommand` objects (PlaceRoad, ZoneArea, SetTaxRate, ...). This keeps save/load, replay, and testing sane.

## 2. Repository Layout
```
neo-civitas/
  ARCHITECTURE.md
  DEVELOPMENT_ROADMAP.md
  simcore/                # pure C# library (.NET 8)
    SimCore.csproj
    World/                # WorldState, TimeSystem, TickScheduler
    Terrain/              # heightmap, water, resources
    Roads/                # graph: nodes, segments, hierarchy
    Zoning/               # zone grid (R/C/I density levels)
    Buildings/            # building records, evolution levels
    Population/           # cohorts, later individuals (LOD)
    Economy/              # money flows, demand, firms (aggregated)
    Utilities/            # power, water coverage
    Government/           # budget, taxes, policies
    Events/               # EventLog -> City Chronicle
    Save/                 # versioned serialization
  simtests/               # xUnit tests for SimCore (headless)
  game/                   # Godot project (GameShell)
    project.godot
    scenes/
    scripts/              # thin GDScript/C# glue only
    ui/
    assets/               # placeholders only, no copyrighted assets
```

## 3. Data Design (data-oriented)
- No per-citizen C# objects. Population stored as **cohort arrays**: struct rows keyed by (district, age band, education, income band). Counts + rates, not individuals.
- Buildings: one flat `List<BuildingRecord>` (struct-like) with int IDs; grid cell -> buildingId lookup for spatial queries.
- Roads: graph of nodes/segments with int IDs; adjacency lists. Traffic later = flow numbers on segments, not simulated cars.
- Money: `long` in whole currency units (no floats for money).
- All cross-references by int ID, never object references — this makes saving trivial and cache-friendly.

## 4. Tick Scheduler
Game time advances in fixed sim ticks (1 tick = 1 in-game hour at 1x speed).
Systems subscribe at different frequencies:
- Utilities coverage: on-change + daily
- Building growth/demand: daily
- Population update: weekly
- Economy/taxes/budget: monthly
- Chronicle checks: event-driven
Time slicing: heavy systems may split work across multiple real frames.

## 5. Sim ↔ Render Bridge
- SimCore emits `SimEvent`s (BuildingSpawned, BuildingUpgraded, MoneyChanged, ...).
- GameShell listens and updates visuals (MultiMeshInstance3D for buildings/trees, simple materials).
- UI polls a `CitySnapshot` (population, money, demand bars) at ~4 Hz, not every frame.
- A citizen/vehicle is rendered only as cosmetic representation of aggregate state.

## 6. Save System
- Format: single file = header (version int, seed, timestamps) + per-module binary blocks, each block tagged with its own version.
- Loader skips/upgrades unknown blocks -> forward compatibility where practical.
- Autosave every N in-game months; multiple city slots.

## 7. City Chronicle (foundation now, feature later)
`EventLog` records structured events (type, date, location, magnitude) from Phase 1 onwards (even boring ones like "first road built"). Phase 3 turns this into the browsable Chronicle and lets events influence land value / district identity. Recording early means history exists later.

## 8. Performance Doctrine
- Object pooling for visuals; instancing (MultiMesh) for repeated meshes.
- Chunked terrain (e.g. 32x32-cell chunks) with LOD.
- Never iterate all cells per frame; dirty-flag systems.
- Benchmarks in simtests must pass before population targets are claimed.

## 9. Decisions Log
- D-001: Godot 4 .NET chosen over Unity/Unreal (licensing, AI-assist friendliness, iteration speed).
- D-002: Cohort-first population model; individuals are promoted on demand (LOD-for-people).
- D-003: Money as integer `long`.
- D-004: Command pattern for all state mutation.
- D-005: Phase 1 map = flat plains + one river, single seed; full procedural terrain deferred.
