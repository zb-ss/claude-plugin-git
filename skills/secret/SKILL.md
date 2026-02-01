---
description: Manage repository secrets for GitHub Actions
---

# Repository Secrets

Manage repository secrets for GitHub Actions using the GitHub CLI (`gh`).

## Arguments

$ARGUMENTS

**Format:** `[action] [args...]`

- `list` - List secrets (names only, values are hidden)
- `set <name>` - Set a secret
- `delete <name>` - Delete a secret
- `sync` - Sync secrets from .env file

## Examples

```
/secret list
/secret set API_KEY
/secret set DATABASE_URL "postgres://..."
/secret delete OLD_SECRET
/secret sync .env.production
```

## Instructions

### List Secrets

```bash
gh secret list
```

Format output:
```
Secret Name          Updated
───────────────────────────
API_KEY              2 days ago
DATABASE_URL         1 week ago
DEPLOY_TOKEN         3 months ago

Total: 3 secrets
```

Note: Secret values are never displayed.

### Set Secret

1. **If value not provided inline:**
   - Ask user to input securely
   - Or read from environment variable

2. **Validate secret name:**
   - Must start with letter or underscore
   - Can only contain alphanumeric and underscores
   - Cannot start with GITHUB_ prefix

3. **Set the secret:**
   ```bash
   # From value
   echo "<value>" | gh secret set <name>

   # From file
   gh secret set <name> < secret.txt

   # From env var
   gh secret set <name> --env-file .env
   ```

4. **Confirm:**
   ```
   Secret 'API_KEY' has been set.
   ```

### Delete Secret

1. **Confirm with user** before deleting

2. **Delete:**
   ```bash
   gh secret delete <name>
   ```

3. **Confirm deletion:**
   ```
   Secret 'OLD_SECRET' has been deleted.
   ```

### Sync from .env File

1. **Read .env file:**
   ```bash
   cat .env.production
   ```

2. **Parse key=value pairs**

3. **Show preview:**
   ```
   Will sync the following secrets:
   - API_KEY (new)
   - DATABASE_URL (update)
   - CACHE_HOST (new)

   Continue? [y/N]
   ```

4. **Set each secret:**
   ```bash
   gh secret set <name> -b "<value>"
   ```

5. **Report results:**
   ```
   Synced 3 secrets from .env.production
   - API_KEY: created
   - DATABASE_URL: updated
   - CACHE_HOST: created
   ```

## Environment Secrets

For organization-level or environment-specific secrets:

```bash
# Environment secrets
gh secret set <name> --env production

# List environment secrets
gh secret list --env production
```

## Security Notes

- **NEVER** echo or log secret values
- **NEVER** commit secrets to the repository
- Recommend using `.env.example` with placeholder values
- Secrets are encrypted and only exposed to workflows

## Error Handling

- If not in repo: "Error: Not in a git repository"
- If no write access: "Error: You don't have permission to manage secrets"
- If secret not found: "Error: Secret '<name>' not found"
- If invalid name: "Error: Secret name must start with letter/underscore and contain only alphanumeric/underscores"

## Important

- This manages **repository** secrets, not environment variables
- For environment-specific secrets, use `--env <environment>`
- Changes take effect on next workflow run
