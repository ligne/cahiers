# Git

Everyone's favourite VCS.

## Index

### View changes to the index

By default `git diff` only shows *unstaged* changes.
Add `--staged` to see what changes are staged for the next commit, or run `git diff HEAD` to see all changes relative to the last commit.

### Unstage files

This is just a simple `git reset`, or `git reset HEAD -- $file ...` to be more discerning.

## Commits

### Undo the last commit

To undo the most recent commit ready for another try: `git reset --soft HEAD^`.

The old commit will still be available as `ORIG_HEAD`.
Add `-c ORIG_HEAD ...` when committing to use it as the basis of the new message.

### Squashing

In the general case this can be done an interactive rebase, and the last commit can be corrected with `git add ...; git commit --amend [--no-edit]`.
But if the last few commits are a mess that need squashing into one, run `git reset --soft HEAD~n` and prepare the final commit.

## Branches

### Turn commits into a new branch

To turn the most recent commits into a new branch:

```sh
git branch new_branch
git reset --hard HEAD~3  # use the three most recent commits
git switch new_branch
```

### Find merged branches

List all branches that have(n't) been merged into the current branch: `git branch --{,no-}merged`.
Can specify a branch name to use instead, and `-r` and `-a` to show remote or all branches respectively.
[(source)](https://stackoverflow.com/questions/226976/how-can-i-know-if-a-branch-has-been-already-merged-into-master)

### Rename a branch

Change the branch name locally: `git branch --move old-name new-name`.

If it also exists upstream, `git push --set-upstream origin new-name; git push origin --delete old-name`.

## Merging

## Stash

### Converting to a branch

Useful when the stash entry can no longer be popped cleanly. `git stash branch testchanges`.
