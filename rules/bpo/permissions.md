---
paths:
  - "apps/bpo/**"
---

# BPO User Entity Permissions

## User Types

| Type | Permission Source | Logic |
|------|------------------|-------|
| WORKSPACE | `workspace_user_country` | Automatic via country |
| CLIENT | `client_user_country` | Automatic via client + country |
| PROVIDER | `provider_user_employment_entity` | Explicit assignment |

## Materialized View

`user_entity_permission` in `auth.hcl` controls entity visibility.

## Key Tables

| Table | Purpose |
|-------|---------|
| `workspace_user_country` | Country assignments (WORKSPACE) |
| `client_user_country` | Country assignments (CLIENT) |
| `provider_user_employment_entity` | Entity mapping (PROVIDER) |
| `recurring_payrun_member` | Payrun membership |

## Permission Checks

- Always verify permissions before data access
- Use permission helpers from shared utilities
- Log permission denials for audit

## Gotchas

| Issue | Behavior |
|-------|----------|
| `only_assigned_payruns = true` | Restricts to payrun membership only |
| CLIENT users | Cannot access Settings pages |
| PROVIDER detail pages | Get 404 even if list visible |

## Testing Permissions

- Test each role separately
- Test permission boundaries (what users CAN'T do)
- Use E2E tests for permission flows

## Citations

| Fact | Citation |
|------|----------|
| Materialized view SQL | `file:apps/bpo/db/schemas/auth.hcl:871-916` |
| Permission tests | `file:apps/bpo/web/src/e2e/tests/permissions/` |
