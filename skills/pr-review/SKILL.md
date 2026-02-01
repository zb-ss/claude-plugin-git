---
description: Review a pull request with approve/comment/request-changes
---

# Review Pull Request

Submit a review on a PR using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `<pr_number> [action] [comment]`

- `pr_number` - PR number to review (required)
- `action` - One of: `approve`, `comment`, `request-changes` (optional, will prompt)
- `comment` - Review comment (optional, will prompt if needed)

## Examples

```
/pr-review 123 approve
/pr-review 123 approve "LGTM! Great work on the refactor."
/pr-review 123 request-changes "Please add unit tests"
/pr-review 123 comment "Looks good, but I have some suggestions"
```

## Instructions

1. **Fetch PR details:**
   ```bash
   gh pr view <pr_number> --json title,author,files,additions,deletions,commits
   ```

2. **Show PR diff summary:**
   ```bash
   gh pr diff <pr_number> --stat
   ```

3. **If no action specified**, ask user to choose:
   - `approve` - Approve the PR
   - `comment` - Leave a comment without approval
   - `request-changes` - Request changes before approval

4. **If no comment provided** and action requires one, generate or prompt:
   - For `approve`: Can use default "LGTM!" or custom
   - For `request-changes`: Comment is required
   - For `comment`: Comment is required

5. **Submit the review:**
   ```bash
   gh pr review <pr_number> --approve --body "<comment>"
   gh pr review <pr_number> --comment --body "<comment>"
   gh pr review <pr_number> --request-changes --body "<comment>"
   ```

6. **Report success** with review status

## Review Guidelines

When analyzing PR for review suggestions:

1. **Check for obvious issues:**
   - Missing tests for new functionality
   - Security concerns
   - Breaking changes without documentation
   - Code style inconsistencies

2. **Be constructive** in feedback

3. **Acknowledge good work** when approving

## Error Handling

- If PR not found: "Error: PR #<number> not found"
- If already reviewed: "Note: You have already reviewed this PR"
- If own PR: "Error: Cannot review your own PR"
