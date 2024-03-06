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
        - name: Check out repository
          uses: actions/checkout@v4

        - name: Set up python
          uses: actions/setup-python@v4
          with:
            python-version: '3.10'
        
        #---------------------------------------------------------------------------
        # If installing a dependencies from private repo, add SSH private key here
        #---------------------------------------------------------------------------
        - uses: webfactory/ssh-agent@v0.9.0
          with:
            ssh-private-key: |
              ${{ secrets.<SSH_PRIVATE_KEY> }}
    
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main

        #----------------------------------------------
        #              Create a pull request
        #----------------------------------------------
        - name: Create Pull Request
        uses: peter-evans/create-pull-request@v6
        with:
            token: ${{ secrets.GITHUB_TOKEN }}
            branch: update/poetry-update
            title: Update poetry dependencies
            commit-message: "Chore(deps): Upgrading `poetry` dependencies"
            body: |
            Update `poetry` dependencies to use latest compatible versions.

            **Outdated packages**:
                ${{ env.UPDATE_MESSAGE }}
```