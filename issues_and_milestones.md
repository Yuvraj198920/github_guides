# Issues & Milestones Guide

Manage issues, filter them effectively, and handle release planning.

[← Back to Main Menu](./README.md)

## 1. Issues (`gh issue`)

Manage issues: list, view, create, comment, and manage lifecycle.

### List Issues (`gh issue list`)

List issues in the repository. By default, it lists open issues.

**Basic Usage:**

```bash
gh issue list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

### Filtering Options

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

### View an Issue (`gh issue view`)

Display the title, body, and metadata of an issue.

```bash
gh issue view 123
```

* **View Comments**: `gh issue view 123 --comments` (Shows the discussion thread)
* **Open in Browser**: `gh issue view 123 --web`

### Create an Issue (`gh issue create`)

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

### Manage Issues

Commands to modify existing issues.

* **Comment**: `gh issue comment 123 --body "I am looking into this."`
* **Close**: `gh issue close 123 --comment "Fixed in v1.0.1"`
* **Reopen**: `gh issue reopen 123`
* **Edit**: `gh issue edit 123 --add-label "priority-high" --remove-label "triage"`
* **Lock**: `gh issue lock 123 --reason "resolved"`

---

## 2. Milestones & Workflows

This section covers how to effectively use Milestones to track progress, filter issues, and manage releases.

### Viewing Milestones

To see what milestones exist and their status (open/closed, due dates).

```bash
gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones --jq '.[] | {title: .title, state: .state, due_on: .due_on, open_issues: .open_issues}'
```

### Working with Issues in Milestones

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

### Managing Milestones (via API)

Since `gh` lacks a top-level `milestone` command, use `gh api`.

* **Create a Milestone:**

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones \
      -f title="v1.0" \
      -f description="First major release" \
      -f due_on="2025-12-31T00:00:00Z"
    ```

* **Close a Milestone:** (Requires the milestone number, e.g., `1`)

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones/1 -X PATCH -f state="closed"
    ```

* **Delete a Milestone:**

    ```bash
    gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/milestones/1 -X DELETE
    ```
