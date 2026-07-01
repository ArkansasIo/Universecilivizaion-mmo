# OGame 0.84 Systems Reference

## Core Resources

| Resource | Role |
|---|---|
| Metal | primary construction material |
| Crystal | research and advanced construction material |
| Deuterium | fuel and advanced fleet resource |
| Energy | production support resource used by energy buildings |

## Building Cost Baselines

These base values match the current calculation utility and scale with `2^(level-1)`.

| Building | Metal | Crystal | Deuterium |
|---|---:|---:|---:|
| Metal Mine | 60 | 15 | 0 |
| Crystal Mine | 48 | 24 | 0 |
| Deuterium Synthesizer | 225 | 75 | 0 |
| Solar Plant | 75 | 30 | 0 |
| Fusion Reactor | 900 | 360 | 180 |
| Robotics Factory | 400 | 120 | 200 |
| Shipyard | 400 | 200 | 100 |
| Research Lab | 200 | 400 | 200 |
| Missile Silo | 20000 | 20000 | 1000 |
| Nanite Factory | 1000000 | 500000 | 100000 |
| Terraformer | 0 | 50000 | 100000 |
| Space Dock | 200 | 0 | 50 |

## Build Time Rule

- building time is derived from `metal + crystal`
- base time = `(totalCost / 2500) * 3600`
- robotics factory reduces time by dividing with `1 + roboticsLevel`
- nanite factory reduces time by dividing with `2^naniteLevel`

## Research Cost Baselines

These base values also scale with `2^(level-1)` in the current sandbox implementation.

| Technology | Metal | Crystal | Deuterium |
|---|---:|---:|---:|
| Energy Technology | 0 | 800 | 400 |
| Laser Technology | 200 | 100 | 0 |
| Ion Technology | 1000 | 300 | 100 |
| Hyperspace Technology | 0 | 4000 | 2000 |
| Plasma Technology | 2000 | 4000 | 1000 |
| Combustion Drive | 400 | 0 | 600 |
| Impulse Drive | 2000 | 4000 | 600 |
| Hyperspace Drive | 10000 | 20000 | 6000 |
| Espionage Technology | 200 | 1000 | 200 |
| Computer Technology | 0 | 400 | 600 |
| Astrophysics | 4000 | 8000 | 4000 |
| Intergalactic Research Network | 240000 | 400000 | 160000 |
| Weapons Technology | 800 | 200 | 0 |
| Shielding Technology | 200 | 600 | 0 |
| Armour Technology | 1000 | 0 | 0 |

## Research Time Rule

- research time is derived from `metal + crystal`
- base time = `(totalCost / 1000) * 3600`
- research lab level reduces time by dividing the base time by `labLevel`

## Fleet Cost Baselines

| Ship | Metal | Crystal | Deuterium |
|---|---:|---:|---:|
| Light Fighter | 3000 | 1000 | 0 |
| Heavy Fighter | 6000 | 4000 | 0 |
| Cruiser | 20000 | 7000 | 2000 |
| Battleship | 45000 | 15000 | 0 |
| Battlecruiser | 30000 | 40000 | 15000 |
| Bomber | 50000 | 25000 | 15000 |
| Destroyer | 60000 | 50000 | 15000 |
| Deathstar | 5000000 | 4000000 | 1000000 |
| Small Cargo | 2000 | 2000 | 0 |
| Large Cargo | 6000 | 6000 | 0 |
| Colony Ship | 10000 | 20000 | 10000 |
| Recycler | 10000 | 6000 | 2000 |
| Espionage Probe | 0 | 1000 | 0 |
| Solar Satellite | 0 | 2000 | 500 |

## Combat Model Used by the Sandbox

Ship combat power is aggregated from base attack, shield, and armor values, then boosted by technology levels:

- weapons bonus = `1 + weaponsTech * 0.1`
- shielding bonus = `1 + shieldingTech * 0.1`
- armour bonus = `1 + armourTech * 0.1`
- total power = `attack + shield + armor`
- the sandbox simulates up to 6 combat rounds and estimates loss percentages from relative damage output

### Base Combat Units Present in the Utility

| Ship | Attack | Shield | Armor |
|---|---:|---:|---:|
| Light Fighter | 50 | 10 | 400 |
| Heavy Fighter | 150 | 25 | 1000 |
| Cruiser | 400 | 50 | 2700 |
| Battleship | 1000 | 200 | 6000 |
| Battlecruiser | 700 | 400 | 7000 |
| Bomber | 1000 | 500 | 7500 |
| Destroyer | 2000 | 500 | 11000 |
| Deathstar | 200000 | 50000 | 900000 |

## Sandbox Test Coverage

The `/game-test` page currently validates these OGame-style loops:

- resource updates and affordability checks
- building cost and build time calculations
- research cost and research time calculations
- ship production costs
- fleet combat power and battle simulation
- game loop production and fleet movement processing
- Supabase-backed table access for live game data
