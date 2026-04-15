# SYF Documentation

**Version:** 1.1  
**Status:** Updated  
**Last Updated:** 2026-04-15

---

## Overview

This repository contains the canonical documentation for the **Systemic Fire Law (SYF)**, 
**Anathema**, and related security architecture.

**📚 Complete Documentation Index:** [docs/INDEX.md](docs/INDEX.md)

---

## Quick Navigation

All documentation has been reorganized into the `docs/` directory for better structure and navigation.

### Core Documentation Sections

- **[1_foundational/](docs/1_foundational/)** — Core concepts and principles
- **[2_security/](docs/2_security/)** — Security model and analysis
- **[3_implementation/](docs/3_implementation/)** — Implementation guidelines
- **[4_product-and-operational/](docs/4_product-and-operational/)** — Product specifications
- **[5_legal/](docs/5_legal/)** — Legal documents and boundaries
- **[6_audit-and-status/](docs/6_audit-and-status/)** — Audit status and verification
- **[7_education/](docs/7_education/)** — Educational materials

---

## Quick Start

### New to SYF?

Start with the foundational documents:

1. [SYF Foundation](docs/1_foundational/syf-foundation.md) — The problem and solution
2. [R Invariant](docs/1_foundational/r-invariant.md) — What R is and isn't
3. [Security Model](docs/2_security/security-model.md) — Threat model and guarantees

### For Implementation

See the implementation section:

- [R Spec Template](docs/3_implementation/r-spec-template.md) — How to apply R
- [SLIME/SAFA Stack](docs/3_implementation/slime-safa-stack.md) — Full implementation stack (SLIME-Core to SAFA)
- [Implementation section](docs/3_implementation/) — All implementation guides

### For Security Audit

- [Tordeur Audit Report](docs/6_audit-and-status/tordeur-audit-2026-04-15.md) — Full adversarial audit (2026-04-15)

### For Communication

- [Anathema Soft Explained](docs/7_education/anathema-soft-explained.md) — Human explanation for CTOs/Engineers

---

## Core Principles (Summary)

| Principle | Description |
|-----------|-------------|
| **Safety by Impossibility** | Actions are limited, not monitored |
| **R is a Sensor** | Read-only, non-accumulative, present-only |
| **Fail-Closed** | Unknown state → no action |
| **No Detection** | Assumes breach, limits damage |
| **No Governance** | No admin, no override, no bypass |

---

## Canonical Statement

> **SYF does not try to stop attackers from entering.**  
> **It makes damage physically impossible, even if they are already inside.**

---

## Contributing

See [docs/DOCS_CONTRIBUTING.md](docs/DOCS_CONTRIBUTING.md) for contribution guidelines and sealing policy.

---

## Document Status

- **SEALED**: Canonical, hash-verified, immutable (PDFs with hashes)
- **CANONICAL**: Official reference documents
- **UPDATED**: Recently modified
- **DRAFT**: Work in progress

See [docs/6_audit-and-status/audit-status.md](docs/6_audit-and-status/audit-status.md) for complete audit status.

---

*For detailed navigation and reading order, see [docs/INDEX.md](docs/INDEX.md)*
