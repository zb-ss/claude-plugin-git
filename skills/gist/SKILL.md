---
description: Create or view GitHub gists for quick code sharing
---

# GitHub Gists

Create or view gists using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `create [filename]` - Create a new gist (default action)
- `view <gist_id>` - View gist content
- `list` - List your gists
- `edit <gist_id>` - Edit an existing gist
- `delete <gist_id>` - Delete a gist

## Examples

```
/gist create snippet.js
/gist create --public
/gist view abc123def
/gist list
/gist edit abc123def
```

## Instructions

### Create Gist (default)

1. **Check for staged/selected content:**
   - If filename provided, read that file
   - If content is selected/provided, use that
   - Otherwise, ask user what to include

2. **Prompt for gist options:**
   - Public or private (default: private)
   - Description (optional)
   - Filename (if not provided)

3. **Create the gist:**
   ```bash
   # From file
   gh gist create <filename> --desc "<description>" [--public]

   # From stdin
   echo "<content>" | gh gist create --filename "<name>" --desc "<description>" [--public]
   ```

4. **Report gist URL** to the user

### View Gist

```bash
gh gist view <gist_id> --raw
```

### List Gists

```bash
gh gist list --limit 20
```

### Edit Gist

```bash
gh gist edit <gist_id>
```

### Delete Gist

```bash
gh gist delete <gist_id>
```

Confirm with user before deleting.

## Output Format

After creation:
```
Created gist: https://gist.github.com/<username>/<id>

Files:
- filename.js (123 bytes)
```

## Error Handling

- If `gh` is not installed: "Error: GitHub CLI (gh) is required. Install from https://cli.github.com"
- If not authenticated: "Error: Run 'gh auth login' first"
- If gist not found: "Error: Gist '<id>' not found"
- If file not found: "Error: File '<filename>' not found"
