# Delete Latest Commit

To delete your latest commit locally so that you can pull changes first, you can use the following steps:

1. **Soft reset your latest commit** (this will remove the commit but keep your changes in the working directory):

```bash
git reset --soft HEAD~1
```

This command undoes the last commit but leaves your changes staged. After this, you can pull the changes from the remote repository.

2. **Pull the latest changes** from the remote repository:

```bash
git pull
```

3. After pulling, you can now **recommit your changes**:

```bash
git commit -m 'your commit message'
```

4. Finally, you can **push the changes**:

```bash
git push
```

This way, you don’t lose your work, and you can successfully pull and push without conflicts.
