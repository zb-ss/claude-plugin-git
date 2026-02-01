---
description: Create and manage GitHub milestones
---

# Manage Milestones

Create and manage milestones for tracking project progress using the GitHub CLI (`gh`) and API.

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `list` - List all milestones
- `create <title>` - Create a new milestone
- `view <number>` - View milestone details
- `edit <number>` - Edit a milestone
- `close <number>` - Close a milestone
- `delete <number>` - Delete a milestone

## Examples

```
/milestone list
/milestone create "v1.0 Release" --due 2024-03-01
/milestone view 1
/milestone edit 1 --due 2024-03-15
/milestone close 1
```

## Instructions

### List Milestones

```bash
gh api repos/{owner}/{repo}/milestones --jq '.[] | [.number, .title, .state, .due_on, .open_issues, .closed_issues] | @tsv'
```

Format output:
```
#    Title           State    Due Date     Progress
───────────────────────────────────────────────────────
1    v1.0 Release    open     2024-03-01   15/20 (75%)
2    v1.1 Beta       open     2024-04-15   3/10 (30%)
3    v0.9 Hotfix     closed   2024-01-15   8/8 (100%)

Open: 2 | Closed: 1
```

### Create Milestone

1. **Gather information:**
   - Title (required)
   - Description (optional)
   - Due date (optional, format: YYYY-MM-DD)

2. **Create:**
   ```bash
   gh api repos/{owner}/{repo}/milestones -f title="<title>" -f description="<desc>" -f due_on="<date>T00:00:00Z"
   ```

3. **Report:**
   ```
   Created milestone #1: "v1.0 Release"
   Due: March 1, 2024
   ```

### View Milestone

```bash
gh api repos/{owner}/{repo}/milestones/<number>
```

Show:
- Title and description
- State (open/closed)
- Due date
- Progress (X of Y issues closed)
- Creator
- Created/updated dates

Also list issues in milestone:
```bash
gh issue list --milestone "<title>"
```

### Edit Milestone

1. **Get current milestone:**
   ```bash
   gh api repos/{owner}/{repo}/milestones/<number>
   ```

2. **Prompt for changes:**
   - New title
   - New description
   - New due date

3. **Update:**
   ```bash
   gh api repos/{owner}/{repo}/milestones/<number> -X PATCH -f title="<title>" -f description="<desc>" -f due_on="<date>"
   ```

### Close Milestone

```bash
gh api repos/{owner}/{repo}/milestones/<number> -X PATCH -f state="closed"
```

Optionally show summary:
```
Closed milestone #1: "v1.0 Release"
Completed: 20/20 issues (100%)
```

### Delete Milestone

1. **Warn user:**
   ```
   Warning: Deleting a milestone will remove it from all associated issues.
   This action cannot be undone.
   ```

2. **Confirm before deleting**

3. **Delete:**
   ```bash
   gh api repos/{owner}/{repo}/milestones/<number> -X DELETE
   ```

## Adding Issues to Milestones

To add an issue to a milestone:
```bash
gh issue edit <issue_number> --milestone "<milestone_title>"
```

To remove from milestone:
```bash
gh issue edit <issue_number> --milestone ""
```

## Progress Tracking

When viewing milestones, calculate and display:
- Percentage complete: `(closed_issues / total_issues) * 100`
- Days remaining until due date
- Overdue warning if past due date

```
Milestone: v1.0 Release
Progress: ████████████░░░░ 75% (15/20)
Due: March 1, 2024 (5 days remaining)
```

## Error Handling

- If milestone not found: "Error: Milestone #<number> not found"
- If title exists: "Error: A milestone with this title already exists"
- If invalid date: "Error: Invalid date format. Use YYYY-MM-DD"
- If no permission: "Error: You don't have permission to manage milestones"
