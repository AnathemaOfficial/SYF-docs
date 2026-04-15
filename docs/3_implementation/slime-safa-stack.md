---
status: canonical
version: 1.0
author: AnathemaOfficial
last_updated: 2026-04-15
tags: [implementation, slime, safa, architecture, stack]
---

# Implementation Stack — SLIME-Core to SAFA

## Overview

The SYF enforcement architecture is implemented as a layered stack,
from formal specification down to production deployment.

```
SYF-Core          Mathematical invariants (R = (F x E) / K)
    |
SYF-Gate          Admission verdict (ALLOW / DENY)
    |
SYF-Shield        Irreversible capacity consumption (EP coupling)
    |                      \
    |                       --> Compiled into:
    |                      /
SLIME-Core        Formal specification (this is the "engine blueprint")
    |
SLIME-Enterprise  Enterprise deployment layer (systemd, dashboard)
    |
SAFA              Production adapter for multi-agent containment
```

---

## Layer Descriptions

### SLIME-Core (Specification)

**Repo:** [github.com/AnathemaOfficial/SLIME-Core](https://github.com/AnathemaOfficial/SLIME-Core)
**Latest tag:** `v0.4.0-tordeur-alignment` (2026-04-15)

SLIME-Core is the formal specification defining:
- The binary enforcement membrane (AUTHORIZED / IMPOSSIBLE)
- The 32-byte egress ABI (`u64 domain_id` + `u64 magnitude` + `u128 actuation_token`)
- Ingress API contract (`POST /action`, JSON schema)
- Egress socket contract (`/run/slime/egress.sock`, SOCK_STREAM)
- V1 invariants (zero runtime configuration, compile-time law, statelessness)
- Formal core model (`A -> E U {empty}` under invariant `I`)

SLIME-Core also contains:
- A reference runner (`noncanon/implementation_bundle/slime-runner`, Rust, v0.4.0)
- Conformance matrix documenting intentional divergences
- SAFA adapter mapping (`SAFA_ADAPTER_MAPPING.md`)
- Known limitations (`KNOWN_LIMITATIONS.md`)

### SLIME-Enterprise (Deployment)

**Repo:** Private (AnathemaOfficial/SLIME-Enterprise)
**Latest tag:** `slime-enterprise-v0.3.0-tordeur-complete` (2026-04-15)

Enterprise deployment layer adding:
- systemd service definitions
- Dashboard (read-only observation, port 8081)
- Production egress socket management
- Actuator bridge integration

### SAFA (Production Adapter)

**Repo:** [github.com/AnathemaOfficial/SAFA](https://github.com/AnathemaOfficial/SAFA)
**Latest tag:** `v0.4.0-tordeur-complete` (2026-04-15)

SAFA extends the SLIME model for multi-agent environments:
- **P3 Agent Containment:** Per-agent workspace isolation, filesystem sandboxing
- **HMAC Authentication:** `X-Agent-Id` + `X-Agent-Timestamp` + `X-Agent-Signature`
- **4 Actuators:** `file_read`, `file_write`, `shell_exec` (Unix), `http_request`
- **Policy Attestation:** `X-Safa-Policy-Hash` header on every response
- **Concurrency Control:** 8 simultaneous request limit
- **Idempotency:** UUID v4 `Idempotency-Key` required per action

SAFA's endpoints use the `/ama/` prefix (historical, from its original name
"Agent Machine Armor").

---

## Security Audit Status (Tordeur, 2026-04-15)

Both SLIME-Core and SAFA completed a full adversarial audit cycle:

| Phase | Auditor | Findings Closed |
|-------|---------|-----------------|
| Cooperative | Qwen | 3 actuator findings |
| Cooperative | Copilot (Opus 4.6) | 4 findings |
| Cooperative | Kimi | 3 findings + observability hardening |
| Cooperative | MiniMax | 5 findings |
| Adversarial | Ana (qwen3-32b) + Codex | 4 findings (1 CRITICAL) |
| Alignment | Claude Opus 4.6 | SLIME-Core: 9 HIGH, 14 MED, 7 LOW |

**Total:** 28+ findings closed across both repos.

### Critical Fix (SAFA)

`shell_exec` intents with `working_dir = "{{workspace_root}}"` were
resolved at config-load time against the GLOBAL workspace root. Every
agent running `git_status`/`git_log` saw the same shared state —
cross-agent information disclosure. Fixed by introducing
`{{agent_workspace}}` resolved at runtime per agent.

### Critical Fix (SLIME-Core Runner)

The hand-rolled JSON parser in `slime-runner` was exploitable: a crafted
`payload` field containing `"domain":"deploy"` could hijack domain
extraction. Replaced with `serde_json`.

---

## Known Limitations

See `KNOWN_LIMITATIONS.md` in SLIME-Core repo for the full list. Key items:

| ID | Limitation |
|----|-----------|
| P-01 | `verify_no_symlinks` is a no-op on Windows |
| P-02 | `shell_exec` requires Unix (`#[cfg(unix)]`) |
| N-01 | IPv6 ULA (`fc00::/7`) not classified as private in HTTP actuator |
| N-02 | IPv6 link-local (`fe80::/10`) not classified as private |
| S-01 | slime-runner is single-threaded (use SAFA for production) |

---

## Cross-References

| Document | Location |
|----------|----------|
| SLIME formal spec | SLIME-Core: `SLIME_FORMAL_CORE.md` |
| Ingress API spec | SLIME-Core: `specs/INGRESS_API_SPEC.md` |
| Egress socket spec | SLIME-Core: `specs/EGRESS_SOCKET_SPEC.md` |
| V1 invariants | SLIME-Core: `specs/V1_INVARIANTS.md` |
| Full-stack conformance | SLIME-Core: `FULL_STACK_CONFORMANCE.md` |
| Security model | SLIME-Core: `ARCHITECTURE_SECURITY_MODEL.md` |
| SAFA adapter mapping | SLIME-Core: `SAFA_ADAPTER_MAPPING.md` |
| SAFA P3 scope | SAFA: `docs/P3_SCOPE.md` |
| SAFA threat model | SAFA: `docs/THREAT_MODEL.md` |

---

*This document is part of the SYF documentation. See [INDEX.md](../INDEX.md) for navigation.*
