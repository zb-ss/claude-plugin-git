---
description: Manage issue and PR labels
---

# Manage Labels

Create, edit, and manage labels for issues and pull requests using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `list` - List all labels in the repository
- `create <name>` - Create a new label
- `edit <name>` - Edit an existing label
- `delete <name>` - Delete a label
- `add <issue> <labels...>` - Add labels to issue/PR
- `remove <issue> <labels...>` - Remove labels from issue/PR

## Examples

```
/label list
/label create bug --color d73a4a --description "Something isn't working"
/label create "help wanted" --color 008672
/label edit bug --color ff0000
/label delete deprecated
/label add 123 bug "help wanted"
/label remove 123 wontfix
```

## Instructions

### List Labels

```bash
gh label list
```

Format output:
```
Label              Color     Description
─────────────────────────────────────────────────────
bug                #d73a4a   Something isn't working
enhancement        #a2eeef   New feature or request
documentation      #0075ca   Improvements or additions to docs
good first issue   #7057ff   Good for newcomers
help wanted        #008672   Extra attention is needed

Total: 5 labels
```

### Create Label

1. **Parse options:**
   - `--color <hex>` - Color without # (default: random)
   - `--description <text>` - Description (optional)

2. **Create:**
   ```bash
   gh label create "<name>" --color "<hex>" --description "<desc>"
   ```

3. **Confirm:**
   ```
   Created label 'bug' with color #d73a4a
   ```

### Edit Label

1. **Get current label info:**
   ```bash
   gh label list --search "<name>"
   ```

2. **Prompt for changes:**
   - New name (optional)
   - New color (optional)
   - New description (optional)

3. **Update:**
   ```bash
   gh label edit "<name>" [--name "<new_name>"] [--color "<hex>"] [--description "<desc>"]
   ```

### Delete Label

1. **Confirm with user** - Deleting removes label from all issues/PRs

2. **Delete:**
   ```bash
   gh label delete "<name>" --yes
   ```

### Add Labels to Issue/PR

```bash
gh issue edit <number> --add-label "<label1>,<label2>"
# or for PR
gh pr edit <number> --add-label "<label1>,<label2>"
```

### Remove Labels from Issue/PR

```bash
gh issue edit <number> --remove-label "<label1>,<label2>"
# or for PR
gh pr edit <number> --remove-label "<label1>,<label2>"
```

## Common Label Sets

Suggest standard labels:
```
Priority:
- priority: critical  (#b60205)
- priority: high      (#d93f0b)
- priority: medium    (#fbca04)
- priority: low       (#0e8a16)

Type:
- bug                 (#d73a4a)
- enhancement         (#a2eeef)
- documentation       (#0075ca)
- question            (#d876e3)

Status:
- wontfix             (#ffffff)
- duplicate           (#cfd3d7)
- invalid             (#e4e669)
```

## Color Reference

Common colors:
- Red (bug): `d73a4a`
- Blue (docs): `0075ca`
- Green (help): `008672`
- Purple (question): `d876e3`
- Yellow (warning): `fbca04`

## Error Handling

- If label exists: "Error: Label '<name>' already exists"
- If label not found: "Error: Label '<name>' not found"
- If issue not found: "Error: Issue/PR #<number> not found"
- If no permission: "Error: You don't have permission to manage labels"
