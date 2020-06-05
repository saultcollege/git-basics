---
title: "Undoing Changes"
date: 2020-05-21T16:55:53-04:00
weight: 100
---

# Undoing Changes

## Goals

By the end of this lesson you should be able to use the `git restore` command to...

- Undo staged changes
- Undo changes in the working tree
- Revert files in the working tree and/or index to a previous revision

## Undoing Staged Changes

If you have staged changes for a file, you may unstage those changes using the following:

```sh
# Unstage changes to files
git restore --staged <files>
```

{{< hint info >}}
**NOTE:** The `git restore` command is relatively new.  You may find older documentation that suggests a command like `git reset HEAD <files>` to unstage changes, which is the old way to do this.  The old way still works, but in general it is best to use the command suggested by Git when you run `git status`.
{{< /hint >}}

**Examples**

```sh
# Unstage changes to foo.txt
$ git restore --staged foo.txt 

# Unstage changes to foo.txt and bar.py
$ git restore --staged foo.txt bar.py

# Unstage all changes in the foo directory (but no others)
$ git restore --staged foo/*

# Unstage all staged changes
$ git restore --staged .
```

{{< action >}}

Your learning repository should have a staged change in `git.txt` and an unstaged change in `a.txt` from the previous activity.  (Use `git status` and `git diff` to refresh your memory of the changes you've made.)

Stage the change in `a.txt`:

```sh
$ git add a.txt
```

You should now see `a.txt` in the set of files with staged changes when you run `git status`.

Now undo the staging you just did:

```sh
$ git restore --staged a.txt
```

A `git status` should now show that `a.txt` has unstaged changes, but not staged changes.

{{</ action >}}

## Undoing Working Tree Changes

If you have made changes in your working tree since the last time you staged, you can undo those changes using the `--worktree` option.  This will copy the revision in the **index** (*not* the repostory) back to your working tree.  (However, if you have not staged any changes then the index and repository have the same state.)

{{< hint info >}}
**NOTE:** If neither the `--worktree` nor the `--staged` option are specified, `--worktree` is assumed by default.
{{< /hint >}}

```sh
# Restore files to the most recent commit
git restore --worktree <files>
```

**Examples**

```sh
# Undo changes to foo.txt that have not been staged
$ git restore --worktree foo.txt 

# Undo changes to foo.txt and bar.py that have not been staged
$ git restore --worktree foo.txt bar.py

# Undo all unstaged changes in the foo directory (but no others)
$ git restore --worktree foo/*

# Undo all unstaged changes
$ git restore --worktree .
```


{{< action >}}

Restore `a.txt` back to its state before you started making changes:

```sh
# Note that --worktree is the default is neither --worktree nor --staged is used
$ git restore a.txt
```

A `git status` should show that there are now no staged or unstaged changes in `a.txt`.

{{</ action >}}

## Restoring Specific Commits

You can use the `--source` option to choose a source from which to restore (the default when `--source` is not specified is the index).  This option in combination with the `--staged` and/or `--worktree` options will copy the source revision into the respective destination.

### Restore the Most Recent Revision Into the Working Tree

```sh
# Restore the most resent revision of foo.txt into the working tree
$ git restore --source=HEAD --worktree foo.txt
```

### Restore an Older Revision Into the Working Tree

```sh
# Restore foo.txt to its state at commit id cd31
$ git restore --source=cd31 --worktree foo.txt
```

{{< action >}}

Restore a previous revision of `git.txt` to your working tree.  Use `git log` to pick any previous commit ID, then use that ID in the following `git restore` command:

```sh
# Replace 17f9 with your chosen commit ID
$ git restore --source=17f9 --worktree git.txt
```

Your `git.txt` should now be in the state that it had in the commit you chose.  Thus, it has both staged changes (the changes you staged previous activity which you can view using `git diff --staged`) and unstaged changes (the changes you just restored which you can view using `git diff`).  You have only updated your working tree and have not staged this latest change to your file.  

Let's put `git.txt` back into the state it was in when was when you last staged it:

```sh
$ git restore git.txt
```

Your `git.txt` should now have just the one new line `The 'git add' command adds changes to the index` and should only appear in the list of files with staged changes when you run `git status`.

Finally, go ahead and commit this staged change:

```text
$ git commit -m "Added a note about the add command"
```

{{< /action >}}

## Undo Staged AND Unstaged Changes

If all three of `--staged`, `--worktree`, and `--source` are specified at once then the source revision is copied into both the index and the working tree, in effect undoing all staged and unstaged changes.

```sh
# Restore ALL files in the index and the working tree to the most recent commit
$ git restore --source=HEAD --worktree --staged *

# Unstage AND undo working tree changes in foo.txt
$ git restore --source=HEAD --worktree --staged foo.txt

```
