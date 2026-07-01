# OGame 0.84 Implementation Map

## Goal

This map ties the OGame 0.84 documentation set to concrete files already present in the repository.

## Repository Mapping

| Concern | File / Route | Notes |
|---|---|---|
| OGame-style sandbox route | `src/router/config.tsx` → `/game-test` | route entry for the dedicated test page |
| Sandbox page implementation | `src/pages/game-test/page.tsx` | runs resource, building, research, fleet, combat, loop, and database checks |
| Cost and timing formulas | `src/utils/gameCalculations.ts` | source of building, research, ship, and combat formulas |
| Existing page documentation | `docs/pages/game-test.md` | short page-level summary already in docs |
| OGame theme tokens | `tailwind.config.ts` | contains `ogame`-named theme classes for UI styling |

## OGame 0.84 Feature Mapping

| OGame 0.84 concept | Current repository representation |
|---|---|
| economic opening loop | resource hooks plus building cost helpers |
| research ladder | research cost and research time helpers |
| shipyard progression | ship cost helpers and sandbox ship test |
| fleet combat | combat power aggregation plus six-round simulation |
| spy / intel loop | espionage technology cost baseline present in utilities |
| test server / sandbox | `/game-test` page for isolated validation |

## Recommended Documentation Usage

1. start with [README.md](README.md)
2. review [SYSTEMS.md](SYSTEMS.md) for the core ruleset
3. use [UML.md](UML.md) when discussing architecture or planning UI/system work
4. use this file to find the implementation entry points before editing game logic

## Boundaries

- this folder documents the current OGame-like sandbox only
- it does not claim full parity with the original OGame 0.84 release
- it is intended as a focused reference set for design, testing, and future feature work
