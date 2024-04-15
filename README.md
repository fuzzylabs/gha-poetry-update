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
    
        - uses: fuzzylabs/gha-poetry-update@v1
```

## Action inputs

All inputs are **optional**. If not set, sensible defaults will be used.

| Name | Description | Default |
| --- | --- | --- |
| `python-version` | The python version to use with poetry, the minimum version required is >=3.10 | 3.10.12 |
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

This action can also be used on repositories which contain multiple projects in different directories. The following example shows a workflow in which the action updates dependencies in projects in directories `project1/` `project2` and `project3`.

If dependencies are updated in one or more of these projects, a separate pull request
will be generated for each of the updated projects.

```yaml
name: Poetry Update

on:
  # Run weekly on Monday at 0700AM
  schedule:
    - cron: "0 7 * * MON"
  # Allow a manual trigger
  workflow_dispatch:

jobs:
  auto-update:
    runs-on: ubuntu-latest
    strategy:
        matrix: { directory: ['project1/', 'project2/', 'project3/'] }
    steps:
      - uses: fuzzylabs/gha-poetry-update@v1
        with:
          python-version: "3.10"
          directory: ${{ matrix.directory }}

```
_Note: We do not explicitly support this action with Python <=3.10.4. Though Python 3.10 is checked for as a minimum requirement, this is to capture workflows which set version generically to 3.10.X specifying only major and minor release numbers._