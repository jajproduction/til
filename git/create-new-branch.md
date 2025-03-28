# Create New Branch

1. Create a new branch

```sh
git checkout -b new-branch-name
```

This creates and switches to the new branch.

2. Make changes (if needed)

Modify files, add commits, etc.

3. Push the branch to GitHub

```sh
git push -u origin new-branch-name
```

The `-u` (or `--set-upstream`) flag sets the upstream branch so that future `git push` and `git pull` commands default to `origin new-branch-name`.

After this, your new branch will be available on GitHub.
