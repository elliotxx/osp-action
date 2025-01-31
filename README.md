# OSP Action

GitHub Action for OSP (Open Source Planning)

## What is OSP?

OSP (Open Source Planning) is a command-line tool that helps you manage your open source planning. It can:
- Automatically update your planning file based on GitHub issues and pull requests
- Track progress of your planning
- Generate reports and statistics

## Usage

```yaml
name: Update Planning

on:
  schedule:
    - cron: '0 0 * * *'  # Run daily at midnight
  workflow_dispatch:      # Allow manual trigger

jobs:
  update-planning:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Update Planning
        uses: elliotxx/osp-action@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          plan-file: '.github/planning.yml'  # Optional, default is '.github/planning.yml'

      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v5
        with:
          commit-message: 'chore: update planning [skip ci]'
          title: 'chore: update planning'
          body: |
            Update planning file based on GitHub issues and pull requests.
            This is an automated pull request.
          branch: update-planning
          delete-branch: true
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `github-token` | GitHub token | Yes | N/A |
| `plan-file` | Path to the plan file | No | `.github/planning.yml` |

## License

MIT
