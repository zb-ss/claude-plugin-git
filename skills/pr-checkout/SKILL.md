---
description: Checkout a pull request locally for review/testing
---

# Checkout Pull Request

Checkout a PR branch locally using the GitHub CLI (`gh`) for review or testing.

## Arguments

$ARGUMENTS

**Format:** `<pr_number|url|branch>`

- `pr_number` - PR number (e.g., 123)
- `url` - Full PR URL
- `branch` - Branch name to find associated PR

## Examples

```
/pr-checkout 123
/pr-checkout https://github.com/owner/repo/pull/123
/pr-checkout feature/user-auth
```

## Instructions

1. **Verify prerequisites:**
   ```bash
   gh auth status
   ```

2. **Stash any local changes** if working directory is dirty:
   ```bash
   git status --porcelain
   # If dirty, offer to stash
   git stash push -m "Auto-stash before PR checkout"
   ```

3. **Checkout the PR:**
   ```bash
   gh pr checkout <pr_number>
   ```

4. **Display PR info:**
   ```bash
   gh pr view <pr_number> --json title,author,state,body,reviewDecision
   ```

5. **Report success** with:
   - PR title and author
   - Current review status
   - Quick commands for review actions

## Post-Checkout Tips

After checkout, suggest useful commands:
```
gh pr diff          # View PR diff
gh pr checks        # View CI status
gh pr review        # Submit review
git log main..HEAD  # View commits
```

## Error Handling

- If PR doesn't exist: "Error: PR #<number> not found"
- If already on PR branch: "Already on PR #<number> branch"
- If conflicts: "Warning: Merge conflicts detected. Resolve before testing."
