# GitHub CLI (`gh`) Guide

Welcome to the comprehensive guide for using the GitHub CLI (`gh`), tailored for the repository:
`https://github.com/EOPF-Sample-Service/GDAL-ZARR-EOPF`

## Table of Contents

* [**Setup & Authentication**](#setup--authentication)
* **[Repositories & Starting from Scratch](./repositories.md)**: Create new repos, clone, fork, and sync.
* **[Issues & Milestones](./issues_and_milestones.md)**: Manage issues, filters, and release recipes.
* **[Pull Requests & Branching](./pr_and_branching.md)**: PR workflows, code reviews, and issue-driven branching.
* **[Project Planning](./projects.md)**: Managing GitHub Projects V2.
* **[Advanced Usage & CI](./advanced.md)**: API, Config, Aliases, and Actions monitoring.
* **[Cheatsheet](./cheatsheet.md)**: Quick reference table.

---

## 1. Introduction

`gh` is GitHub's official command-line tool. It brings pull requests, issues, and other GitHub concepts to the terminal next to where you are already working with `git`.

## 2. Setup & Authentication

Before using `gh`, you need to authenticate.

### Authenticate

```bash
gh auth login
```

* **Explanation**: Starts the interactive login process. You'll choose between GitHub.com or Enterprise, and HTTPS or SSH.
* **Tip**: Select "Login with a web browser" for the easiest experience.

### Check Status

```bash
gh auth status
```

* **Explanation**: Shows which account you are logged into and which configuration is active.

## 3. Tips for `sample-repo`

* **Context Awareness**: If you are inside the `sample-repo` directory, you can omit the `--repo sample-repo` flag. `gh` automatically detects the repository from the git remote.
* **Filtering**: Since this repo might have specific labels (e.g., `bug`, `enhancement`), use `gh issue list --label "bug"` to focus on what matters.
* **CI Monitoring**: Use `gh run watch` after pushing changes to see if the CI pipeline passes without leaving your terminal.
