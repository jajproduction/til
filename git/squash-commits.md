# Squash Commits

Git squash is a technique used to combine multiple commits into a single commit. This is often done to simplify the commit history, particularly when working on feature branches with numerous small, incremental commits.

Let's start by `rebase` the `HEAD~3` represents the number of recent commits, change the value if needed. Also the `HEAD~3` will not work in your master branch (based on my experience) make sure that you are doing this on a separate branch.

```sh
git rebase i- HEAD~3
```

After you execute the command you will see this:

```sh
pick 857fb4e feat(docs): added hope.
pick 68d69d7 feat(docs): added another sentence.
pick a297a23 feat(docs): added headline.

# Rebase 69e158e..a297a23 onto 69e158e (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

Change them to this:

```sh
pick 857fb4e feat(docs): added hope.
squash 68d69d7 feat(docs): added another sentence.
squash a297a23 feat(docs): added headline.

# Rebase 69e158e..a297a23 onto 69e158e (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

Save and quit, then another will open like this:

```sh
# This is a combination of 3 commits.
# This is the 1st commit message:

feat(docs): added hope.

# This is the commit message #2:

feat(docs): added another sentence.

# This is the commit message #3:

feat(docs): added headline.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Mon May 5 14:29:10 2025 +0800
#
# interactive rebase in progress; onto 69e158e
# Last commands done (3 commands done):
#    squash 68d69d7 feat(docs): added another sentence.
#    squash a297a23 feat(docs): added headline.
# No commands remaining.
# You are currently rebasing branch 'bugs' on '69e158e'.
#
# Changes to be committed:
#       modified:   test.md
#
```

Change them to this by adding hash on the commits:

```sh
# This is a combination of 3 commits.
# This is the 1st commit message:

feat(docs): added hope.

# This is the commit message #2:

# feat(docs): added another sentence.

# This is the commit message #3:

# feat(docs): added headline.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Mon May 5 14:29:10 2025 +0800
#
# interactive rebase in progress; onto 69e158e
# Last commands done (3 commands done):
#    squash 68d69d7 feat(docs): added another sentence.
#    squash a297a23 feat(docs): added headline.
# No commands remaining.
# You are currently rebasing branch 'bugs' on '69e158e'.
#
# Changes to be committed:
#       modified:   test.md
#
```

And done, we are good to go, ready to push!
