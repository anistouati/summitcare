# SummitCare Delivery Roadmap

Status values: `TODO`, `IN_PROGRESS`, `BLOCKED`, `DONE`.

## P0 — Platform workspace and quality gate

### SC-001 — Create application workspace — TODO
**Goal:** preserve the root landing page and create `platform/` for product code.

Acceptance criteria:
- `index.html` remains deployable as the public landing page.
- `platform/api` contains ASP.NET Core modular-monolith solution skeleton.
- `platform/web` contains Angular 18 standalone application skeleton.
- PostgreSQL is available through Docker Compose.
- Health checks and local bootstrap instructions exist.

### SC-002 — CI quality gate — TODO
**Depends on:** SC-001

Acceptance criteria:
- Backend restore/build/test on pull requests.
- Frontend install/test/build on pull requests.
- No production secrets required by CI.

## P0 — Identity and role scope

### SC-010 — Role-based identity boundary — TODO
**Depends on:** SC-001

Acceptance criteria:
- Roles Admin, ClinicAdmin, Provider, Family are modeled.
- Authorization policies are centralized.
- Tests prove users cannot access another role/tenant scope improperly.

### SC-011 — Provider, clinic and family core aggregates — TODO
**Depends on:** SC-010

Acceptance criteria:
- Provider, Clinic, Family/Household aggregates exist.
- Provider can carry multiple independent clinic verifications.
- Family referral attribution points to one clinic.
- Audit fields exist for attribution/verification changes.

## P0 — Pilot workflows

### SC-020 — Provider onboarding and verification — TODO
**Depends on:** SC-011

Acceptance criteria:
- Provider profile, service areas, services, documents/certifications and availability can be maintained.
- ClinicAdmin can verify/revoke verification for a provider without affecting other clinic verifications.
- Family-facing trust signals expose only approved information.

### SC-021 — Family onboarding and clinic attribution — TODO
**Depends on:** SC-011

Acceptance criteria:
- Family/household profile supports senior/service-recipient context and addresses.
- Referral clinic attribution is explicit and immutable except through audited administrative correction.
- Family opt-in/consent is recorded for relevant communication/referral use.

### SC-022 — Provider discovery and matching — TODO
**Depends on:** SC-020, SC-021

Acceptance criteria:
- Families can search/filter providers by service, geography, availability and verification.
- Matching boost is explainable and deterministic.
- No hidden ranking based on protected/sensitive attributes.

### SC-023 — Booking lifecycle — TODO
**Depends on:** SC-022

Acceptance criteria:
- Request/confirm/cancel/complete lifecycle exists.
- Availability conflicts are prevented transactionally.
- Role permissions and audit trail are tested.

## P1 — Revenue and operations

### SC-030 — Clinic referral commission ledger — TODO
**Depends on:** SC-021, SC-023

Acceptance criteria:
- Eligible completed bookings generate clinic commission attribution based on the family referral clinic.
- Calculation is deterministic/idempotent.
- Corrections are auditable; history is not overwritten.

### SC-031 — Provider payout reporting — TODO
**Depends on:** SC-023

Acceptance criteria:
- Provider can view gross bookings, fees, adjustments and expected payout.
- Admin can reconcile payout-ready amounts.
- No autonomous payout execution in this milestone.

### SC-032 — Email notification transport — TODO
**Depends on:** SC-023

Acceptance criteria:
- Notification abstraction supports dev and production transports.
- Booking/referral lifecycle messages are idempotent and localized.

### SC-033 — Admin/clinic analytics — TODO
**Depends on:** SC-030

Acceptance criteria:
- Clinic dashboard shows referred families, bookings and commission metrics within authorized scope.
- Admin dashboard shows platform pilot KPIs and exceptions.

## P1 — Pilot hardening

### SC-040 — End-to-end critical-path tests — TODO
Cover provider onboarding -> clinic verification -> family attribution -> discovery -> booking -> completion -> commission ledger.

### SC-041 — Security/privacy hardening — TODO
Threat-model identity, document uploads, PII, role scope and payment/commission data; add tests and operational controls.

### SC-042 — Pilot observability — TODO
Structured logging, health checks, traces/metrics for booking failures, notification failures and authorization anomalies.

## P2 — Post-pilot
- Payment processor/payout execution.
- Messaging/real-time communication.
- Advanced matching.
- Multi-market expansion.
- External clinic integrations.

## Explicitly out of scope before pilot hardening
- Microservice decomposition.
- Medical diagnosis/treatment functionality.
- Autonomous clinical or financial decisions.
- Broad marketplace expansion before Montreal pilot workflows are reliable.
