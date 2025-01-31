# OSP Action

GitHub Action for OSP (Open Source Software Pilot) - Streamline your open source project management in CI/CD pipelines.

## What is OSP?

OSP (Open Source Software Pilot) is a command-line tool designed to improve the efficiency of open source project management. It provides various features to help you:

- Generate and update community planning based on milestone issues
- Track project statistics and star history
- Handle authentication and tokens
- And more...

By integrating OSP into your CI/CD pipeline through this GitHub Action, you can automate various project management tasks and improve your workflow efficiency.

## Usage

## Community Planning Updater

The following example demonstrates how to use `elliotxx/osp-action` to track milestones and issues in your repository. This workflow triggers on milestone and issue events, allowing you to automate updates and planning based on changes to these elements.

```yaml
name: Community Planning Updater

on:
  # Trigger on milestone events
  milestone:
    types: [created, edited, deleted]
  # Trigger on issue events
  issues:
    types: [opened, edited, deleted, transferred, milestoned, demilestoned, labeled, unlabeled, assigned, unassigned]

jobs:
  osp-run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate Milestone Planning
        uses: elliotxx/osp-action@main
        with:
          # Optional: version of OSP to use (default: latest)
          version: 'latest'
          
          # Optional: working directory (default: project root)
          working-directory: '.'
          
          # Optional: GitHub token (default: ${{ github.token }})
          github-token: ${{ secrets.GITHUB_TOKEN }}
          
          # Optional: enable debug mode (default: false)
          debug: false
          
          # Optional: skip caching (default: false)
          skip-cache: false
          
          # Optional: additional OSP arguments
          args: 'plan --yes --categories bug,documentation,enhancement'
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `version` | Version of OSP to use (v1.2.3 or 'latest') | No | `latest` |
| `working-directory` | Working directory for OSP commands | No | Project root |
| `github-token` | GitHub token for authentication | No | `${{ github.token }}` |
| `skip-cache` | Skip all caching functionality | No | `false` |
| `debug` | Enable debug mode for verbose output | No | `false` |
| `args` | Additional OSP command line arguments | No | `""` |

## Example usage with debug mode

```yaml
- name: Run OSP with debug
  uses: elliotxx/osp-action@main
  with:
    debug: true
    args: 'plan --yes'
```

This will show verbose output including:
- Authentication status and token source
- API calls and responses
- Command execution details

## Features

- **CI/CD Integration**: Seamlessly integrate OSP into your GitHub Actions workflow
- **Version Management**: Specify any version of OSP to use
- **Performance**: Built-in caching for faster execution
- **Flexible**: Supports all OSP command line arguments
- **Secure**: Uses GitHub token for authentication
- **Customizable**: Configure working directory and more

## License

MIT
