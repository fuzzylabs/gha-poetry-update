# GHA Poetry Update

A GitHub action to run `poetry update`.

Can be used in workflow which would automatically creates a pull request when updates to one or more dependencies are available.

## Example

```yaml
name: Poetry Update

on: 
  # Run daily at midnight
  schedule:
    - cron: "0 0 * * *"
  # Allow a manual trigger
  workflow_dispatch:

jobs:
  auto-update:
    runs-on: ubuntu-latest
    steps:
        #---------------------------------------------------------------------------
        # If installing dependencies from private repo, add SSH private key here
        #---------------------------------------------------------------------------
        - uses: webfactory/ssh-agent@v0.9.0
          with:
            ssh-private-key: |
              ${{ secrets.<SSH_PRIVATE_KEY> }}
    
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main
```