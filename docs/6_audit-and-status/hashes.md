---
status: sealed
version: 0.1
author: AnathemaOfficial
last_updated: 2026-01-24
tags: [audit, hashes, verification]
---

# Technologies CoreXalt Inc. Foundation Archive — Cryptographic Hashes

**Generated:** 2026-01-23T19:19:33.776301  
**Algorithm:** SHA-256  
**Status:** CANON SEALED

---

## Purpose

This document contains SHA-256 cryptographic hashes for all sealed PDF documents in the archive. These hashes provide cryptographic verification of document integrity.

---

## Document Hashes

```
SHA256(SYF_LAW_USAGE_LICENSE_v0.1.pdf) =
  f2dca58687d0d81f3b31a158b0d463fb41279856a32538b3605ffe29a4eb3733

SHA256(SYFCORP_OVERVIEW_v0.1.pdf) =
  8cf02746219d194e69b693a6900a8689790a4440b6d62404ff93a00961f3f277

SHA256(ARCHITECTURE_CANON_v0.1.pdf) =
  b57a81876bf8adc9eaf57a9e43274a46e1303f99f2c73e9bf33bd19c4a0f6425

SHA256(LEGAL_MAPPING_v0.1.pdf) =
  00f609eabf7c63c2e69b2e82b44be3a8e0ce3434d48d1bdce046e7e177748131

SHA256(FOUNDATION_CHARTER_v0.1.pdf) =
  9d517accbd17d6b225f1670042a13635e27259bd8c2d10e0deffb978e007ea0f

SHA256(BOUNDARY_OF_LIABILITY_v0.1.pdf) =
  ade3bbc64055111329521a45a7169d7de80699222f85993146b93d50aab22b35

SHA256(TERMS_OF_NON_USE_v0.1.pdf) =
  6d80035d11a1d4108d4406d804ae08f523dfa7733b3d90b682d8ce72eea3caae

SHA256(INVARIANTS_v0.1.pdf) =
  666e938f03fe22f3cc9fe8670245f1ef282e0d97ef88673ef30a78709f1de584
```

---

## Verification Instructions

To verify a document:

```bash
sha256sum <filename>.pdf
```

Compare the output with the hash listed above. They must match exactly.

---

## Notes

- Any modification to a sealed document will change its hash
- Hash mismatches indicate tampering or corruption
- All hashes must be verified before relying on canonical status

---

*Converted from HASHES.txt as part of documentation reorganization. Original content preserved.*
