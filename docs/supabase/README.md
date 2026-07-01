# Supabase

17 Supabase Edge Functions for server-side game logic.

For the consolidated server-side overview, SQL notes, and UML, see [`../backend/README.md`](../backend/README.md).

## Account & Auth Functions

| Function | File | Purpose |
|---|---|---|
| `create-user-account` | `create-user-account/index.ts` | Creates new user account and empire |
| `create-demo-user` | `create-demo-user/index.ts` | Creates demo/test accounts |
| `bootstrap-admin` | `bootstrap-admin/index.ts` | Initial admin setup |
| `seed-admin` | `seed-admin/index.ts` | Seeds admin credentials |
| `check-admin-exists` | `check-admin-exists/index.ts` | Admin existence check |
| `admin-verify-user` | `admin-verify-user/index.ts` | Manual user verification |
| `resolve-admin-email` | `resolve-admin-email/index.ts` | Admin email resolution |
| `resend-verification-email` | `resend-verification-email/index.ts` | Email re-send |
| `list-pending-verifications` | `list-pending-verifications/index.ts` | Pending verifications list |

## Game Logic Functions

| Function | File | Purpose |
|---|---|---|
| `process-fleet-mission` | `process-fleet-mission/index.ts` | Fleet movement execution |
| `process-expedition` | `process-expedition/index.ts` | Expedition outcome generation |
| `resolve-combat` | `resolve-combat/index.ts` | PvP combat resolution |
| `process-missile-attack` | `process-missile-attack/index.ts` | Interplanetary missile attacks |
| `process-marketplace-trade` | `process-marketplace-trade/index.ts` | Trade execution |
| `process-resource-tick` | `process-resource-tick/index.ts` | Resource production tick |
| `process-harvest-debris` | `process-harvest-debris/index.ts` | Debris field harvesting |
| `create-moon-from-debris` | `create-moon-from-debris/index.ts` | Moon creation from debris |
