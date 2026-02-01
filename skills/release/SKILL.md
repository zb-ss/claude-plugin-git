---
description: Create a GitHub release with rich changelog notes
---

# Create GitHub Release

Create a release using the GitHub CLI (`gh`) with auto-generated or custom changelog notes.

## Arguments

$ARGUMENTS

**Format:** `<version> [--draft] [--prerelease] [--target <branch>]`

- `version` - Version tag (e.g., v1.2.0, 1.2.0)
- `--draft` - Create as draft release
- `--prerelease` - Mark as pre-release
- `--target` - Target branch (defaults to current branch)

## Examples

```
/release v1.2.0
/release v2.0.0-beta.1 --prerelease
/release v1.3.0 --draft
/release v1.4.0 --target main
```

## Instructions

1. **Verify prerequisites:**
   ```bash
   gh auth status
   git fetch --tags
   ```

2. **Check if tag already exists:**
   ```bash
   git tag -l "<version>"
   gh release view <version> 2>/dev/null
   ```

3. **Find previous release tag:**
   ```bash
   git describe --tags --abbrev=0 2>/dev/null || echo "No previous tag"
   ```

4. **Generate changelog** by analyzing commits since last release:
   ```bash
   git log <previous_tag>..HEAD --pretty=format:"%h %s" --no-merges
   ```

5. **Categorize changes** into sections:
   - **Features** - `feat:` commits
   - **Bug Fixes** - `fix:` commits
   - **Performance** - `perf:` commits
   - **Breaking Changes** - commits with `BREAKING CHANGE:` or `!:`
   - **Documentation** - `docs:` commits
   - **Other Changes** - remaining commits

6. **Create release notes** in markdown format (see template below)

7. **Create the release:**
   ```bash
   gh release create <version> \
     --title "<version>" \
     --notes "<changelog>" \
     [--draft] \
     [--prerelease] \
     [--target <branch>]
   ```

8. **Report the release URL** to the user

## Changelog Template

```markdown
## What's Changed

### Features
- feat: description (#PR)
- feat(scope): description (#PR)

### Bug Fixes
- fix: description (#PR)

### Performance
- perf: description (#PR)

### Breaking Changes
- **BREAKING:** description

### Other Changes
- chore: description
- refactor: description

**Full Changelog**: https://github.com/owner/repo/compare/v1.1.0...v1.2.0
```

## Smart Changelog Generation

When generating the changelog:

1. **Parse commit messages** for conventional commit prefixes
2. **Extract PR numbers** from commit messages or merge commits
3. **Link contributors** using `@username` when available
4. **Include comparison link** at the bottom
5. **Highlight breaking changes** prominently at the top if any exist

## Error Handling

- If `gh` is not installed: "Error: GitHub CLI (gh) is required. Install from https://cli.github.com"
- If not authenticated: "Error: Run 'gh auth login' first"
- If tag exists: "Error: Release <version> already exists. Use a different version."
- If no commits since last release: "Warning: No new commits since <previous_tag>"

## Important

- Do NOT add any AI/LLM attribution
- Follow semantic versioning conventions
- Include breaking changes prominently if present
- Keep changelog entries concise but descriptive
