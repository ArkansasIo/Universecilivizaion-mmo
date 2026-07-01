# OGame 0.84 Test Documentation

This folder collects a focused OGame 0.84 documentation pack for the existing `/game-test` sandbox in this repository.

## Purpose

- describe the intended OGame 0.84 gameplay loop
- document the current sandbox route and calculation utilities
- keep UML and system notes in one dedicated place

## Documents

| File | Purpose |
|---|---|
| [README.md](README.md) | entry point for the OGame 0.84 doc set |
| [UML.md](UML.md) | structural, flow, and state UML diagrams |
| [SYSTEMS.md](SYSTEMS.md) | resources, buildings, research, fleet, and combat rules |
| [IMPLEMENTATION_MAP.md](IMPLEMENTATION_MAP.md) | mapping between OGame 0.84 concepts and repository files |

## Current Repository Touchpoints

- **Sandbox route:** `/game-test`
- **Page implementation:** `src/pages/game-test/page.tsx`
- **Route registration:** `src/router/config.tsx`
- **Core formulas:** `src/utils/gameCalculations.ts`
- **Existing page documentation:** `docs/pages/game-test.md`

## OGame 0.84 Scope Covered Here

This pack focuses on the classic browser-game loop that already appears in the sandbox implementation:

1. gather **metal**, **crystal**, and **deuterium**
2. upgrade economic and infrastructure buildings
3. unlock research milestones
4. produce fleets and probes
5. resolve fleet power and combat outcomes
6. validate the systems inside the `/game-test` page

## Notes

The material here is documentation-only. It does not change gameplay logic, formulas, or routes.
