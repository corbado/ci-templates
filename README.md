# ci-templates

## Dependabot Security Workflow

Reusable GitHub Actions workflow to handle Dependabot PRs across the org.

Features:

- Only runs for PRs opened by `dependabot[bot]`
- Creates or reuses a tracking issue (labels: `dependabot`, `security` if GHSA)
- Mentions a configurable team/users
- Optionally auto-merges the PR after all checks pass

---

## Usage

```yaml
# .github/workflows/dependabot-security.yml
name: Dependabot security

on:
  pull_request:
    types: [opened, reopened, synchronize]

permissions:
  issues: write
  contents: write
  pull-requests: write
  checks: read
  statuses: read

jobs:
  dependabot-security:
    uses: corbado/ci-templates/.github/workflows/dependabot-security.yml@v1
    secrets:
      repo-token: ${{ secrets.GITHUB_TOKEN }}
    with:
      auto-merge: true # or false for "issue only"
      team_mention: "@Dopeamin / @snacker81" # optional override
```
