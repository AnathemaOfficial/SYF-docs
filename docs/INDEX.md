---
status: updated
version: 1.0
author: AnathemaOfficial
last_updated: 2026-04-15
tags: [documentation, index, navigation]
---

# SYF Documentation Index

**Version:** 1.0  
**Last Updated:** 2026-01-24  
**Status:** Updated

---

## Welcome

This is the central index for all **Systemic Fire Law (SYF)** and **Anathema** documentation.

The documents are organized by topic and numbered for recommended reading order.

---

## Document Structure

```
docs/
├── 1_foundational/           # Core concepts (Start here)
├── 2_security/               # Security model and analysis
├── 3_implementation/         # Implementation guidelines
├── 4_product-and-operational/ # Product specifications
├── 5_legal/                  # Legal documents and boundaries
├── 6_audit-and-status/       # Audit status and verification
├── 7_education/              # Educational materials
└── templates/                # Document templates
```

---

## Reading Order

### For Understanding (Start Here)

1. **[SYF Foundation](1_foundational/syf-foundation.md)** — The problem and solution
2. **[R Invariant](1_foundational/r-invariant.md)** — What R is and isn't
3. **[SYF-Anathema Bridge](1_foundational/syf-anathema-bridge.md)** — From law to body *(stub)*

### For Security Evaluation

4. **[Security Model](2_security/security-model.md)** — Threat model and guarantees
5. **[Comparison with Classic Approaches](2_security/comparison-classic.md)** — SYF vs traditional security *(stub)*
6. **[Why Detection Fails](2_security/why-detection-fails.md)** — Why SYF doesn't detect *(stub)*
7. **[Breaker Q&A](2_security/breaker-qa.md)** — Anathema Breaker questions *(stub)*

### For Implementation

8. **[R Spec Template](3_implementation/r-spec-template.md)** — How to apply R
9. **[R FAQ](3_implementation/r-faq.md)** — Common developer questions *(stub)*
10. **[R Failure Modes](3_implementation/r-failure-modes.md)** — Failure analysis *(stub)*
11. **[SLIME/SAFA Implementation Stack](3_implementation/slime-safa-stack.md)** — Full stack from SLIME-Core to SAFA production adapter

### For Product and Operations

11. **[SYF Gate Product Spec](4_product-and-operational/syf-gate-product-spec_v0.1.md)** — Flagship product *(stub)*
12. **[SYF Shield Product Spec](4_product-and-operational/syf-shield-product-spec_v0.1.md)** — Shield product *(stub)*
13. **[Anathema Breaker Spec](4_product-and-operational/anathema-breaker-spec.md)** — Central organ *(stub)*
14. **[Client Pilot Template](4_product-and-operational/client-pilot-template.md)** — Pilot engagement *(stub)*
15. **[Compliance Checklist](4_product-and-operational/compliance-checklist.md)** — Self-audit tool *(stub)*

### Legal and Boundaries

16. **[Manifest](5_legal/manifest.md)** — Archive manifest
17. **[Boundary of Liability](5_legal/boundary-of-liability.md)** — Liability separation *(reference to PDF)*
18. **[Terms of Non-Use](5_legal/terms-of-non-use.md)** — Forbidden uses *(reference to PDF)*
19. **[Invariants](5_legal/invariants.md)** — Complete invariant list I-1 to I-10 *(reference to PDF)*

### Audit and Status

20. **[Audit Status](6_audit-and-status/audit-status.md)** — Document completion status
21. **[Hashes](6_audit-and-status/hashes.md)** — Cryptographic verification hashes
22. **[Tordeur Audit Report](6_audit-and-status/tordeur-audit-2026-04-15.md)** — Full adversarial security audit results (2026-04-15)

### For Communication

22. **[Anathema Soft Explained](7_education/anathema-soft-explained.md)** — Human explanation for CTOs/Engineers

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

See **[DOCS_CONTRIBUTING.md](DOCS_CONTRIBUTING.md)** for guidelines on contributing to this documentation.

---

## Status Legend

- **SEALED**: Canonical, hash-verified, immutable
- **CANONICAL**: Official but may receive non-substantive updates
- **UPDATED**: Recently modified
- **DRAFT**: Work in progress

---

*For root README and quick links, see [/README.md](../README.md)*
