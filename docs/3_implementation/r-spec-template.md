---
status: canonical
version: 1.0
author: AnathemaOfficial
last_updated: 2026-01-24
tags: [implementation, r-spec, engineering]
---

# R-Spec Template

## How to Apply R in Your System

**Status:** CANONICAL — REQUIRED for any SYF-compliant integration.

---

## 1. Purpose

This document defines how a system projects the invariant R into concrete action limits.

- **R is provided by SYF.**
- **This spec defines how your system reacts to it.**

> ⚠️ R itself MUST NOT be modified, stored, smoothed, averaged, or overridden.

---

## 2. Scope

This R-Spec applies to:

| Field | Value |
|-------|-------|
| System | `<SYSTEM_NAME>` |
| Environment | `<ENVIRONMENT>` |
| Risk domain | `<DOMAIN>` |

---

## 3. Points of Effect (REQUIRED)

List only irreversible or high-impact actions.

**Example:**
```
- write_prod_db
- deploy_prod
- external_payment
- robot_motion
```

> ⚠️ R MUST NOT be applied inside business logic or cognition.  
> ⚠️ R MUST be enforced at the point of effect.

---

## 4. Action Units

Define what counts as one unit of action.

**Example:**
```
write_prod_db = 1 unit
deploy_prod   = 3 units
```

**Rules:**
- Units MUST be concrete and measurable
- Units MAY differ per action
- Units MUST NOT depend on intent or identity

---

## 5. Budget Derivation

Define how R is projected into a short-lived budget.

**Example:**
```
Window (TTL): 5 seconds
Budget = floor(R / K)
K = 10
```

**Rules:**
- Budget MUST be derived from current R only
- No accumulation
- No historical carryover

---

## 6. Enforcement Rule

```
IF budget < cost(action):
    DENY (fail-closed)
```

**Optional behaviors:**
- throttle
- delay
- split action

**Default:** DENY

---

## 7. Forbidden Operations (NON-NEGOTIABLE)

This spec MUST NOT:
- ❌ modify R
- ❌ store R
- ❌ average R
- ❌ smooth R
- ❌ override R
- ❌ react to R with control logic

**Violation = OUT OF SYF SCOPE**

---

## 8. Compliance Statement

> This system applies R strictly as a read-only sensor and enforces action limits 
> at the point of effect, in compliance with SYF invariants.

---

# R-Spec Template (Copy-Paste)

```markdown
# R-Spec: <SYSTEM_NAME>

## Scope
- System: 
- Environment: 
- Domain: 

## Points of Effect
- action_1
- action_2
- action_3

## Action Units
| Action | Cost |
|--------|------|
| action_1 | 1 |
| action_2 | 2 |

## Budget Derivation
- TTL: X seconds
- Formula: budget = floor(R / K)
- K = 

## Enforcement
- Default: DENY
- Optional: [throttle | delay | split]

## Compliance
This spec complies with SYF invariants.
R is read-only and never modified.
```
