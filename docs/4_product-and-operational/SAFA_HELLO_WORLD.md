---
status: draft
version: 0.1
author: Codex
last_updated: 2026-03-25
tags: [safa, hello-world, agent-adapter, packaging]
---

# SAFA Hello World

## Purpose

Define the smallest package that proves `SAFA` works as an
agent-facing constrained action adapter.

This package should prove:

- request validation
- canonicalization
- domain mapping
- authorization surface
- proof visibility
- bounded actuation

without pretending to be a full product integration.

---

## Goal

A local operator should be able to:

1. start `safa-daemon`
2. inspect a manifest
3. submit one allowed action
4. submit one denied action
5. inspect proof output
6. confirm the effect happened only in the allowed case

---

## Hello World Scenario

### Allowed action

- route: `POST /ama/action`
- action: `file_write`
- target: `hello.txt`
- payload: `hello from safa`
- magnitude: `1`

Expected:

- response status corresponds to `authorized`
- file appears in the bounded workspace
- policy hash is present
- proof record can be fetched

### Denied action

- route: `POST /ama/action`
- action: `file_write`
- target: `../escape.txt` or an otherwise invalid bounded target

Expected:

- response indicates `impossible`
- no effect occurs
- proof/journal still records the verdict

---

## Package Contents

The package should contain:

- `safa-daemon`
- minimal `config.toml`
- minimal `domains.toml`
- minimal `allowlist.toml`
- minimal `intents.toml`
- one dedicated hello-world agent config
- start script
- quick validation script
- README / quickstart

Recommended demo agent:

- `hello-world`

Avoid using:

- `developer`

for the package demo surface.

---

## Minimal Agent Contract

The demo agent should be narrowly bounded:

- `file_read`
- `file_write`

Optional:

- `http_request` for an allowlisted probe

Avoid in Hello World:

- broad shell execution
- large capacities
- broad networking

---

## Validation Contract

### Manifest

```bash
curl http://127.0.0.1:8787/ama/manifest/hello-world
```

Expected:

- manifest exists
- policy hash exists
- exposed domains match the package

### Authorized write

```bash
curl -X POST http://127.0.0.1:8787/ama/action \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: <uuid>" \
  -H "X-Agent-Id: hello-world" \
  -d '{"adapter":"hello-world","action":"file_write","target":"hello.txt","magnitude":1,"payload":"hello from safa"}'
```

Expected:

- bounded authorization
- file written
- proof-visible metadata

### Denied write

```bash
curl -X POST http://127.0.0.1:8787/ama/action \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: <uuid>" \
  -H "X-Agent-Id: hello-world" \
  -d '{"adapter":"hello-world","action":"file_write","target":"../escape.txt","magnitude":1,"payload":"nope"}'
```

Expected:

- denial / impossibility
- no file written outside workspace

---

## Release Acceptance Criteria

`SAFA Hello World` is accepted only if:

1. `cargo test --workspace` is green
2. manifest route works
3. one allowed action works
4. one denied action works
5. proof surface is visible
6. package uses a dedicated demo agent, not a broad developer profile

---

## Future Extension Boundary

This package proves the adapter surface.
It does not yet prove:

- full appliance chaining into `SLIME-Enterprise`
- rich product integration
- broad agent capability sets

