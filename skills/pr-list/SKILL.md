---
description: List pull requests with filters (author, reviewer, state)
---

# List Pull Requests

List pull requests with various filters using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[filters...]`

Filters can include:
- `--author <user>` - Filter by author
- `--reviewer <user>` - Filter by reviewer
- `--assignee <user>` - Filter by assignee
- `--state <state>` - open, closed, merged, all (default: open)
- `--label <label>` - Filter by label
- `--base <branch>` - Filter by base branch
- `--draft` - Show only draft PRs
- `--search <query>` - Custom search query

## Examples

```
/pr-list
/pr-list --author @me
/pr-list --reviewer @me
/pr-list --state merged --author octocat
/pr-list --label bug --state open
/pr-list --base main --draft
/pr-list --search "WIP in:title"
```

## Instructions

1. **Parse filter arguments**

2. **Build and execute query:**
   ```bash
   gh pr list [--author <user>] [--assignee <user>] [--state <state>] [--label <label>] [--base <branch>] [--limit 30]
   ```

   For reviewer filter (not directly supported):
   ```bash
   gh pr list --search "review-requested:<user>"
   ```

3. **Format output** in a readable table:
   ```
   #    Title                          Author      Status    Updated
   ──────────────────────────────────────────────────────────────────
   123  Fix login validation           @user1      OPEN      2h ago
   120  Add dark mode support          @user2      DRAFT     1d ago
   118  Update dependencies            @user3      MERGED    3d ago
   ```

4. **Show summary:**
   ```
   Showing 15 of 42 pull requests (state: open)
   ```

## Special Values

- `@me` - Current authenticated user
- `--state all` - Show all states
- `--limit <n>` - Number of results (default: 30)

## Output Details

For each PR show:
- PR number
- Title (truncated if too long)
- Author
- Status (OPEN, DRAFT, MERGED, CLOSED)
- Labels (if any)
- Updated time (relative)

## Error Handling

- If not in a repo: "Error: Not in a git repository. Run from a repo directory or specify --repo owner/name"
- If user not found: "Error: User '<user>' not found"
- If no results: "No pull requests found matching your filters"

## Tips

Suggest common queries:
- "PRs awaiting your review: `/pr-list --reviewer @me`"
- "Your open PRs: `/pr-list --author @me`"
- "Recently merged: `/pr-list --state merged --limit 10`"
