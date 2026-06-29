---
name: update-changelog
description: "Read this skill before updating changelogs"
---

Update the repository changelog with changes between the last release and the current version (`main` or `master`). If `CHANGELOG.md` file does not exist, use `CHANGELOG` instead.

## Step-by-Step Process

### 1. Determine baseline version
If no baseline version is provided, use the most recent git tag. You can find it with `git describe --tags --abbrev=0`.

### 2. Find the commits from git

Use the following commands to gather commit information:

```bash
# Get the baseline version (if not provided)
git describe --tags --abbrev=0

# Get all commits since the baseline version
git log <baseline-version>..HEAD
```

### 3. Update the changelog
Read the existing changelog file (`CHANGELOG.md` or `CHANGELOG` if missing) and check if there are changes not yet incorporated, then add them. Always add them to the "Unreleased" section only. If there is none yet, add it at the top in the same style as the existing changelog (for example, `## Unreleased` vs `## [Unreleased]`).

## Ground Rules When Writing Changelogs

### Content Guidelines
* Focus on **notable changes** that affect users (features, fixes, breaking changes)
* Mention pull requests (`#NUMBER`) when available, but not raw commit hashes
* Ignore insignificant changes (typo fixes, internal refactoring, minor documentation updates)
* Group related changes together by a category when it is possible
* Order entries by importance: breaking changes first, then features, then fixes

### Style Guidelines
* Use valid markdown syntax
* Start each entry with a past-tense verb or descriptive phrase
* Keep entries concise but descriptive enough to understand the change
* Use bullet points (`*` or `-`) for individual changes
* Format code references with backticks (e.g., `` `foo.cleanup` ``)

### Example Format

```markdown
## 1.1.0
* Added multi-key support to the `sort` filter. (#15)
* Added asyncio-compatible interfaces (#14)
* Fixed `not undefined` with strict undefined behavior. (#12)

## 1.2.0
* Added multi-consumer channels for message passing (#17)
* Added `map` support for streams. (#18)
* Added CLI `--dry-run` feature flag (#24)
* Fixed timezone handling for scheduled tasks (#25)
* Fixed crash when parsing empty JSON files (#23)
```

### Good vs Bad Examples
**Good:**
* `Fixed an issue with the TypeScript SDK which caused an incorrect config for CJS.`
* `Added support for claim timeout extension on checkpoint writes.`
* `Improved error reporting when task claim expires.`

**Bad:**
* `Fixed bug` (too vague)
* `Updated dependencies` (insignificant unless it fixes a security issue)
* `Refactored internal code structure` (internal change, not user-facing)
* `Fixed typo in comment` (insignificant)

## Notes
* If the current changelog already has an "Unreleased" section with content, append to it rather than replacing it
* Preserve the existing changelog style and formatting (headings, bullet style, ordering, and spacing)
* If the repo uses a different default branch name, treat that as the "current version" instead of `main` or `master`
* When in doubt about whether a change is significant, ask a user about adding this change
