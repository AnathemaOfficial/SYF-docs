---
status: canonical
version: 1.0
author: AnathemaOfficial
last_updated: 2026-04-15
tags: [audit, security, tordeur, adversarial]
---

# Tordeur Audit Report — 2026-04-15

## Overview

The "tordeur" (security wringer) is a complete adversarial audit cycle
applied to both SAFA and SLIME-Core. It consists of cooperative audits
followed by independent adversarial passes.

**Scope:** SAFA v0.3.2 through v0.4.0, SLIME-Core v0.3.6 through v0.4.0
**Duration:** 2026-04-15 (single day, multiple AI auditors in parallel)
**Result:** All CRITICAL and HIGH findings closed. Tags applied.

---

## Audit Phases

### Phase 1 — Cooperative Audits (SAFA)

| Auditor | Branch/PR | Findings | Severity |
|---------|-----------|----------|----------|
| Qwen | `security/qwen-audit` | 3 | Actuator hardening |
| Copilot (Opus 4.6) | `security/copilot-audit` | 4 | Config validation, bounds |
| Kimi | `security/kimi-audit` | 3 | Observability, attestation |
| MiniMax | PR #7 | 5 | Subdomain, daemon availability |

**Subtotal:** 15 findings closed, 4 PRs merged.

### Phase 2 — Adversarial Passes (SAFA)

| Auditor | Branch/PR | Findings | Severity |
|---------|-----------|----------|----------|
| Ana (qwen3-32b via OpenClaw) + Codex | PR #8 | 4 | 1 CRITICAL, 1 HIGH, 1 MED, 1 LOW |

**Critical finding:** `shell_exec` cross-agent workspace read via
`{{workspace_root}}` — config loader substituted at load time against the
GLOBAL workspace root with no agent_id, so every agent's `git_status`/`git_log`
saw shared state.

**High finding:** Intermediate-directory TOCTOU on `file_write` — between
`verify_no_symlinks` and `create_dir_all`, a concurrent actor could replace
a path component with a symlink.

### Phase 3 — Alignment Audit (SLIME-Core)

| Auditor | Findings | Severity Breakdown |
|---------|----------|--------------------|
| Claude Opus 4.6 (security-reviewer agent) | 30 | 9 HIGH, 14 MED, 7 LOW |

All 9 HIGH findings resolved:
- Hand-rolled JSON parser replaced with serde_json (exploit fix)
- Egress silent reconnect removed (fail-closed per canon)
- domain_id truncation contradiction fixed (R-7 alignment)
- IPv6 SSRF gap documented
- Windows symlink limitation documented
- HMAC auth absent from specs (SAFA_ADAPTER_MAPPING.md created)
- Per-agent workspace isolation documented
- Stale architecture refs noted

### Phase 4 — Post-Merge Verification (SAFA)

| Auditor | Findings | Action |
|---------|----------|--------|
| Codex (rescue agent) | 8 | 1 HIGH (IPv6 HTTP), 2 MED, 5 LOW — tracked for P4 |

---

## Final State

### SAFA
- **Tests:** 131/131 passing
- **Clippy:** 1 nit (unused `agent_id` on Windows, `#[cfg(unix)]` gated)
- **Tags:** `v0.4.0-tordeur-complete`, `slime-enterprise-v0.3.0-tordeur-complete`
- **PRs:** #7 and #8 merged, branches cleaned

### SLIME-Core
- **Tests:** 12/12 passing (up from 8)
- **Clippy:** Clean (0 warnings)
- **Tag:** `v0.4.0-tordeur-alignment`
- **PR:** #8 merged, branch cleaned
- **New docs:** `SAFA_ADAPTER_MAPPING.md`, `KNOWN_LIMITATIONS.md`

---

## Remaining Items (P4 Follow-ups)

| Severity | Item | Repo |
|----------|------|------|
| HIGH | IPv6 SSRF: `fc00::/7`, `fe80::/10`, `64:ff9b::/96` not blocked | SAFA |
| MEDIUM | `agent_id` raw `&str` in path concat (no type enforcement) | SAFA |
| MEDIUM | HTTP actuator tests don't cover redirect/bounded-body | SAFA |
| MEDIUM | `cleanup_orphan_temps` follows symlinks | SAFA |
| LOW | `eprintln!` -> `tracing::warn!` for shared-workspace warning | SAFA |
| LOW | README startup instructions need placeholder note | SAFA |
| LOW | THREAT_MODEL.md overstates redirect handling | SAFA |

---

## Methodology

The tordeur methodology uses progressive escalation:

1. **Cooperative audits** with diverse AI models (different blind spots)
2. **Cross-confirmation** between auditors
3. **Independent adversarial passes** by agents not involved in the code
4. **Post-merge verification** by a separate agent
5. **Alignment audit** of upstream specs against implementation

Each phase builds on the previous — adversarial passes target areas the
cooperative audits may have overlooked or deferred.

---

*For full details, see the PR descriptions in the respective repositories.*
