# Git

Everyone's favourite VCS.

## Diff

### Readable diffs of binary files

Well, binary-like files at least.
Anything in a format that is not directly legible, in this case PEM-encoded certificates.
Unlike smudge/clean filters this will not touch either the worktree file or its blob.

First define a diff driver, either globally or locally: `git config diff.crt.textconv "openssl x509 -noout -text -in"`.

Then add a pattern to associate the new driver with some files: `*.crt diff=crt`.
This can go in `.gitattributes` or the local or global `attributes` files, depending on who might be interested in using it.

Git will now convert the certificate into its textual form before feeding it to diff.

More details [here](https://www.kernel.org/pub/software/scm/git/docs/gitattributes.html#_performing_text_diffs_of_binary_files).

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

In the general case this can be done with an interactive rebase, and the last commit can be corrected with `git add ...; git commit --amend [--no-edit]`.
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

### Stash and the index

By default `git stash [push]` will also stash the contents of the index.
To only stash unstaged changes, add the `-k` option.

Alternatively, it's possible to stash *only* staged changes with `-S`.
This is equivalent to committing them to a new branch, but quicker (and arguably tidier).

### Converting to a branch

Useful when the stash entry can no longer be popped cleanly. `git stash branch testchanges`.

## .gitignore

If you add rules to ignore vim droppings and similar in `~/.config/git/ignore`, you don't need to add them to every project you create.
It's obvious when you think about it, isn't it?

There is a collection of per-language rules [here](https://github.com/github/gitignore).

To ignore something that's only relevant locally or for a short time: `echo boring/ >> .git/info/exclude`.
If it's a directory, doing `echo \* > boring/.gitignore` means the ignore will automatically get cleaned up when it's deleted.
Some tools (including `uv`, `pytest` and `mypy`) do this automatically to their cache directories, so check before ignoring them explicitly.

## Repository administration

### git-sizer

[Warns about](https://github.com/github/git-sizer) possible size-related issues that can cause slowness.
