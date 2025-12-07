# Commits & History

Search, view, and manage commit history.

[← Back to Main Menu](./README.md)

## 1. Searching Commits (`gh search commits`)

`gh` excels at finding specific commits across the repository using powerful search filters.

### Search by Keyword

Find commits containing specific words in the message.

```bash
gh search commits "memory leak"
```

### Search by Author

Find commits by a specific user.

```bash
gh search commits --author "username"
```

* **Combined**: `gh search commits "memory leak" --author "username"`

### Search by Hash

Find a commit by its SHA hash.

```bash
gh search commits --hash "8dd0314"
```

---

## 2. Git Basics for Commits

For managing the history (viewing diffs, reverting changes), use standard `git` commands. `gh` focuses on the "social" and search aspects.

### View History (`git log`)

See the lists of commits.

```bash
git log --oneline -n 10
```

* **Explanation**: Shows the last 10 commits in a concise format.

### View a Commit (`git show`)

See the exact changes (diff) of a commit.

```bash
git show <commit_hash>
```

### Revert a Commit (`git revert`)

Create a *new* commit that undoes the changes of a previous commit. This is the safe way to undo changes in public branches.

```bash
git revert <commit_hash>
```

### Delete/Undo Recent Commits (`git reset`)

**Warning**: This changes history. Only use this on your local private branch, never on shared branches like `main`.

* **Soft Reset**: Undoes the commit but keeps your changes in the file system (staged).

    ```bash
    git reset --soft HEAD~1
    ```

* **Hard Reset**: DESTROYS the last commit and all changes.

    ```bash
    git reset --hard HEAD~1
    ```
