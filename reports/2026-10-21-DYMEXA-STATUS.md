# DYMEXA — Cross-repository status reconciliation (2026-10-21)

## Scope and evidence

This is a **snapshot**, not proof of production readiness. It reconciles the frontend's merged Loop 17 evidence, the QA deployment results supplied by the operator, and the backend's canonical product-state documentation. No backend, infrastructure, API contract, or running service was changed as part of this report.

**Naming:** DYMEXA is the approved customer-facing product name. Historical BOSIN/Buzily repository names, protocol identifiers, contract channels, deployment directories and technical codenames are retained until a separately planned migration; do not rename them indiscriminately.

## Verified/reported milestones

| Area | Status | Evidence and limitation |
| --- | --- | --- |
| Frontend stabilization (Overnight UX + Loop 17) | **Merged** | `RayDR/bosin-frontend` PR #66, merge commit `ad7307930f9f6dce02203ab90d13ff30e62ee61e` on `develop`. |
| Frontend CI | **PASS** | GitHub Actions run 39615679289, Quality gates and Production builds/Playwright successful. |
| Frontend local testing | **PASS (reported handoff)** | 699/699 unit/integration; 145/145 Chromium; TypeScript, lint, architectural rules, locale, runtime and builds passed (see frontend validation report). |
| QA frontend deployment | **Deployed / HTTP smoke checked (operator report)** | Active symlink release `20261021T161234Z-ad7307930f9f`; portal 200, public runtime 200, unauthenticated session endpoint 401 (expected). Authenticated workflow acceptance is not established by these HTTP checks alone. |
| Backend implementation | **Documented baseline, not revalidated today** | `RayDR/bosin-backend` `develop` and `docs/product/CURRENT_PRODUCT_STATE.md` (last canonical evidence dated 2026-10-02). Business/session, Customers, Catalog, Inventory, Reservations, Appointments, Quotes, Orders, Invoices and Payments are described as implemented subject to configuration/capability limits. |
| Home direct-manipulation editor | **In progress / not delivered** | Loop 18A is scoped to eliminating the separate `home-customization` panel and enabling true inline drag/resize and contextual add/remove. Loop 17 had an inline draft editor, but current QA screenshots show a separate configuration panel. Do not label Loop 18A accepted until new evidence is available. |
| Business Control Center | **Audit/design or active agent work; not accepted** | Business Settings personalization, permitted login mechanisms, payment configuration UX, module/feature management and adoption analytics are Loop 18B goals; actual backend contracts must be verified. |
| External IdP / SSO expansion | **Architecture proposed; implementation pending** | Google/Amazon/external OIDC linking and Business-managed login policy require approved server-side Identity contracts and threat model. |
| Advanced Home persistence | **Contract-dependent** | Current GET/PUT `/api/business/workspace/preferences` supports principal+Business layout preferences; arbitrary geometry, Business-wide defaults, optimistic concurrency/version preconditions and autosave guarantees need further contracts. |
| Telemetry/analytics and production incident transport | **Planned / contract-dependent** | Do not invent usage events, business analytics, AI recommendations or telemetry transport. |
| Performance | **Known non-blocking warning** | Portal initial raw bundle 842.97 kB vs 650 kB warning budget, +192.97 kB. CommonJS messageformat warning remains; no suppression. |

## Product architecture and boundaries

- **Business Blueprint → capabilities/entitlements → Adaptive Workspace composition → workflows** is the target model, not a claim that all future workspaces are merged.
- Business is the tenant isolation boundary; Branch is operational context and is **not** currently a Branch-scoped authorization boundary.
- A module entitlement, an exact member capability, and a user's workspace/navigation preference are distinct. Frontend preferences cannot grant access.
- Catalog defines products/services/rentals. Inventory applies to physical products/rentals, not services.
- Commercial lifecycle preserves Quotes, Orders, Invoices and Payments as canonical distinct artifacts; direct Order creation must not be represented as shipped without backend evidence.

## Next priorities

1. **Loop 18A / Home:** one dashboard renderer for normal/edit modes; inline drag/drop, size constraints, max 4 user-selected quick actions and max 4 shortcuts, real widget picker, capability-based setup progress and safe server persistence.
2. **Loop 18B / Business Settings:** audit existing Payments/Identity/Branding/Modules contracts before new UI; implement safe business-level personalization, then privacy-aware adoption metrics.
3. **QA acceptance:** authenticated smoke across Home, Settings, Customers, Appointments, module permissions, switching Businesses and persistence; record actual findings before declaring production-ready.
4. **Backend and contracts:** versioned Home layout/concurrency, IdP integration, incident pipeline, business analytics event schema, and any missing settings/payment endpoints need their own authorization.
5. **Naming migration:** plan product-facing rebranding separately from technical protocol and infrastructure compatibility.

## Repository status notes

- `bosin-frontend`: contains authoritative implementation and Loop 17 validation; QA frontend-only release is tracked operationally, not assumed from repository state.
- `bosin-backend`: canonical technical/current-state documentation exists but its source baselines predate this snapshot; no fresh backend verification in this report.
- `buzily-api-specs`: versioned contract registry; changes must be promoted from authoritative service-generated OpenAPI, not edited manually.
- `bosin-demo`: independent static presentation/demo, **not** production implementation.
- `bosin-deploy` and `bosin-brand-assets`: existence observed; contents/operational readiness not verified by this reconciliation.

## Documentation discrepancy

At review time `buzily-product/README.md` describes `roadmap/roadmap.yaml`, `roadmap/ROADMAP.md`, and `product/modules.md`, but the indicated paths could not be fetched from `main`. Treat those advertised sources as **unverified/missing**, not as a synchronized roadmap. Establish or locate the canonical planning model in a separate audited task before assigning percent-complete figures.

## Evidence links

- [PR #66](https://github.com/RayDR/bosin-frontend/pull/66)
- [Frontend validation](https://github.com/RayDR/bosin-frontend/blob/develop/docs/reports/overnight-ux-excellence/04-VALIDATION.md)
- [Frontend handoff](https://github.com/RayDR/bosin-frontend/blob/develop/docs/reports/overnight-ux-excellence/05-FINAL-HANDOFF.md)
- [Home v2 architecture](https://github.com/RayDR/bosin-frontend/blob/develop/docs/architecture/HOME_WORKSPACE_V2.md)
- [Backend current product state](https://github.com/RayDR/bosin-backend/blob/develop/docs/product/CURRENT_PRODUCT_STATE.md)
