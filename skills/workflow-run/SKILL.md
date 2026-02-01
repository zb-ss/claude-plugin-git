---
description: Trigger or view GitHub Actions workflows
---

# GitHub Actions Workflows

Trigger, view, or manage GitHub Actions workflows using `gh workflow` and `gh run`.

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `list` - List available workflows (default)
- `run <workflow> [--ref <branch>]` - Trigger a workflow
- `view [run_id]` - View workflow run status
- `watch <run_id>` - Watch a running workflow
- `logs <run_id>` - View run logs

## Examples

```
/workflow-run
/workflow-run list
/workflow-run run ci.yml
/workflow-run run deploy.yml --ref main
/workflow-run view
/workflow-run view 12345678
/workflow-run watch 12345678
/workflow-run logs 12345678
```

## Instructions

### List Workflows (default)

```bash
gh workflow list
```

Show workflow names, states, and IDs.

### Trigger Workflow

1. **List available workflows:**
   ```bash
   gh workflow list
   ```

2. **Check if workflow accepts inputs:**
   ```bash
   gh workflow view <workflow>
   ```

3. **Run the workflow:**
   ```bash
   gh workflow run <workflow> [--ref <branch>]
   ```

4. **Get the run ID:**
   ```bash
   gh run list --workflow <workflow> --limit 1 --json databaseId
   ```

5. **Offer to watch:**
   ```bash
   gh run watch <run_id>
   ```

### View Run Status

```bash
# Latest run
gh run list --limit 5

# Specific run
gh run view <run_id>

# With web
gh run view <run_id> --web
```

### Watch Running Workflow

```bash
gh run watch <run_id>
```

Shows live status updates until completion.

### View Logs

```bash
# Full logs
gh run view <run_id> --log

# Failed steps only
gh run view <run_id> --log-failed
```

## Common Workflows

Detect and suggest common workflows:
- `ci.yml` / `test.yml` - CI/Testing
- `build.yml` - Build
- `deploy.yml` / `release.yml` - Deployment
- `lint.yml` - Linting

## Error Handling

- If workflow not found: "Error: Workflow '<name>' not found. Available: <list>"
- If workflow disabled: "Error: Workflow is disabled. Enable in repo settings."
- If no permission: "Error: Cannot trigger workflows in this repository"
- If run failed: Show failed steps and suggest viewing logs
