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
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main
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
    
        - uses: git@github.com:fuzzylabs/gha-poetry-update.git@main
```

currentver="3.10.0"
requiredver="5.0.0"
test="$(printf '%s\n' "$requiredver" "$currentver" | sort -V)"
echo $test

 if [ "$(printf '%s\n' "$requiredver" "$currentver" | sort -V | head -n1)" = "$requiredver" ]; then 
        echo "Greater than or equal to ${requiredver}"
 else
        echo "Less than ${requiredver}"
 fi

        min_python_version="3.10.0"
        min_poetry_version="1.5.0"
        if [ "$(printf '%s\n' "$min_python_version" "$inputs.python-version" | sort -V | head -n1)" = "$min_python_version" ]; then
          echo "Greater than or equal to ${requiredver}"
        else
          echo "Less than ${requiredver}"
        fi