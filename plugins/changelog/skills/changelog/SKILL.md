---
name: changelog
description: Generate changelogs and audit documentation against code for inconsistencies
---

# Changelog Skill

Generates changelogs from git history and audits documentation against the actual codebase to catch inconsistencies — wrong install instructions, outdated API examples, nonexistent CLI flags, broken paths, and more.

## Usage

```
/changelog
/changelog --since v1.0.0
/changelog --audit
/changelog --full --fix
/changelog --scope ./plugins/focusgroup
/doccheck
/doccheck --fix
```

## Arguments

| Argument | Description | Default |
|----------|-------------|---------|
| `--since TAG\|COMMIT` | Starting point for changelog | last tag or 50 commits |
| `--audit` | Doc audit only, skip changelog | both |
| `--full` | Changelog + comprehensive doc audit | both |
| `--fix` | Auto-fix unambiguous inconsistencies | off |
| `--format md\|json` | Output format | md |
| `--out <dir>` | Output directory | .changelog/{timestamp} |
| `--scope <path>` | Limit audit to a subdirectory | repo root |
| `--audience dev\|user\|both` | Changelog audience targeting | both |
| `--group-by type\|scope\|component` | Changelog grouping | type |

## What It Catches

### Install & Setup
- Package names that don't exist in manifest files
- Install commands with wrong syntax or nonexistent packages
- Referenced scripts/binaries that don't exist
- Setup steps that would fail or are in wrong order

### API & Usage
- Function signatures that don't match source code
- CLI flags that don't exist in the argument parser
- Code examples using APIs that were renamed or removed
- Documented defaults that differ from actual defaults

### Configuration
- Config keys the code doesn't actually read
- Environment variables with wrong names
- Example configs that don't match the schema

### Architecture & Structure
- File paths that don't exist
- Component descriptions that don't match the code
- Outdated dependency relationships

### Change Coverage
- Code changes without corresponding doc updates
- Docs referencing removed or changed features
- New features without any documentation

## Output

All output goes to `.changelog/{timestamp}/`:
- `report.md` — unified report with health score
- `CHANGELOG.md` — generated changelog
- `audit-*.md` — per-category audit details
- `cross-reference.md` — changes-to-docs mapping
- `fixes-applied.md` — auto-fix log (if --fix)
- `report.json` — machine-readable report (if --format json)

## Documentation Health Score

Scores documentation on a 0-100 scale:
- **80-100 HEALTHY** — docs are in good shape
- **50-79 NEEDS ATTENTION** — some inconsistencies to address
- **0-49 CRITICAL** — docs are actively misleading users

## Magic Keywords

- "changelog", "doc check", "doc audit", "documentation check", "doc drift", "doc consistency"
