# 🧑‍💻 Contributing to `gha-poetry-update`

Welcome to `gha-poetry-update`! This document contains the instructions on how to contribute to `gha-poetry-update`.

## 🔥 Quicklinks

* [Getting Started](#🎬-getting-started)
  * [Issues](#😭-issues)
  * [Pull Requests](#🎫-pull-requests)

## 🎬 Getting started

Contributions are made to this project using Issues and Pull Request (PRs). Before creating your own, search for existing Issues and PRs - as I'm sure you're aware, this removes duplication and makes everyone's life easier!

### 😭 Issues

Issues should be used to report bugs with `gha-poetry-update`, proposing new features before a PR is raised, and to request new features. We're making use of templates to make this process easier for you and consistent for everyone - this will appear when you create an issue.

If you find an issue that has already been reported by another good samaritan, then please add your own reproduction information to the existing issue rather than creating a new one. Reacting to issues can also help our maintainers understand that the issue is affecting more than one reporter.

### 🎫 Pull Requests

Pull Requests (PRs) are how contributions are made to `gha-poetry-update` and are always welcome.

The preferred way to contribute to `gha-poetry-update` is to fork the main repository on Github and then submit a pull request.

#### 🖥️ Getting setup locally

Here, we'll explain to get setup locally with `gha-poetry-update` and how to set up your git repository:

1. If you don't already have one, [create an account](https://github.com/join) on Github.

2. Fork the repository by clicking on the 'fork' button near the top of the page. What this will do is create a copy of the `gha-poetry-update` repository under your Github account. See [here](https://help.github.com/articles/fork-a-repo/) for a guide on how to fork a repository.

3. Clone this forked version of `gha-poetry-update` to your local disk:

```bash
git clone git@github.com:<your_username>/gha-poetry-update.git
cd `gha-poetry-update`
```

4. Add the `upstream` remote. Adding this means you can keep your repository sync'd with the latest changes to the main repository:

```bash
git remote add upstream git@github.com:fuzzylabs/gha-poetry-update.git
```

5. Check that these remote aliases are correctly configured by running: `git remote -v`, this should show the following:

```bash
origin  git@github.com:<your_username>/gha-poetry-update.git (fetch)
origin  git@github.com:<your_username>/gha-poetry-update.git (push)
upstream        git@github.com:fuzzylabs/gha-poetry-update.git (fetch)
upstream        git@github.com:fuzzylabs/gha-poetry-update.git (push)
```

6. Sync your `main` branch with the `upstream/main` branch:

```bash
git checkout main
git fetch upstream
git merge upstream/main
```

7. Create your feature branch which will contain your development changes:

```bash
git checkout -b <your_feature>
```

and you can now start making changes! We're sure that you don't need reminding but it's good practise to never work on the `main` branch and to always use a feature branch.

8. Develop your feature on your computer and when you're done editing, add the changed files to git and then commit:

```bash
git add <modified_files>
git commit -m '<a meaningful commit message>'
```

Once committed, push your changes to your Github account:

```bash
git push -u origin <your_feature>
```

9. Once you're finished and ready to make a pull request to the main repository, then follow the [steps below](#🤔-making-a-pull-request)

#### 🤔 Making a pull request
Before a PR can be merged, two core developers need to approve it. The core developer team handle the review process and will be notified when a new PR is submitted.

It may be the case that you have an incomplete contribution, where you're expecting to do more work before receiving a full review. In this case please use the draft PR functionality within GitHub. These types of PRs often benefit from including a task list in the PR description.