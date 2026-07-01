# Backend & Database

Backend behavior in this repository is split across two server-side areas:

- `supabase/functions/` — live game backend handlers deployed as Supabase Edge Functions
- `database/no_mans_sky/` — a checked-in SQL pack for the No Man's Sky content catalog

## Runtime Overview

| Layer | Location | Responsibility |
|---|---|---|
| Client gateway | `src/lib/supabase.ts` | Creates the shared Supabase client used by the React app |
| Edge runtime | `supabase/functions/*/index.ts` | Handles authenticated server-side game actions |
| Primary backend data | Supabase Postgres | Stores player, planet, fleet, research, economy, and admin data |
| Reference SQL pack | `database/no_mans_sky/*.sql` | Defines a normalized exploration/catalog database |

## Backend Feature Areas

### Account bootstrap

The account functions create a fully playable starter state instead of only creating auth users.

| Function | Purpose | Main tables touched |
|---|---|---|
| `create-user-account` | Creates a confirmed user plus starter empire state | `profiles`, `player_resources`, `resources`, `planets`, `buildings`, `population_data`, `ships`, `research`, `leaderboard` |
| `create-demo-user` | Creates or refreshes demo access for testing | `profiles`, `player_resources`, `planets`, `buildings` |
| `resend-verification-email` | Re-triggers auth verification | Supabase Auth |

### Admin operations

| Function | Purpose | Main tables touched |
|---|---|---|
| `bootstrap-admin` | Creates the first admin record | `admin_users`, `admin_logs` |
| `seed-admin` | Seeds admin data for setup flows | `admin_users`, `admin_logs` |
| `check-admin-exists` | Checks whether admin bootstrap already happened | `admin_users` |
| `admin-verify-user` | Marks players as manually verified | `admin_users`, `admin_logs` |
| `resolve-admin-email` | Resolves which email is mapped to an admin | `admin_users` |
| `list-pending-verifications` | Lists players waiting for approval | verification-related auth/profile data |

### Game simulation

| Function | Purpose | Main tables / RPC used |
|---|---|---|
| `process-resource-tick` | Computes elapsed production and updates stored resources | `player_resources`, `planets`, `buildings` |
| `process-fleet-mission` | Schedules outbound missions and computes travel/fuel | `fleets`, `planets`, `fleet_missions`, `server_settings`, `deduct_resources()` |
| `process-expedition` | Rolls expedition outcomes and rewards | `fleets`, `expedition_results`, `add_resources()` |
| `resolve-combat` | Resolves fleet-vs-fleet combat rounds | fleet records plus combat payload |
| `process-missile-attack` | Applies missile damage to target assets | `ships`, `missile_attacks` |
| `process-marketplace-trade` | Executes market trades | marketplace and resource tables |
| `process-harvest-debris` | Converts debris fields into returned resources | `fleets`, `debris_fields`, `fleet_missions` |
| `create-moon-from-debris` | Attempts moon creation from a debris field | `debris_fields`, `server_settings`, `planets` |

## Common Edge Function Pattern

Most handlers follow the same structure:

1. Reply to CORS preflight requests.
2. Validate HTTP method and JSON body.
3. Read Supabase environment variables.
4. Authenticate the caller when the action is player-specific.
5. Query or mutate Postgres tables.
6. Return a JSON payload for the React client.

Privileged flows such as account creation use the service-role key, while gameplay flows usually validate a bearer token first and then read/write gameplay tables.

## Core Gameplay Tables Seen In Server Code

These are the main live-game tables referenced directly by the server-side files in this repository:

- `profiles`
- `player_resources`
- `resources`
- `planets`
- `buildings`
- `population_data`
- `ships`
- `research`
- `leaderboard`
- `fleets`
- `fleet_missions`
- `debris_fields`
- `server_settings`
- `admin_users`
- `admin_logs`
- `missile_attacks`
- `expedition_results`

## SQL Pack: `database/no_mans_sky`

The checked-in SQL files are a separate, normalized content database for universe cataloging.

### What it contains

- Core geography: `galaxies`, `regions`, `star_systems`, `planets`
- Discovery content: `flora`, `fauna`, `minerals`, `buildings`, `space_stations`
- Equipment and vehicles: `ships`, `multitools`, `freighters`, `frigates`
- Classification tables: `galaxy_types`, `economy_types`, `conflict_levels`, `species`, `factions`, `biomes`
- Join tables such as `planet_resources`

### Load order

Use `database/no_mans_sky/load_all.sql` or load the files in the order documented in `database/no_mans_sky/README.md`.

### Important distinction

The SQL pack is versioned in this repository, but the live Supabase game schema is not checked in here as migrations. For the live game backend, the most reliable source of truth in this repository is the table usage inside `supabase/functions` and the `Database` typing in `src/lib/supabase.ts`.

## Related Files

- [Backend UML](UML.md)
- [`docs/supabase/README.md`](../supabase/README.md)
- [`database/no_mans_sky/README.md`](../../database/no_mans_sky/README.md)
