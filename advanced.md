# Advanced Usage & CI Guide

Master `gh` with API calls, configuration, and CI monitoring.

[← Back to Main Menu](./README.md)

## 1. Workflows & Actions (`gh workflow`, `gh run`)

Interact with GitHub Actions.

### List Workflows

```bash
gh workflow list --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists all active workflow files in the repository.

### View Workflow Runs

```bash
gh run list --workflow "CI" --repo EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Explanation**: Lists recent runs for the workflow named "CI".

### Watch a Run

```bash
gh run watch
```

* **Explanation**: Watches the progress of the most recent workflow run in the terminal until it finishes.

### View Logs

```bash
gh run view --log
```

* **Explanation**: View the logs of the most recent run.

---

## 2. API (`gh api`)

Make direct calls to the GitHub API.

```bash
gh api repos/EOPF-Sample-Service/GDAL-ZARR-EOPF/languages
```

* **Explanation**: Fetches the languages used in the repository via the API.

---

## 3. Aliases (`gh alias`)

Create shortcuts for common commands.

```bash
gh alias set co "pr checkout"
```

* **Usage**: `gh co 123` is now the same as `gh pr checkout 123`.

---

## 4. Config (`gh config`)

Configure `gh` behavior.

```bash
gh config set editor "code --wait"
```

* **Explanation**: Sets VS Code as the default editor for `gh` (e.g., for writing PR descriptions).
