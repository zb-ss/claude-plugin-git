---
description: Clone a repository with automatic setup (install deps, create branch)
---

# Clone Repository with Setup

Clone a GitHub repository and automatically set it up for development.

## Arguments

$ARGUMENTS

**Format:** `<repo> [branch_name]`

- `repo` - Repository to clone (owner/repo or URL)
- `branch_name` - Optional feature branch to create after cloning

## Examples

```
/repo-clone owner/repo
/repo-clone owner/repo feature/my-feature
/repo-clone https://github.com/owner/repo.git
/repo-clone owner/repo --fork
```

## Instructions

1. **Parse repository reference:**
   - Accept `owner/repo` format
   - Accept full GitHub URL
   - Detect `--fork` flag to fork first

2. **Fork if requested:**
   ```bash
   gh repo fork <owner/repo> --clone
   ```

3. **Clone the repository:**
   ```bash
   gh repo clone <owner/repo>
   # or
   git clone <url>
   ```

4. **Change to repository directory:**
   ```bash
   cd <repo_name>
   ```

5. **Detect and install dependencies:**

   Check for package managers and install:

   | File | Command |
   |------|---------|
   | `package.json` | `npm install` or `yarn` or `pnpm install` |
   | `composer.json` | `composer install` |
   | `requirements.txt` | `pip install -r requirements.txt` |
   | `Gemfile` | `bundle install` |
   | `go.mod` | `go mod download` |
   | `Cargo.toml` | `cargo build` |

6. **Create feature branch if specified:**
   ```bash
   git checkout -b <branch_name>
   ```

7. **Run initial setup scripts if present:**
   - Check for `setup.sh`, `init.sh`, or similar
   - Check for `make init` or `make setup`
   - Report but don't auto-run (security)

8. **Report summary:**
   ```
   Cloned: owner/repo
   Directory: /path/to/repo
   Dependencies: npm install (completed)
   Branch: feature/my-feature (created)

   Ready to develop!
   ```

## Options

- `--fork` - Fork the repository first, then clone your fork
- `--depth <n>` - Shallow clone with limited history
- `--no-deps` - Skip dependency installation

## Error Handling

- If repo not found: "Error: Repository '<repo>' not found or not accessible"
- If directory exists: "Error: Directory '<name>' already exists"
- If deps fail: "Warning: Dependency installation failed. Run manually."

## Important

- Always inform user before running install commands
- Do not auto-run arbitrary setup scripts (security risk)
- Report the full path where repo was cloned
