---
paths:
  - "apps/bpo/db/**"
---

# BPO Database Migrations

## Source of Truth

HCL schemas in `apps/bpo/db/schemas/*.hcl`

## Workflow

### 1. Edit Schema

Modify `.hcl` files (auth.hcl, payroll.hcl, etc.)

### 2. Generate Migration

```bash
moon bpo-db:migrate-diff
```

Creates SQL file in `apps/bpo/db/migrations/`

### 3. Apply Migration

```bash
moon bpo-db:migrate-apply-k8s   # For Tilt/K8s
moon bpo-db:migrate-apply       # For local
```

## Ports

| Port | Purpose |
|------|---------|
| 5432 | Real K8s database (Tilt) |
| 5433 | Atlas dev database |

## Conventions

- One migration per logical change
- Reversible migrations preferred
- Test migrations in dev before staging
- Never modify existing migrations

## Gotchas

| Wrong | Right |
|-------|-------|
| `atlas migrate apply --env=local` | `moon bpo-db:migrate-apply-k8s` |
| Assume Tilt applies migrations | Must run `migrate-apply-k8s` manually |

## Citations

| Fact | Citation |
|------|----------|
| HCL source of truth | `file:apps/bpo/db/README.md` |
| Moon tasks | `file:apps/bpo/db/moon.yml` |
