---
status: draft
version: 0.1
author: Codex
last_updated: 2026-03-25
tags: [slime-enterprise, hello-world, appliance, packaging]
---

# SLIME-Enterprise Hello World

## Purpose

Define the smallest appliance package that proves `SLIME-Enterprise` is:

- installable
- fail-closed
- observable
- reproducible

without adding product complexity.

This is not a demo of business semantics.
It is a demo of the appliance chain itself.

---

## Goal

A clean Linux host should be able to:

1. install the appliance
2. boot `actuator.service` and `slime.service`
3. send one minimal authorized action
4. observe one actuator event
5. confirm reboot stability
6. uninstall cleanly

---

## Hello World Scenario

### Action

- domain: `test`
- magnitude: `1`

### Expected outcome

- runner returns `AUTHORIZED`
- a 32-byte frame is emitted
- `actuator-min` logs one hex frame
- dashboard, if installed, shows the event as observation only

### Explicit non-goals

- no product semantics
- no dynamic config
- no variable payload protocol
- no bidirectional channel
- no agent layer

---

## Package Contents

The package must contain:

- `slime-runner`
- `actuator-min`
- `fireplank-guard-boot.sh`
- `generate-seal.sh`
- `actuator.service`
- `slime.service`
- `fp4-hardening-actuator.conf`
- `fp4-hardening-slime.conf`
- `install.sh`
- `uninstall.sh`
- `SHA256SUMS`

Optional:

- dashboard assets
- `slime-dashboard.service`

---

## Install Contract

### Inputs

- Linux host
- systemd
- sudo
- appliance bundle or repo checkout

### Outputs

- binaries installed under `/usr/local/bin`
- unit files installed under `/etc/systemd/system`
- seal file generated under `/usr/lib/slime/fireplank.seal`
- runtime socket created at `/run/slime/egress.sock`

---

## Validation Contract

Minimum validation commands:

```bash
systemctl is-active actuator.service slime.service
ls -l /run/slime/egress.sock
curl -sS -X POST http://127.0.0.1:8080/action \
  -H "Content-Type: application/json" \
  -d '{"domain":"test","magnitude":1}'
tail -n 5 /var/log/slime-actuator/events.log
```

Expected:

- both services active
- socket present
- POST returns `AUTHORIZED`
- one new 64-char hex line in actuator log

---

## Reboot Proof

The package is not accepted until this also works:

```bash
sudo reboot
# reconnect
systemctl is-active actuator.service slime.service
ls -l /run/slime/egress.sock
```

Expected:

- services return active after reboot
- socket recreated correctly
- appliance remains fail-closed if actuator socket is missing

---

## Release Acceptance Criteria

`SLIME-Enterprise Hello World` is accepted only if:

1. install works from a fresh host
2. uninstall works cleanly
3. reboot proof passes
4. bundle checksum is published
5. install docs match the real paths and files
6. no hidden dependency on the public `SLIME-Core` checkout is required at install time

---

## Future Extension Boundary

This package proves the appliance.
It does not yet prove:

- replay-hardened production actuator behavior
- full domain registry management
- advanced operational dashboarding
- agent adaptation

Those belong to later package layers.

