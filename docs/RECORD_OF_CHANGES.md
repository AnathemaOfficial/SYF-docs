# Record of Changes

**Repository:** SYF-DOCS  
**Maintained Since:** 2026-01-24

---

## Purpose

This file tracks significant changes to the documentation structure and canonical documents.

For detailed commit history, use `git log`.

---

## 2026-01-24 — Documentation Reorganization

**Type:** Major restructuring  
**Status:** In Progress  
**Branch:** `docs/reorg/2026-01-24`

### Changes

#### Structure
- Created `docs/` directory with numbered sections (1-7)
- Added `docs/INDEX.md` as central navigation
- Added `docs/DOCS_CONTRIBUTING.md` with contribution guidelines
- Added `docs/.gitignore` to exclude private documentation
- Created `docs/templates/` for document templates
- Created `assets/` for diagrams and media

#### Migrations
- Moved `SYF_FOUNDATION.md` → `docs/1_foundational/syf-foundation.md`
- Moved `R_INVARIANT.md` → `docs/1_foundational/r-invariant.md`
- Moved `SECURITY_MODEL.md` → `docs/2_security/security-model.md`
- Moved `R_SPEC_TEMPLATE.md` → `docs/3_implementation/r-spec-template.md`
- Moved `ANATHEMA_SOFT_EXPLAINED.md` → `docs/7_education/anathema-soft-explained.md`
- Moved `AUDIT_STATUS.md` → `docs/6_audit-and-status/audit-status.md`
- Converted `MANIFEST.txt` → `docs/5_legal/manifest.md`
- Converted `HASHES.txt` → `docs/6_audit-and-status/hashes.md`

#### Stubs Created
The following stubs were created for documents listed in AUDIT_STATUS.md as missing:
- `docs/1_foundational/syf-anathema-bridge.md` (draft)
- `docs/2_security/comparison-classic.md` (draft)
- `docs/2_security/why-detection-fails.md` (draft)
- `docs/2_security/breaker-qa.md` (draft)
- `docs/3_implementation/r-faq.md` (draft)
- `docs/3_implementation/r-failure-modes.md` (draft)
- `docs/4_product-and-operational/syf-gate-product-spec_v0.1.md` (draft)
- `docs/4_product-and-operational/syf-shield-product-spec_v0.1.md` (draft)
- `docs/4_product-and-operational/anathema-breaker-spec.md` (draft)
- `docs/4_product-and-operational/client-pilot-template.md` (draft)
- `docs/4_product-and-operational/compliance-checklist.md` (draft)
- `docs/5_legal/boundary-of-liability.md` (reference to PDF)
- `docs/5_legal/terms-of-non-use.md` (reference to PDF)
- `docs/5_legal/invariants.md` (reference to PDF)

#### Front-Matter Added
- All migrated markdown files received YAML front-matter
- Status extracted from source documents where available
- Version numbers preserved from original documents

#### Root Updates
- Updated `README.md` to point to `docs/INDEX.md`
- Created `README.md.bak` as backup of original

#### Automation
- Added `.github/workflows/docs-hash.yml` skeleton for manifest regeneration

### Rationale

This reorganization:
1. Creates clear navigation structure with numbered sections
2. Standardizes file naming (kebab-case)
3. Adds metadata for document lifecycle management
4. Separates canonical documents from stubs
5. Preserves all original content without modification
6. Establishes contribution and sealing policies

### Impact

- **Breaking:** Internal links may need updates
- **Non-Breaking:** All content preserved, only relocated
- **Git History:** Preserved via `git mv` where possible

---

## Template

```markdown
## YYYY-MM-DD — Change Title

**Type:** Major|Minor|Patch|Fix  
**Status:** Completed|In Progress  
**Branch:** branch-name (if applicable)

### Changes
- Bullet points of changes

### Rationale
Why the changes were made

### Impact
- Breaking changes
- Migrations required
- Compatibility notes
```

---

*This file is maintained manually. For complete history, use `git log --follow`.*
