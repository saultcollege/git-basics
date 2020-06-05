---
title: "Removing, Moving, and Renaming Files"
date: 2020-06-04T12:04:41-04:00
weight: 120
---

# Removing, Moving, and Renaming Files

## Goals

By the end of this lesson you should be able to...

- Stage file removals using the `git rm` command
- Stage file renames using the `git mv` command
- Stage file moves using the `git mv` command

## Overview

As you have seen, changes to file *contents* must be staged and then committed in order to be recorded in the respository history.  In the same way and for the same reasons, changes to file *names* and *paths* must also be staged and then committed in order to be stored in the repository.  Instead of using the `git add` command, though, you use `git rm` and `git mv`.

{{< action >}}

Remove the `a.txt` file from your working directory using the `rm` command (*not* the `git rm` command), then check `git status`:

```text
$ rm a.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    a.txt
no changes added to commit (use "git add" and/or "git commit -a")
```

Note that Git detects the removal of files in your working directory, but you must stage these removals manually.

{{< /action >}}

## Removing Files

The `git rm` is used instead of `git add` to stage file removals.  This command can be used both to stage files that have already been removed or to remove files *and* stage the removal simultaneously.

```sh
# Format for git rm command
$ git rm <files>
```

{{< action >}}

Stage your previous removal of `a.txt`:

```text
$ git rm a.txt
rm 'a.txt'
```

Now use `git rm` to remove `b.txt` and stage the removal simultaneously:

```text
$ git rm b.txt
rm 'b.txt'
```

Verify that both `a.txt` and `b.txt` are no longer in your working directory, then check `git status` to verify that both the removals are staged and ready to commit.

```text
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    a.txt
	deleted:    b.txt
```

Finally, commit this change:

```text
$ git commit -m "Removed unnecessary files"
[master 714c41e] Removed unnecessary files
 2 files changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 a.txt
 delete mode 100644 b.txt
```

Note that Git indicates the files that were removed in this commit.

{{< /action >}}

## Renaming Files

### Renaming Using `rm` and `add`

Renaming a file can be thought of as copying the file to a new name and deleting the orinal file.  It is possible to stage a file rename using just the `git rm` and `git add` commands:

{{< action >}}

Rename `git.txt` to `git-cheat-sheet.txt` and check the status:

```text
$ mv git.txt git-cheat-sheet.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    git.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	git-cheat-sheet.txt

no changes added to commit (use "git add" and/or "git commit -a")

Note that Git sees the new `git-cheat-sheet.txt` and the removal of `git.txt`.  We can stage these changes using `git rm` and `git add` respectively:

```sh
$ git rm git.txt
$ git add git-cheat-sheet.txt
```

Check the status:

```text
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    git.txt -> git-cheat-sheet.txt
```

Note that Git has automatically detected that the combined removal and addition are in fact a rename!

Finally, commit the change:

```text
$ git commit -m "Renamed git.txt"
[master 08f4897] Renamed git.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename git.txt => git-cheat-sheet.txt (100%)
```

{{< /action >}}

### Renaming Using `mv`

The process used above can be done in a single step with the `git mv` command!

```sh
# Format for the git mv command
$ git mv <from> <to>
```

{{< action >}}

Rename `git-cheat-sheet.txt` back to `git.txt`:

```text
$ git mv git-cheat-sheet.txt git.txt
```

Verify that the file has been renamed in your working directory, and use `git status` to verify that the change has been staged.

Undo this change. (The name `git-cheat-sheet.txt` is more descriptive.)

```text
$ git mv git.txt git-cheat-sheet.txt
```

Verify that the file is named `git-cheat-sheet.txt` in your working directory, and verify that there are no changes to be committed using `git status`.

{{< /action >}}

## Moving Files

The `git mv` file can also be used to move files between directories.  It works exactly the same as renaming except that instead of two different file names, you specify two different paths to the same file name.

**Examples**

```sh
# Move foo.txt into the directory named bar
$ git mv foo.txt bar/foo.txt
$ git mv foo.txt bar  # <-- this does the same thing too

# Move foo.txt into the parent directory
$ git mv foo.txt ../foo.txt
$ git mv foo.txt ..  # <-- this does the same thing too
```

You can even move and rename simultaneously:

**Examples**

```sh
# Rename foo.txt to baz.txt and move it into the directory named bar
$ git mv foo.txt bar/baz.txt

# Rename foo.txt to baz.txt and move it into the parent directory
$ git mv foo.txt ../baz.txt
```
