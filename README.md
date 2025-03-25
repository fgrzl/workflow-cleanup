# Cleanup Workflow History Action

This GitHub Action deletes old workflow runs from your repository based on their age. It’s perfect for keeping your Actions history clean and manageable.

## Inputs

| Name       | Description                                            | Required | Default |
|------------|--------------------------------------------------------|----------|---------|
| `days_old` | Number of days to keep workflow runs                   | No       | `7`     |
| `per_page` | Number of workflow runs to fetch per request (max 100) | No       | `50`    |

## Example Usage

Add this to your workflow file (e.g., `.github/workflows/cleanup.yml`):

```yaml
name: Clean Up Old Workflow Runs

on:
  schedule:
    - cron: '0 0 * * *' # Runs daily at midnight UTC
  workflow_dispatch: # Allows manual triggering

jobs:
  cleanup:
    runs-on: ubuntu-latest
    steps:
      - name: Delete Old Workflow Runs
        uses: fgrzl/workflow-cleanup@v1
        with:
          days_old: 14 # Delete runs older than 14 days
          per_page: 100 # Fetch up to 100 runs at a time
```