# Automated Dependency Updates with Poetry 📦

A GitHub action to run [`poetry update`](https://python-poetry.org/docs/cli/#update).

Can be used in workflow which would automatically creates a pull request when updates to one or more dependencies are available.

The Poetry update action will:
1. Checkout the caller repository and set up Python.
2. Install and configure poetry.
3. Check whether there is a `poetry.lock` file in the caller repository, skip update if not.
4. Run `poetry update`.
5. Create a PR with a description showing the updated dependencies.

This action is currently compatible only with Python version 3.10 and will install Poetry version 1.8.2.

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
        - uses: fuzzylabs/gha-poetry-update@v1
```

 ### Handling Private Dependencies Example 🔐

If your poetry package installs dependencies from one or more private repository, you will need to configure the SSH key required to access these repositories.

For more information on how to add SSH keys, please refer to Usage section of [webfactory/ssh-agent](https://github.com/webfactory/ssh-agent?tab=readme-ov-file#usage) github action.

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
    
        - uses: fuzzylabs/gha-poetry-update.git@v1
```

## Action inputs

All inputs are **optional**. If not set, sensible defaults will be used.

| Name | Description | Default |
| --- | --- | --- |
| `python-version` | The python version to use with poetry, the minimum version required is >=3.10.5 | 3.10.12 |
| `poetry-version` | The poetry version to use | 1.8.2 |

### Example

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
        - uses: fuzzylabs/gha-poetry-update@v1
          with:
            python-version: '3.10.12'
            poetry-version: '1.8.2'
```