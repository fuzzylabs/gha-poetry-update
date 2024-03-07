# Automated Dependency Updates with Poetry 📦

A GitHub action to run [`poetry update`](https://python-poetry.org/docs/cli/#update).

Can be used in workflow which would automatically creates a pull request when updates to one or more dependencies are available.

The Poetry update action will:
1. Checkout the caller repository and set up Python.
2. Install and configure poetry.
3. Check whether there is a `poetry.lock` file in the caller repository, skip update if not.
4. Run `poetry update`.
5. Create a PR with a description showing the updated dependencies.


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
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main
```

 ### Handling Private Dependencies Example 🔐

If your poetry package installs dependencies from one or more private repository, you will need to configure the SSH key required to access these repositories.

For more information on how to add SSH keys, please refer to Usage section of webfactory/ssh-agent github action.

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
        - uses: webfactory/ssh-agent@v0.9.0
          with:
            ssh-private-key: |
              ${{ secrets.<SSH_PRIVATE_KEY_1> }}
              ${{ secrets.<SSH_PRIVATE_KEY_2> }}
    
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main
```