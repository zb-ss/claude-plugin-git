---
description: Merge a pull request
---

# Merge Pull Request

Merge a PR using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `<pr_number> [--squash|--rebase|--merge] [--delete-branch]`

- `pr_number` - PR number to merge (required)
- `--squash` - Squash and merge (combines all commits)
- `--rebase` - Rebase and merge (linear history)
- `--merge` - Create merge commit (default)
- `--delete-branch` - Delete branch after merge

## Examples

```
/pr-merge 123
/pr-merge 123 --squash
/pr-merge 123 --squash --delete-branch
/pr-merge 123 --rebase
```

## Instructions

1. **Check PR status:**
   ```bash
   gh pr view <pr_number> --json state,mergeable,mergeStateStatus,reviewDecision,statusCheckRollup
   ```

2. **Verify merge requirements:**
   - PR is open
   - PR is mergeable (no conflicts)
   - Required reviews are approved
   - CI checks pass

3. **If not mergeable**, report the blocker:
   - Conflicts: "Error: PR has merge conflicts. Resolve before merging."
   - Reviews: "Error: PR requires approved reviews."
   - Checks: "Error: CI checks are failing."

4. **Confirm merge strategy** if not specified:
   - Show repo's default merge strategy
   - Ask user preference

5. **Merge the PR:**
   ```bash
   gh pr merge <pr_number> --squash|--rebase|--merge [--delete-branch]
   ```

6. **Report success** with:
   - Merge commit SHA
   - Branch deletion status
   - Link to merged PR

## Merge Strategies Explained

| Strategy | Use When |
|----------|----------|
| `--merge` | Preserving full commit history |
| `--squash` | Cleaning up messy commit history |
| `--rebase` | Maintaining linear history |

## Post-Merge Cleanup

After successful merge, suggest:
```bash
git checkout main
git pull
git branch -d <feature-branch>  # local cleanup
```

## Error Handling

- If PR not found: "Error: PR #<number> not found"
- If already merged: "Error: PR #<number> is already merged"
- If closed: "Error: PR #<number> is closed"
- If conflicts: "Error: Resolve merge conflicts first"
- If checks failing: "Error: CI checks must pass before merge"
