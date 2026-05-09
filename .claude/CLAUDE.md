# OPS PLATFORM — Monorepo

Central monorepo dispatching to multiple *-ops projects.

## Current Apps

- **bar-ops** — Event Management SaaS
  - Location: `apps/bar-ops/`
  - See: [PROJECT_CONTEXT.md](../apps/bar-ops/PROJECT_CONTEXT.md)

## Future Apps

- *-ops projects (to be expanded)

## Shared Infrastructure

- **Netlify Functions** — Serverless backend (shared across apps)
- **Supabase** — Auth + Database (app-specific tenants)
- **Stripe** — Payments (per-app)

## Repo

- **GitHub**: https://github.com/SPECTRE888/ops-platform
- **Deploy**: git push → auto-deploy per app via Netlify

## Key Principle

**Monorepo structure**: Each app in `apps/` is independent but shares backend infrastructure.

