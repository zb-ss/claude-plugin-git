# Git Plugin for Claude Code

Git and GitHub workflow commands using the `gh` CLI.

## Installation

Add to your Claude Code configuration:

```bash
claude --plugin-dir /path/to/git
```

Or add to your settings:

```json
{
  "plugins": ["/path/to/git"]
}
```

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| commit | `/git:commit` | Create conventional commit |
| pr | `/git:pr` | Create pull request |
| pr-checkout | `/git:pr-checkout` | Checkout PR locally |
| pr-review | `/git:pr-review` | Review a pull request |
| pr-merge | `/git:pr-merge` | Merge a pull request |
| release | `/git:release` | Create GitHub release with changelog |
| issue | `/git:issue` | Create or view issues |
| browse | `/git:browse` | Open in browser |
| workflow-run | `/git:workflow-run` | Trigger GitHub Actions |

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

### GitHub Actions
```bash
/git:workflow-run              # List workflows
/git:workflow-run run ci.yml   # Trigger workflow
/git:workflow-run watch 123    # Watch running workflow
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
