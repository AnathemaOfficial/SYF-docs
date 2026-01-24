---
status: draft
version: 0.1
author: AnathemaOfficial
last_updated: 2026-01-24
tags: [documentation, maintenance, naming]
---

# File Naming Suggestions

**Purpose:** This document tracks files that don't follow kebab-case naming convention and suggests safe renaming strategies.

---

## Overview

According to `docs/DOCS_CONTRIBUTING.md`, all files should use **kebab-case** (lowercase with hyphens).

The following files currently use SCREAMING_SNAKE_CASE:

---

## Files Requiring Review

### Meta-Documentation Files

These are high-level meta-documentation files. Renaming them would require:
1. Updating all references in other markdown files
2. Updating any CI/CD workflows that may reference them
3. Communicating the change to all contributors

| Current Name | Suggested Name | Impact Assessment |
|-------------|----------------|-------------------|
| `DOCS_CONTRIBUTING.md` | `docs-contributing.md` | **HIGH** - Referenced in README.md and multiple docs. Central contribution guide. |
| `INDEX.md` | `index.md` | **HIGH** - Main navigation file, referenced in README.md and throughout docs. |
| `RECORD_OF_CHANGES.md` | `record-of-changes.md` | **MEDIUM** - Referenced in DOCS_CONTRIBUTING.md. Manual changelog. |

---

## Recommendation

**Option 1: Accept Exception (RECOMMENDED)**
- Keep SCREAMING_SNAKE_CASE for meta-documentation files (DOCS_CONTRIBUTING.md, INDEX.md, RECORD_OF_CHANGES.md)
- Rationale: These are special meta-files that intentionally stand out in directory listings
- Precedent: Common pattern in open-source (e.g., README, LICENSE, CONTRIBUTING files)
- Update `DOCS_CONTRIBUTING.md` to explicitly allow SCREAMING_SNAKE_CASE for meta-documentation

**Option 2: Gradual Rename**
- Create kebab-case versions alongside existing files
- Update all references gradually
- Deprecate old names after transition period
- Risk: Confusion during transition, broken links if incomplete

**Option 3: Immediate Rename with Git Redirect**
- Rename all at once using `git mv`
- Update all references in single PR
- Risk: High impact, requires thorough testing

---

## Next Steps

1. Review this document with maintainers
2. Decide on naming policy for meta-documentation
3. If renaming is approved:
   - Create comprehensive impact analysis
   - Identify all references (code, docs, CI/CD)
   - Plan coordinated update
4. Update `DOCS_CONTRIBUTING.md` with final policy

---

*Created: 2026-01-24*  
*Status: Awaiting maintainer review*
