# Git Plugin for Claude Code

Git and GitHub workflow commands using the `gh` CLI.

## Installation

In Claude Code, run:

```
/plugin marketplace add zb-ss/claude-plugin-git
/plugin install git@zb-ss-claude-plugin-git
```

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| commit | `/git:commit` | Create conventional commit |
| pr | `/git:pr` | Create pull request |
| pr-checkout | `/git:pr-checkout` | Checkout PR locally |
| pr-review | `/git:pr-review` | Review a pull request |
| pr-merge | `/git:pr-merge` | Merge a pull request |
| pr-list | `/git:pr-list` | List PRs with filters |
| release | `/git:release` | Create GitHub release with changelog |
| issue | `/git:issue` | Create or view issues |
| label | `/git:label` | Manage issue/PR labels |
| milestone | `/git:milestone` | Create/manage milestones |
| gist | `/git:gist` | Create/view gists for code sharing |
| browse | `/git:browse` | Open in browser |
| workflow-run | `/git:workflow-run` | Trigger GitHub Actions |
| secret | `/git:secret` | Manage repository secrets |
| repo-clone | `/git:repo-clone` | Clone with automatic setup |
| codespace | `/git:codespace` | Create/connect to Codespaces |

## Usage Examples

### Commits
```bash
/git:commit                    # Commit staged changes
/git:commit fix login bug      # Commit with context
```

### Pull Requests
```bash
/git:pr feature/auth           # Create PR from branch
/git:pr-checkout 123           # Checkout PR #123
/git:pr-review 123 approve     # Approve PR
/git:pr-merge 123 --squash     # Squash merge PR
/git:pr-list --author @me      # List my PRs
/git:pr-list --reviewer @me    # PRs awaiting my review
```

### Releases
```bash
/git:release v1.2.0            # Create release with changelog
/git:release v2.0.0-beta --prerelease
```

### Issues
```bash
/git:issue create "Bug title"  # Create issue
/git:issue view 42             # View issue
/git:issue list                # List open issues
```

### Labels & Milestones
```bash
/git:label list                # List all labels
/git:label create bug --color d73a4a
/git:label add 123 bug         # Add label to issue
/git:milestone create "v1.0"   # Create milestone
/git:milestone list            # List milestones
```

### Gists
```bash
/git:gist create snippet.js    # Create gist from file
/git:gist list                 # List your gists
/git:gist view abc123          # View a gist
```

### GitHub Actions
```bash
/git:workflow-run              # List workflows
/git:workflow-run run ci.yml   # Trigger workflow
/git:workflow-run watch 123    # Watch running workflow
```

### Secrets
```bash
/git:secret list               # List repository secrets
/git:secret set API_KEY        # Set a secret
/git:secret sync .env          # Sync secrets from .env
```

### Repository Setup
```bash
/git:repo-clone owner/repo     # Clone and install deps
/git:repo-clone owner/repo feature/new  # Clone + create branch
/git:repo-clone owner/repo --fork       # Fork then clone
```

### Codespaces
```bash
/git:codespace create          # Create codespace
/git:codespace list            # List codespaces
/git:codespace code my-space   # Open in VS Code
/git:codespace ssh my-space    # SSH into codespace
```

### Browse
```bash
/git:browse                    # Open repo
/git:browse 123                # Open issue/PR #123
/git:browse --actions          # Open Actions tab
```

## Requirements

- GitHub CLI (`gh`) installed and authenticated
- Git repository with GitHub remote

## Commit Convention

Uses [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `refactor:` - Code refactoring
- `test:` - Tests
- `chore:` - Maintenance

## License

MIT
