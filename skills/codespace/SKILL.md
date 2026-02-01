---
description: Create or connect to GitHub Codespaces
---

# GitHub Codespaces

Create, manage, and connect to GitHub Codespaces using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `create [repo]` - Create a new codespace
- `list` - List your codespaces
- `code [name]` - Open codespace in VS Code
- `ssh [name]` - SSH into a codespace
- `stop [name]` - Stop a running codespace
- `delete [name]` - Delete a codespace

## Examples

```
/codespace create
/codespace create owner/repo
/codespace create --machine largePremiumLinux
/codespace list
/codespace code my-codespace
/codespace ssh my-codespace
/codespace stop
/codespace delete my-codespace
```

## Instructions

### Create Codespace

1. **Determine repository:**
   - If repo provided, use it
   - If in a git repo, use current repo
   - Otherwise, ask user

2. **Check for devcontainer:**
   ```bash
   gh api repos/{owner}/{repo}/contents/.devcontainer
   ```
   Report if devcontainer exists.

3. **Prompt for options:**
   - Machine type (if user wants non-default)
   - Branch (default: default branch)
   - Region (optional)

4. **Create codespace:**
   ```bash
   gh codespace create --repo <owner/repo> [--branch <branch>] [--machine <type>]
   ```

5. **Report creation:**
   ```
   Created codespace: <name>
   Machine: 2-core, 4GB RAM
   Repository: owner/repo
   Branch: main

   Connect with:
     VS Code: /codespace code <name>
     SSH: /codespace ssh <name>
     Browser: gh codespace code --web -c <name>
   ```

### List Codespaces

```bash
gh codespace list
```

Format output:
```
Name                 Repository        Branch    State     Machine
─────────────────────────────────────────────────────────────────
turbo-spork-abc123   owner/repo        main      Running   2-core
fuzzy-robot-xyz789   owner/other       develop   Stopped   4-core
```

### Open in VS Code

```bash
gh codespace code -c <name>
```

### SSH into Codespace

```bash
gh codespace ssh -c <name>
```

### Stop Codespace

```bash
gh codespace stop -c <name>
```

If no name provided, show list and let user choose.

### Delete Codespace

```bash
gh codespace delete -c <name>
```

**Always confirm** before deleting.

## Machine Types

Common machine types:
- `basicLinux` - 2 cores, 4GB RAM
- `standardLinux` - 4 cores, 8GB RAM
- `premiumLinux` - 8 cores, 16GB RAM
- `largePremiumLinux` - 16 cores, 32GB RAM

## Error Handling

- If not authenticated: "Error: Run 'gh auth login' first"
- If codespace limit reached: "Error: Codespace limit reached. Delete unused codespaces."
- If codespace not found: "Error: Codespace '<name>' not found"
- If VS Code not installed: "Tip: Install VS Code or use --web flag for browser"

## Billing Note

Remind users: "Note: Codespaces usage may incur charges. Check your billing settings."
