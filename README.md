# 🏙️ NEO CIVITAS — City of a Million Stories

A browser-based city builder & economic simulation game. Start with empty land in 2035, build roads, zone neighborhoods, provide utilities, and grow a living city — no install needed, runs anywhere.

**▶️ PLAY NOW:** https://sksaparia.github.io/neo-civitas/neo-civitas-v01.html

Built with Three.js + vanilla JavaScript. Designed and developed with AI-assisted engineering.

## 🎮 Current Features (v0.1 — First Playable)
- Procedural terrain with river, 128×128 buildable grid
- Full city-builder camera (pan / zoom / rotate / tilt)
- Road construction with drag placement (Bresenham line interpolation)
- Zoning: Residential / Commercial / Industrial with automatic building growth
- Power plants & water towers with coverage radius — buildings need both to develop
- Living economy: population migration, jobs, monthly tax income, maintenance costs
- Simulation speeds: pause / 1x / 3x / 10x
- Save / Load / Autosave (browser storage)
- Click-to-inspect any building

## 🗺️ Version History
| Version | Milestone | Link |
|---|---|---|
| m1a | Terrain & Camera | [play](https://sksaparia.github.io/neo-civitas/neo-civitas-m1a.html) |
| m1b | Roads & Zoning | [play](https://sksaparia.github.io/neo-civitas/neo-civitas-m1b.html) |
| m1c | Population, Jobs & Taxes | [play](https://sksaparia.github.io/neo-civitas/neo-civitas-m1c.html) |
| **v0.1** | **First Playable (utilities + save/load)** | **[play](https://sksaparia.github.io/neo-civitas/neo-civitas-v01.html)** |

## 🚧 Roadmap
- **Phase 2 (in progress):** city services (schools, hospitals, police, fire), citizen happiness, traffic, districts, property values
- **Phase 3:** production chains, banking, startups, City Chronicle (persistent city history), politics
- **Phase 4:** disasters, airports/ports, mega-projects, future technology
- **Phase 5:** large-city optimization (benchmark ladder to 1M cohort-residents)

See [ARCHITECTURE.md](ARCHITECTURE.md) and [DEVELOPMENT_ROADMAP.md](DEVELOPMENT_ROADMAP.md) for design details.

## 🧠 Design Philosophy
> Every building has a purpose. Every company has an economy. Every citizen has a life. Every neighborhood has a history. Every decision has consequences.

Simulation state (SimCore) is strictly separated from rendering (GameShell), with cohort-based population modeling for future scale.

## 📜 License & Assets
Original game. All geometry is procedural; no copyrighted game assets used.
