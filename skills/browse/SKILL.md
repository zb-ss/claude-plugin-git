---
description: Open repository, PR, issue, or file in browser
---

# Browse in GitHub

Open various GitHub resources in your default browser using `gh browse`.

## Arguments

$ARGUMENTS

**Format:** `[target]`

- (none) - Open repository homepage
- `<number>` - Open issue or PR by number
- `<file>` - Open file in current branch
- `<file>:<line>` - Open file at specific line
- `--branch <name>` - Open specific branch
- `--settings` - Open repo settings
- `--wiki` - Open wiki
- `--projects` - Open projects
- `--releases` - Open releases page
- `--actions` - Open GitHub Actions

## Examples

```
/browse
/browse 123
/browse src/index.ts
/browse src/index.ts:42
/browse --branch develop
/browse --settings
/browse --actions
/browse --releases
```

## Instructions

1. **Parse the target argument**

2. **Execute appropriate browse command:**

   **Repository homepage:**
   ```bash
   gh browse
   ```

   **Issue or PR:**
   ```bash
   gh browse <number>
   ```

   **File (optionally with line):**
   ```bash
   gh browse <file>
   gh browse <file>:<line>
   ```

   **Branch:**
   ```bash
   gh browse --branch <name>
   ```

   **Special pages:**
   ```bash
   gh browse --settings
   gh browse --wiki
   gh browse --projects
   ```

   **Releases:**
   ```bash
   gh browse --releases
   # Or: gh release view --web
   ```

   **Actions:**
   ```bash
   gh browse --actions
   # Or: gh run list --web
   ```

3. **Report the URL** that was opened

## Smart Detection

If a number is provided, detect whether it's an issue or PR:
```bash
gh issue view <number> --json number 2>/dev/null && echo "issue" || echo "pr"
```

## Error Handling

- If not in a git repo: "Error: Not in a GitHub repository"
- If file not found: "Error: File '<file>' not found"
- If issue/PR not found: "Error: #<number> not found"
