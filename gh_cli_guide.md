# GitHub CLI (`gh`) Guide

This guide provides a comprehensive overview of the GitHub CLI (`gh`) tool, with examples tailored for the repository:
`https://github.com/EOPF-Sample-Service/GDAL-ZARR-EOPF`

## Table of Contents

1. [Introduction](#1-introduction)
2. [Installation & Authentication](#2-installation--authentication)
3. [Core Commands](#3-core-commands)
    * [Repositories](#repositories-gh-repo)
    * [Issues](#issues-gh-issue)
    * [Pull Requests](#pull-requests-gh-pr)
    * [Workflows & Actions](#workflows--actions-gh-workflow-gh-run)
    * [Branch Management](#branch-management--development)
    * [Project Planning](#project-planning-gh-project)
    * [Gists](#gists-gh-gist)
4. [Advanced Usage](#4-advanced-usage)
    * [Aliases](#aliases-gh-alias)
    * [API](#api-gh-api)
    * [Milestones & Workflows](#milestones--workflows)
    * [Config](#config-gh-config)
5. [Quick Reference Table](#5-quick-reference-table)
6. [Tips for GDAL-ZARR-EOPF](#6-tips-for-gdal-zarr-eopf)

## 1. Introduction

`gh` is GitHub's official command-line tool. It brings pull requests, issues, and other GitHub concepts to the terminal next to where you are already working with `git`.

## 2. Installation & Authentication

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

## 3. Core Commands

### Repositories (`gh repo`)

Manage repositories: create, clone, fork, view, etc.

#### Clone a Repository

```bash
gh repo clone EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Clones the specified repository to your local machine.

#### View Repository Details

```bash
gh repo view EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Displays the README and description of the repository in the terminal.
* **Web**: Add `--web` or `-w` to open it in your browser.

#### Fork a Repository

```bash
gh repo fork EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Creates a fork of the repository under your account and optionally clones it.

#### Sync a Fork

```bash
gh repo sync EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Syncs your fork with the upstream repository.

---

### Issues (`gh issue`)

Manage issues: list, view, create, comment, and manage lifecycle.

#### 1. List Issues (`gh issue list`)

List issues in the repository. By default, it lists open issues.

**Basic Usage:**

```bash
gh issue list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

**Filtering Options:**

* **By State (`--state`)**:
  * `gh issue list --state open` (Default)
  * `gh issue list --state closed` (View closed issues)
  * `gh issue list --state all` (View both open and closed)

* **By Assignee (`--assignee`)**:
  * `gh issue list --assignee "@me"` (Issues assigned to you)
  * `gh issue list --assignee "username"` (Issues assigned to specific user)
  * `gh issue list --search "no:assignee"` (Issues with no assignee)

* **By Author (`--author`)**:
  * `gh issue list --author "username"` (Issues created by specific user)
  * `gh issue list --author "@me"` (Issues created by you)

* **By Label (`--label`)**:
  * `gh issue list --label "bug"` (Issues with 'bug' label)
  * `gh issue list --label "enhancement" --label "help wanted"` (Issues with BOTH labels)

* **By Milestone (`--milestone`)**:
  * `gh issue list --milestone "v1.0"` (Issues in specific milestone)

* **Advanced Search (`--search`)**:
    Uses GitHub's search syntax.
  * `gh issue list --search "error no:assignee sort:created-asc"` (Oldest unassigned error issues)
  * `gh issue list --search "is:open is:issue label:bug -label:wontfix"` (Open bugs that are not 'wontfix')

* **Web View (`--web`)**:
  * `gh issue list --web` (Opens the list in your browser)

#### 2. View an Issue (`gh issue view`)

Display the title, body, and metadata of an issue.

```bash
gh issue view 123
```

* **View Comments**: `gh issue view 123 --comments` (Shows the discussion thread)
* **Open in Browser**: `gh issue view 123 --web`

#### 3. Create an Issue (`gh issue create`)

Create a new issue.

**Interactive Mode:**

```bash
gh issue create
```

(Follow the prompts to select template, title, and body)

**Command Line Flags:**

```bash
gh issue create \
  --title "Bug: Application crashes on start" \
  --body "Steps to reproduce: 1. Run app 2. Crash" \
  --label "bug" \
  --assignee "@me" \
  --milestone "v1.0"
```

#### 4. Manage Issues

Commands to modify existing issues.

* **Comment**: Add a comment to an issue.

    ```bash
    gh issue comment 123 --body "I am looking into this."
    ```

* **Close**: Close an issue.

    ```bash
    gh issue close 123 --comment "Fixed in v1.0.1"
    ```

* **Reopen**: Reopen a closed issue.

    ```bash
    gh issue reopen 123
    ```

* **Edit**: Edit title, body, or reviewers.

    ```bash
    gh issue edit 123 --add-label "priority-high" --remove-label "triage"
    ```

* **Lock**: Lock conversation on an issue.

    ```bash
    gh issue lock 123 --reason "resolved"
    ```

---

### Pull Requests (`gh pr`)

Manage pull requests: list, checkout, create, review, merge.

#### List Pull Requests

```bash
gh pr list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists open pull requests.

#### Checkout a Pull Request

```bash
gh pr checkout 456
```

* **Explanation**: Checks out the branch associated with PR #456 locally. This is extremely useful for testing changes.
* **Note**: Run this inside the cloned repository directory.

#### Create a Pull Request

```bash
gh pr create
```

* **Explanation**: Creates a PR from your current branch. Opens an interactive prompt to fill in title and body.
* **Flags**: `--title "Fix: typo" --body "Fixed a typo in README"` to skip prompts.

#### Review a Pull Request

```bash
gh pr review 456
```

* **Explanation**: Starts a review for PR #456. You can approve, request changes, or comment.

#### Merge a Pull Request

```bash
gh pr merge 456
```

* **Explanation**: Merges PR #456. It will ask for the merge strategy (merge, squash, rebase).
* **Auto-merge**: `gh pr merge 456 --auto --squash` enables auto-merge when checks pass.

---

### Workflows & Actions (`gh workflow`, `gh run`)

Interact with GitHub Actions.

#### List Workflows

```bash
gh workflow list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists all active workflow files in the repository.

#### View Workflow Runs

```bash
gh run list --workflow "CI" --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists recent runs for the workflow named "CI".

#### Watch a Run

```bash
gh run watch
```

* **Explanation**: Watches the progress of the most recent workflow run in the terminal until it finishes.

#### View Logs

```bash
gh run view --log
```

* **Explanation**: View the logs of the most recent run.

---

### Branch Management & Development

While standard `git` commands (like `git checkout -b`) are used for traditional branching, `gh` streamlines bridging issues and PRs with branches.

#### 1. Issue-Driven Branching (`gh issue develop`)

Create a branch directly from an issue. This automatically links the branch to the issue.

```bash
# Create a branch for issue #123 (uses default naming convention)
gh issue develop 123 --checkout
```

* **Custom Name**: `gh issue develop 123 --name "feat/login-fix" --checkout`
* **Benefit**: When you later create a PR from this branch, it will automatically reference the issue.

#### 2. Checkout Pull Request Branches (`gh pr checkout`)

Testing someone else's code is the most common use case.

```bash
gh pr checkout 456
```

* **Explanation**: Fetches and switches to the branch associated with PR #456. It manages the remote configurations for you automatically.

#### 3. Standard Git Integration

Since `gh` works alongside `git`, you continue to use standard commands for local management:

* `git switch -c new-branch` (Create new branch)
* `git branch` (List branches)
* `gh repo sync` (Syncs your current branch with the upstream remote)

---

### Project Planning (`gh project`)

Manage GitHub Projects (Projects V2). Projects are often used for roadmap planning and task tracking at the organization or user level.

#### List Projects

List projects for the organization `EOPF-Sample-Service`.

```bash
gh project list --owner EOPF-Sample-Service
```

* **Result**: Displays the Title and Number (ID) of available projects.

#### View a Project

View the board or table of a specific project.

```bash
gh project view 1 --owner EOPF-Sample-Service
```

* **Explanation**: Views project #1.
* **Web**: `gh project view 1 --owner EOPF-Sample-Service --web` (Opens in browser, which is the best way to visualize the board).

#### Manage Project Items

You can add issues or Pull Requests to projects.

* **List Items**: See what's on the board.

    ```bash
    gh project item-list 1 --owner EOPF-Sample-Service
    ```

* **Add Item**: Add an issue to a project.

    ```bash
    # First, get the Issue URL or ID, e.g., https://github.com/EOPF-Sample-Service/GDAL-ZARR-EOPF/issues/123
    gh project item-create 1 --owner EOPF-Sample-Service --url "https://github.com/EOPF-Sample-Service/GDAL-ZARR-EOPF/issues/123"
    ```

* **Edit Item**: specific fields (like Status).

    ```bash
    # You need the Item ID from `item-list`
    gh project item-edit --id <item-id> --field-id <status-field-id> --project-id <project-id>
    ```

    *Note: Editing project items via CLI can be complex because it requires knowing internal IDs. It is often easier to use the `--web` flag to manage the board visually.*

---

### Gists (`gh gist`)

Manage code snippets.

#### Create a Gist

```bash
gh gist create script.py
```

* **Explanation**: Creates a gist from the file `script.py`.

## 4. Advanced Usage

### Aliases (`gh alias`)

Create shortcuts for common commands.

```bash
gh alias set co "pr checkout"
```

* **Usage**: `gh co 123` is now the same as `gh pr checkout 123`.

### API (`gh api`)

Make direct calls to the GitHub API.

```bash
gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/languages
```

* **Explanation**: Fetches the languages used in the repository via the API.

### Milestones & Workflows

This section covers how to effectively use Milestones to track progress, filter issues, and manage releases.

#### 1. Viewing Milestones

To see what milestones exist and their status (open/closed, due dates).

```bash
gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones --jq '.[] | {title: .title, state: .state, due_on: .due_on, open_issues: .open_issues}'
```

#### 2. Working with Issues in Milestones

The power of milestones comes from filtering issues.

**Basic Filtering:**

* **Show all issues in v1.0:**

    ```bash
    gh issue list --milestone "v1.0"
    ```

**Advanced Workflows (Recipes):**

* **"The Show Stoppers"** (Critical bugs in the current milestone):
    Find all open issues in milestone "v1.0" with the label "bug" or "critical".

    ```bash
    gh issue list --milestone "v1.0" --label "bug"
    ```

* **"My Tasks for this Release"** (What do I need to do?):
    Find all open issues in "v1.0" assigned to me.

    ```bash
    gh issue list --milestone "v1.0" --assignee "@me"
    ```

* **"Unassigned Work"** (What needs to be picked up?):
    Find issues in "v1.0" that no one is working on yet.

    ```bash
    gh issue list --milestone "v1.0" --search "no:assignee"
    ```

* **"The Burndown"** (What is left?):
    View all open issues in the milestone, sorted by oldest creation date.

    ```bash
    gh issue list --milestone "v1.0" --search "sort:created-asc"
    ```

* **"Progress Check"**:
    View both closed and open issues to see completion status.

    ```bash
    gh issue list --milestone "v1.0" --state all
    ```

#### 3. Managing Milestones (via API)

Since `gh` lacks a top-level `milestone` command, use `gh api`.

* **Create a Milestone:**

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones \
      -f title="v1.0" \
      -f description="First major release" \
      -f due_on="2025-12-31T00:00:00Z"
    ```

* **Close a Milestone:**
    (Requires the milestone number, e.g., `1`)

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones/1 -X PATCH -f state="closed"
    ```

* **Delete a Milestone:**

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones/1 -X DELETE
    ```

### Config (`gh config`)

Configure `gh` behavior.

```bash
gh config set editor "code --wait"
```

* **Explanation**: Sets VS Code as the default editor for `gh` (e.g., for writing PR descriptions).

## 5. Quick Reference Table

| Command | Description | Example |
| :--- | :--- | :--- |
| `gh auth login` | Authenticate with GitHub | `gh auth login` |
| `gh repo clone` | Clone a repo | `gh repo clone owner/repo` |
| `gh repo view` | View repo details | `gh repo view owner/repo` |
| `gh issue list` | List issues | `gh issue list` |
| `gh issue create` | Create an issue | `gh issue create` |
| `gh pr list` | List pull requests | `gh pr list` |
| `gh pr checkout` | Checkout a PR branch | `gh pr checkout <number>` |
| `gh pr create` | Create a PR | `gh pr create` |
| `gh pr merge` | Merge a PR | `gh pr merge <number>` |
| `gh run list` | List workflow runs | `gh run list` |
| `gh run watch` | Watch a workflow run | `gh run watch` |
| `gh browse` | Open in browser | `gh browse` |

## 6. Tips for `sample-repo`

* **Context Awareness**: If you are inside the `sample-repo` directory, you can omit the `--repo sample-repo` flag. `gh` automatically detects the repository from the git remote.
* **Filtering**: Since this repo might have specific labels (e.g., `bug`, `enhancement`), use `gh issue list --label "bug"` to focus on what matters.
* **CI Monitoring**: Use `gh run watch` after pushing changes to see if the CI pipeline passes without leaving your terminal.
