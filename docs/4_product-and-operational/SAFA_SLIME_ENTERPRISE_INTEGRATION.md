---
status: draft
version: 0.1
author: Codex
last_updated: 2026-03-25
tags: [integration, safa, slime-enterprise, slapy]
---

# SAFA -> SLIME-Enterprise Integration

## Purpose

Define the clean integration model between:

- `SAFA`
- `SLIME-Enterprise`
- and later `SLAPY`

This document exists to prevent architectural confusion between:

- the public core (`SLIME-Core`)
- the appliance layer (`SLIME-Enterprise`)
- the agent adapter (`SAFA`)
- the product layer (`SLAPY`)

---

## Target Chain

The target execution chain is:

```text
SLAPY -> SAFA -> SLIME-Enterprise -> actuator -> system effect
```

The authority chain is:

```text
SLIME-Core -> defines and proves
SLIME-Enterprise -> packages and executes
SAFA -> adapts agent requests
SLAPY -> exposes workflow and UX
```

---

## Responsibility Split

### SLIME-Core

Responsible for:

- canon
- law-layer proof
- bounded public compatibility surface

Not responsible for:

- appliance packaging
- agent adaptation
- product UX

### SLIME-Enterprise

Responsible for:

- hardened execution appliance
- actuator path
- boot integrity
- release packaging

Not responsible for:

- agent request parsing
- product semantics
- user workflow

### SAFA

Responsible for:

- request validation
- canonicalization
- domain mapping
- identity binding
- proof / policy surfaces

Not responsible for:

- product UX
- direct human workflow
- appliance packaging details

### SLAPY

Responsible for:

- user workflow
- product surfaces
- orchestration
- visibility

Not responsible for:

- law execution
- actuator integrity
- proof kernel design

---

## Integration Principle

`SAFA` should not target `SLIME-Core` as if it were the final runtime appliance.

Instead:

- `SLIME-Core` remains the proof and canon lineage
- `SLIME-Enterprise` becomes the real execution appliance
- `SAFA` becomes the universal adapter above it

This allows:

- public proof to remain bounded and honest
- real execution to be hardened separately
- product systems like `SLAPY` to consume one stable adapter contract

---

## Hello World Integration Path

### Step 1

Install and validate `SLIME-Enterprise Hello World`.

Proof:

- appliance boots
- runner emits
- actuator logs

### Step 2

Install and validate `SAFA Hello World`.

Proof:

- manifest works
- one allowed action works
- one denied action works
- proof surface visible

### Step 3

Bind `SAFA` to the `SLIME-Enterprise` execution path.

Proof:

- a SAFA-authorized action reaches the appliance path
- the appliance performs the effect
- the chain remains fail-closed

---

## Why This Matters For SLAPY

This is the reason `SLAPY` should consume `SAFA`.

`SLAPY` should not:

- talk directly to an actuator
- embed execution-law logic
- act as a policy kernel

Instead:

- `SLAPY` requests a bounded action
- `SAFA` validates and proves
- `SLIME-Enterprise` executes within the appliance envelope

This keeps the product layer clean.

---

## Package Sequence

Recommended sequence:

1. `SLIME-Enterprise Hello World`
2. `SAFA Hello World`
3. `SAFA -> SLIME-Enterprise` integration bundle
4. later: `SLAPY` consuming `SAFA`

This order is safer than wiring `SLAPY` first and forcing the lower layers to
stabilize afterward.

---

## Final Recommendation

Treat `SAFA` as the universal agent adapter.

Treat `SLIME-Enterprise` as the real execution appliance.

Treat `SLIME-Core` as the proof/canon base.

Then `SLAPY` can sit on top without inheriting execution ambiguity.

