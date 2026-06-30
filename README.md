# gh-secure

A [GitHub CLI](https://cli.github.com) extension to enable security features on repositories, following best practices from [GitHub Security Lab](https://securitylab.github.com/protect-your-project.html).

## Installation

```bash
gh extension install <owner>/gh-secure
```

### Prerequisites

- [GitHub CLI](https://cli.github.com) (`gh`) installed and authenticated
- Admin or maintainer permissions on the target repository

## Usage

```bash
gh secure                                  # Interactive mode, all features
gh secure --all                            # Enable all features, no prompts
gh secure branch-protection dependabot     # Enable only these two features
gh secure bp ss cs --all                   # Enable 3 features, no prompts
gh secure --repo owner/repo code-scanning  # Enable CodeQL on specific repo
gh secure --all --dry-run                  # Preview what would be enabled
gh secure status                           # Check current feature status
gh secure status --repo owner/repo         # Check status of specific repo
```

### Flags

| Flag | Description |
|------|-------------|
| `-r`, `--repo <owner/repo>` | Target repository (default: current repo) |
| `-a`, `--all` | Enable all features without prompting |
| `-n`, `--dry-run` | Simulate changes without applying them |
| `-v`, `--version` | Print version |
| `-h`, `--help` | Show help message |

### Feature Names

Pass one or more feature names to enable only specific features. If none are specified, all features are included.

| Feature | Shorthand |
|---------|-----------|
| `branch-protection` | `bp` |
| `vulnerability-reporting` | `vr` |
| `secret-scanning` | `ss` |
| `dependabot` | `dep` |
| `code-scanning` | `cs` |

## Security Features

This tool enables five security features based on [GitHub Security Lab recommendations](https://securitylab.github.com/protect-your-project.html):

### 1. Branch Protection
Protects your main branch from unauthorized changes:
- Requires 1 pull request review before merging
- Dismisses stale reviews when new commits are pushed
- Prevents force pushes and branch deletion
- Requires conversation resolution before merging

### 2. Private Vulnerability Reporting
Lets security researchers privately report vulnerabilities to you, giving you time to fix issues before public disclosure.

### 3. Secret Scanning
Detects exposed secrets (API keys, tokens, passwords) and enables push protection to block commits containing secrets. Secret scanning is automatically enabled for public repositories.

### 4. Dependabot
Monitors dependencies for known vulnerabilities, alerts you, and automatically creates PRs to update vulnerable packages.

### 5. Code Scanning (CodeQL)
Uses GitHub's CodeQL static analysis engine to detect security vulnerabilities (SQL injection, XSS, path traversal, etc.) and vulnerable GitHub Actions workflows (script injection, unsafe inputs) on every push and pull request. Uses GitHub's default setup — no workflow file needed.

## Troubleshooting

### "403 Forbidden" Errors
Ensure you have admin or maintain permissions on the repository. For org repos, you may need `admin:org` scope — run `gh auth refresh -s admin:org`.

### Code Scanning Fails
Ensure the repository contains [supported languages](https://codeql.github.com/docs/codeql-overview/supported-languages-and-frameworks/) and that code scanning is available for your plan.

### Branch Protection Fails
Some organizations have policies that restrict branch protection. Contact your org admin.

## Resources

- [GitHub Security Lab: Protect Your Project](https://securitylab.github.com/protect-your-project.html)
- [GitHub Security Documentation](https://docs.github.com/en/code-security)
- [CodeQL Documentation](https://codeql.github.com/docs/)

## License

MIT License
