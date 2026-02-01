---
description: Create or view GitHub issues
---

# GitHub Issues

Create or view issues using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `create [title]` - Create a new issue (default action)
- `view <number>` - View issue details
- `list` - List open issues
- `close <number>` - Close an issue

## Examples

```
/issue create "Bug: Login fails on mobile"
/issue create
/issue view 42
/issue list
/issue close 42
```

## Instructions

### Create Issue (default)

1. **If title not provided**, analyze recent context or ask user

2. **Prompt for issue type:**
   - Bug report
   - Feature request
   - Documentation
   - Other

3. **Generate issue body** based on type:

   **Bug Report:**
   ```markdown
   ## Description
   Brief description of the bug

   ## Steps to Reproduce
   1. Step one
   2. Step two

   ## Expected Behavior
   What should happen

   ## Actual Behavior
   What actually happens

   ## Environment
   - OS:
   - Version:
   ```

   **Feature Request:**
   ```markdown
   ## Description
   Brief description of the feature

   ## Use Case
   Why this feature is needed

   ## Proposed Solution
   How it could be implemented

   ## Alternatives Considered
   Other approaches
   ```

4. **Create the issue:**
   ```bash
   gh issue create --title "<title>" --body "<body>" [--label "<label>"]
   ```

5. **Report issue URL**

### View Issue

```bash
gh issue view <number> --comments
```

### List Issues

```bash
gh issue list --state open --limit 20
```

### Close Issue

```bash
gh issue close <number> --reason completed
```

## Labels

Common labels to suggest:
- `bug`, `feature`, `documentation`
- `good first issue`, `help wanted`
- `priority: high/medium/low`

## Error Handling

- If issue not found: "Error: Issue #<number> not found"
- If no write access: "Error: You don't have permission to create issues"
