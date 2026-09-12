# Buzily Product

Canonical product-planning repository for Buzily.

This repository is intended to track the product roadmap across backend, frontend, integration, QA, release readiness, and future product modules without coupling product planning to a single implementation repository.

## Source of truth

The roadmap model is organized as:

`Release -> Milestone -> Track -> Deliverable`

Tracks:

- `BE` — backend
- `FE` — frontend
- `INT` — end-to-end integration
- `QA` — release/security/testing
- `PRODUCT` — product/UX/planning prerequisites

Status symbols used in human-facing reports:

- ✅ complete / accepted
- 🔄 in progress
- ⚠️ partial
- ⬜ not started
- ⛔ blocked
- ➕ stretch / delivered ahead of committed scope

A deliverable is only considered complete after its acceptance evidence is available. Code existing by itself is not sufficient.

## Repository layout

```text
roadmap/
  roadmap.yaml           # canonical structured roadmap
  ROADMAP.md             # human-readable roadmap
  releases/              # release-specific definitions
product/
  modules.md             # product/module registry
  concepts/              # future product concepts
reports/
  README.md               # reporting policy
  templates/             # collaborator/client report templates
docs/
  roadmap-governance.md   # update and acceptance rules
```

Client-specific readiness, pricing strategy, internal commercial plans, and other confidential material must only be added when this repository is private.

## Update rule

Every meaningful backend/frontend acceptance should produce a `ROADMAP UPDATE` block identifying:

- release
- milestone
- area/track
- deliverable
- status
- progress
- acceptance evidence
- remaining work
- client/product impact where applicable

The canonical roadmap is then updated from that evidence.
