# Project Planning Guide

Manage GitHub Projects (Projects V2) for roadmap planning and task tracking.

[← Back to Main Menu](./README.md)

## Project Planning (`gh project`)

Manage GitHub Projects (Projects V2). Projects are often used for roadmap planning and task tracking at the organization or user level.

### List Projects

List projects for the organization `EOPF-Sample-Service`.

```bash
gh project list --owner EOPF-Sample-Service
```

* **Result**: Displays the Title and Number (ID) of available projects.

### View a Project

View the board or table of a specific project.

```bash
gh project view 1 --owner EOPF-Sample-Service
```

* **Explanation**: Views project #1.
* **Web**: `gh project view 1 --owner EOPF-Sample-Service --web` (Opens in browser, which is the best way to visualize the board).

### Manage Project Items

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
