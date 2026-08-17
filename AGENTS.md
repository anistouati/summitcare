# SummitCare — Codex Engineering Instructions

## Mission
Build SummitCare as a premium Montreal-first non-medical support marketplace connecting families, verified providers and referring clinics.

## Repository safety
- `index.html` is the existing public landing page. Preserve it unless a roadmap item explicitly changes marketing content.
- Product application code belongs under `platform/` so GitHub Pages/landing behavior is not disrupted.

## Target architecture
- ASP.NET Core modular monolith (.NET 9 compatible) with clear Domain/Application/Infrastructure/Api boundaries.
- Angular 18 standalone frontend.
- PostgreSQL + EF Core migrations.
- Docker Compose for local dependencies.
- Roles: Admin, ClinicAdmin, Provider, Family.

## Non-negotiable domain rules
- Providers may be verified by multiple clinics.
- A family referral attribution belongs to one clinic for commission attribution unless a future explicit business rule changes it.
- Clinic commission follows the referred family across eligible bookings.
- Role-scoped data access must not leak cross-clinic or cross-family data.
- This is non-medical support; do not add clinical diagnosis/treatment behavior.

## Engineering rules
- Keep business rules deterministic and tested.
- No payment movement without explicit user/system authorization and idempotency.
- No secrets in source control.
- Schema changes use EF Core migrations.
- Prefer modular monolith boundaries over microservices.
- Reuse existing patterns before introducing new dependencies.
- Accessibility and EN/FR readiness are required for user-facing work.

## Agent workflow
1. Read `ROADMAP.md`; select first unblocked P0/P1 item.
2. Use architecture/security subagents before cross-cutting identity, attribution, payout or authorization changes.
3. Assign backend/frontend workers to non-overlapping files.
4. QA verifies acceptance criteria and role isolation before completion.
5. Update roadmap status only after checks pass.

## Definition of done
- Acceptance criteria met.
- Tests/build pass for touched layers.
- Authorization and role scope verified.
- Migrations included where needed.
- EN/FR/accessibility implications addressed.
- No regression to landing page deployment.
