# Repositories & Starting from Scratch

Learn how to create, clone, fork, and sync repositories.

[← Back to Main Menu](./README.md)

## 1. Starting from Scratch (`gh repo create`)

You can create a new repository from scratch or from an existing local project.

### Create a New Empty Repository

Create a new remote repository and clone it to your machine immediately.

```bash
# Create a public repository named "my-new-project"
gh repo create my-new-project --public --clone
```

* **Flags**:
  * `--public`, `--private`, or `--internal`.
  * `--clone`: Clones it locally after creation.
  * `--add-readme`: Adds a default README.

### Push an Existing Local Project

If you have a folder with code that isn't on GitHub yet:

1. Navigate to your project folder: `cd my-existing-project`
2. Run the create command with `--source=.`:

    ```bash
    gh repo create --source=. --public --push
    ```

    * **Explanation**: Creates a repo on GitHub with the same name as your folder, connects the remote, and pushes your code.

---

## 2. Core Repository Commands

### Clone (`gh repo clone`)

Download a repository from GitHub.

```bash
gh repo clone EOPF-Sample-Service/GDAL-ZARR-EOPF
```

### View (`gh repo view`)

See the README and metadata in your terminal.

```bash
gh repo view EOPF-Sample-Service/GDAL-ZARR-EOPF
```

* **Web**: `gh repo view --web` (Opens in browser).

### Fork (`gh repo fork`)

Create a copy of a repository under your own account.

```bash
gh repo fork EOPF-Sample-Service/GDAL-ZARR-EOPF --clone
```

* **--clone**: Clones your new fork immediately.

### Sync (`gh repo sync`)

Keep your fork up to date with the original upstream repository.

```bash
gh repo sync
```

* **Context**: Run this inside your local fork directory. It fetches changes from the upstream and merges them into your branch.
