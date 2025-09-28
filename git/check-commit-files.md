# Check Commit Files

1. Check files staged for the next commit (before commiting)

```sh
git diff --cached --name-only
```

This shows the files that will be included when you run `git commit`.

2. Check files in your last commit

```sh
git show --name-only --oneline HEAD
```

3. Check files in a specific commit

```sh
git show --name-only <commit-hash>
```

Replace `<commit-hash>` with the commit ID (from `git log --oneline`).

4. Check what will be pushed to the remote

If you want to see what commits (and their files) haven’t been pushed yet:

```sh
git log origin/main..HEAD --oneline --name-only
```

(replace `main` with your branch name if different)
