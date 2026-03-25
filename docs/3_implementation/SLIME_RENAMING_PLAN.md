---
status: draft
version: 0.1
author: Codex
last_updated: 2026-03-25
tags: [naming, slime, core, enterprise, migration]
---

# SLIME Renaming Plan

## Purpose

This document defines the target naming model for the `SLIME` family and the
safe migration order needed to remove architectural ambiguity without breaking
the current ecosystem.

The core problem is simple:

> `SLIME` currently names both the public canon/core layer and, by implication,
> the appliance execution layer that actually belongs to `SLIME-Enterprise`.

This ambiguity contaminates documentation, integration language, and product
planning downstream.

---

## Target Naming

The target names should be:

- `SLIME-Core`
- `SLIME-Enterprise`
- `SAFA`
- `SLAPY`

## Role of Each Layer

### SLIME-Core

`SLIME-Core` is the public law/core layer.

It contains:

- canonical specs
- public proof surface
- bounded public runner surface
- compatibility proof material

It is **not** the hardened appliance.

### SLIME-Enterprise

`SLIME-Enterprise` is the hardened appliance layer.

It contains:

- bundled runner binary
- bundled actuator
- systemd packaging
- FirePlank boot integrity
- release bundle
- optional read-only dashboard

It is the execution appliance, not the public canon.

### SAFA

`SAFA` is the agent-facing adapter.

It provides:

- validation
- canonicalization
- domain mapping
- identity binding
- policy/proof surfaces

It is not the law-layer itself.

### SLAPY

`SLAPY` is the product layer.

It provides:

- UX
- workflow
- orchestration

It should consume `SAFA`, not target the execution layer directly.

---

## Canonical Chain

The target execution chain is:

```text
SLAPY -> SAFA -> SLIME-Enterprise -> actuator -> system effect
```

The target authority chain is:

```text
SLIME-Core -> defines and proves
SLIME-Enterprise -> packages and executes
SAFA -> adapts agent requests
SLAPY -> exposes product workflow
```

---

## Vocabulary Rules

These rules should be applied everywhere after this plan is adopted.

### Rule 1

Use `SLIME-Core` when referring to:

- the public canon
- the public core repo
- the public runner baseline
- bounded compatibility proof

### Rule 2

Use `SLIME-Enterprise` when referring to:

- the hardened appliance
- the actuator package
- systemd packaging
- release bundles
- FirePlank-Guard appliance runtime

### Rule 3

Do not use plain `SLIME` by itself in architecture-critical documentation,
unless the text explicitly says:

> `SLIME` (legacy name; being renamed to `SLIME-Core`)

### Rule 4

Use `SAFA` as the product-facing action contract for agent systems.

### Rule 5

Use `SLIME-Core` for public proof and canon discussion.
Use `SLIME-Enterprise` for real appliance execution discussion.

---

## Impact Surface

The rename affects four types of material.

### 1. Public Core Documentation

Affected surfaces:

- `SLIME` root README
- `CANON.md`
- `CORE_SCOPE.md`
- `CONFORMANCE.md`
- public implementation bundle docs

Required change:

- explain that the current repo is the public core and should be read as
  `SLIME-Core`

### 2. Enterprise Appliance Documentation

Affected surfaces:

- `SLIME-Enterprise` README
- install docs
- FAQ
- architecture docs
- release notes

Required change:

- replace generic references to `SLIME` with explicit references to
  `SLIME-Core` where canon/proof is meant

### 3. SAFA Documentation

Affected surfaces:

- root README
- architecture docs
- integration notes
- future packaging docs

Required change:

- distinguish:
  - `SLIME-Core` for law/proof lineage
  - `SLIME-Enterprise` for ready-to-ship execution chain

### 4. Product / UX Documentation

Affected surfaces:

- `SLAPY` docs
- substrate notes
- future product integration docs

Required change:

- make `SAFA` the immediate contract
- make `SLIME-Enterprise` the eventual execution appliance
- stop using plain `SLIME` as a floating integration target

---

## Migration Order

The rename should happen in four phases.

### Phase A - Semantic Clarification

Do not rename folders or repos yet.

First:

- update docs to say `SLIME` is being clarified as `SLIME-Core`
- align downstream architecture language
- stop writing new ambiguous references

This phase is the least risky and should happen first.

### Phase B - Canonical Naming Freeze

Formally declare the target names in architecture notes and cross-repo docs.

Deliverables:

- this plan
- updates in `SLIME`
- updates in `SLIME-Enterprise`
- updates in `SAFA`

After this phase, ambiguity should already be reduced even before physical rename.

### Phase C - Physical Rename

Only after the docs and integration language are stable:

- rename repo/folder `SLIME` -> `SLIME-Core`
- update Git remotes, badges, URLs, archive paths, and release text

This phase should be mechanical, not conceptual.

### Phase D - Downstream Resealing

After the physical rename:

- `SLIME-Enterprise` docs point to `SLIME-Core`
- `SAFA` distinguishes proof lineage from appliance execution
- `SLAPY` integration docs point to `SAFA -> SLIME-Enterprise`

---

## Safe Default During Transition

Until the physical rename is done, the safe wording is:

> `SLIME` (public core, to be renamed `SLIME-Core`)

and

> `SLIME-Enterprise` (hardened appliance layer)

This wording is preferred over using plain `SLIME` without qualification.

---

## Final Recommendation

Do not start with the physical repo rename.

Start with:

1. semantic rename in docs
2. architecture chain clarification
3. downstream vocabulary freeze
4. only then physical rename

That order minimizes breakage and maximizes clarity.

