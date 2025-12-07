# Pull Requests & Branching Guide

Manage PRs, reviews, and issue-driven development.

[← Back to Main Menu](./README.md)

## 1. Pull Requests (`gh pr`)

Manage pull requests: list, checkout, create, review, merge.

### List Pull Requests

```bash
gh pr list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists open pull requests.

### Checkout a Pull Request

```bash
gh pr checkout 456
```

* **Explanation**: Checks out the branch associated with PR #456 locally. This is extremely useful for testing changes.
* **Note**: Run this inside the cloned repository directory.

### Create a Pull Request

```bash
gh pr create
```

* **Explanation**: Creates a PR from your current branch. Opens an interactive prompt to fill in title and body.
* **Flags**: `--title "Fix: typo" --body "Fixed a typo in README"` to skip prompts.

### Review a Pull Request

```bash
gh pr review 456
```

* **Explanation**: Starts a review for PR #456. You can approve, request changes, or comment.

### Merge a Pull Request

```bash
gh pr merge 456
```

* **Explanation**: Merges PR #456. It will ask for the merge strategy (merge, squash, rebase).
* **Auto-merge**: `gh pr merge 456 --auto --squash` enables auto-merge when checks pass.

---

## 2. Branch Management & Development

While standard `git` commands (like `git checkout -b`) are used for traditional branching, `gh` streamlines bridging issues and PRs with branches.

### Issue-Driven Branching (`gh issue develop`)

Create a branch directly from an issue. This automatically links the branch to the issue.

```bash
# Create a branch for issue #123 (uses default naming convention)
gh issue develop 123 --checkout
```

* **Custom Name**: `gh issue develop 123 --name "feat/login-fix" --checkout`
* **Benefit**: When you later create a PR from this branch, it will automatically reference the issue.

### Checkout Pull Request Branches (`gh pr checkout`)

Testing someone else's code is the most common use case.

```bash
gh pr checkout 456
```

* **Explanation**: Fetches and switches to the branch associated with PR #456. It manages the remote configurations for you automatically.

### Standard Git Integration

Since `gh` works alongside `git`, you continue to use standard commands for local management:

* `git switch -c new-branch` (Create new branch)
* `git branch` (List branches)
* `gh repo sync` (Syncs your current branch with the upstream remote)
