# Contributing to SYF Documentation

**Version:** 1.0  
**Last Updated:** 2026-01-24

---

## Overview

This document describes how to contribute to the SYF-DOCS repository while maintaining 
canonical integrity and the sealing policy.

---

## Document Status Hierarchy

### SEALED Documents

**Status:** `sealed`  
**Characteristics:**
- Hash-verified and cryptographically sealed
- Cannot be modified without invalidating canonical status
- Typically stored as PDFs with SHA-256 hashes in `docs/6_audit-and-status/hashes.md`
- Examples: Foundation Charter, Legal Mapping, Terms of Non-Use

**Contribution Policy:** NO modifications permitted. Any change requires re-audit and re-sealing.

### CANONICAL Documents

**Status:** `canonical`  
**Characteristics:**
- Official reference documents
- May receive non-substantive updates (typos, formatting, clarifications)
- Substantive changes require version bump and audit

**Contribution Policy:** 
- Minor fixes: submit PR with clear justification
- Major changes: requires maintainer approval and version update

### UPDATED Documents

**Status:** `updated`  
**Characteristics:**
- Recently modified from canonical version
- Under active development or review
- May be promoted to CANONICAL after stabilization

**Contribution Policy:** Open to contributions with review

### DRAFT Documents

**Status:** `draft`  
**Characteristics:**
- Work in progress
- Not yet canonical
- May have missing sections or placeholder content

**Contribution Policy:** Contributions welcome, follow template guidelines

---

## File Naming Conventions

- Use **kebab-case** (lowercase with hyphens): `security-model.md`
- Version numbers in filename when applicable: `syf-gate-product-spec_v0.1.md`
- No spaces or special characters except hyphens and underscores

---

## Front-Matter Requirements

Every markdown file must include YAML front-matter:

```yaml
---
status: sealed|canonical|updated|draft
version: 0.1
author: AnathemaOfficial
last_updated: YYYY-MM-DD
tags: [legal, engineering, education, security, product]
---
```

**Required Fields:**
- `status`: Document lifecycle stage
- `version`: Semantic version or iteration number
- `author`: Organization or individual author
- `last_updated`: ISO date (YYYY-MM-DD)
- `tags`: Relevant categories (array)

---

## Contribution Workflow

### 1. Fork and Branch

```bash
git checkout main
git pull origin main
git checkout -b docs/your-feature-name
```

### 2. Make Changes

- Follow existing document structure
- Preserve canonical language where applicable
- Add front-matter to new files
- Update `docs/RECORD_OF_CHANGES.md` with your changes

### 3. Validate

- Check markdown syntax
- Verify internal links
- Ensure front-matter is complete
- Review against sealing policy

### 4. Submit Pull Request

**PR Title Format:** `docs: brief description of change`

**PR Description Must Include:**
- Summary of changes
- Files added/modified/removed
- Justification for any CANONICAL or SEALED document changes
- Confirmation that no substantive content was altered (if applicable)

### 5. Review Process

- Maintainers review for canonical integrity
- Sealed documents: automatic rejection if content modified
- Canonical documents: reviewed for substantive vs non-substantive changes
- Draft documents: reviewed for clarity and consistency

---

## Stub Document Policy

Stub documents are placeholders for planned content marked as `status: draft`.

**Stub Template:**
```markdown
---
status: draft
version: 0.1
author: AnathemaOfficial
last_updated: YYYY-MM-DD
tags: [relevant, tags]
---

# Document Title

**Status:** Draft (Stub)

This document is planned but not yet authored.

## Planned Content

- Section 1
- Section 2
- Section 3

---

*This stub was created as part of the documentation reorganization.*
```

---

## Private Documentation

The `docs/private/` directory is gitignored and used for:
- Work-in-progress drafts
- Internal notes
- Sensitive information (never commit)
- Scratch files

**Never commit files from `docs/private/`** — they are automatically ignored.

---

## Templates

Use templates from `docs/templates/` when creating new documents:
- `product-spec-template.md` — Product specifications
- `operational-template.md` — Operational procedures

---

## Contact

For questions about contribution policy or sealing requirements:
- Open an issue in the repository
- Tag maintainers for guidance
- Reference this document in discussions

---

*Maintaining canonical integrity is everyone's responsibility.*
