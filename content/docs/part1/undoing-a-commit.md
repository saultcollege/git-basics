---
title: "Undoing a Commit"
date: 2020-05-22T10:56:38-04:00
weight: 110
---

# Undoing a Commit

## Goals

By the end of this lesson you should be able to...

- Undo a commit using the `git revert` command

## Revert

Sometimes instead of undoing staged or working tree changes you need to undo a commit.  The `git revert` command is the safest way to do so.  This command does *not* remove any commits.  Instead, it simply creates a new commit that applies the changes *opposite* to a specified commit.

```sh
# Format for the git revert command
$ git revert [--no-edit] <commit>
```

The `--no-edit` option tells Git that you do not wish to edit the default commit message made by `revert`.  If you do not provide this option Git will open the [default command line text editor]({{< ref "installing-and-configuring-git.md#editor" >}}) for you to edit the message.

## Examples

```sh
# Revert the most recent commit
$ git revert --no-edit HEAD

# Revert the changes in a specific commit
# AND edit the commit message
$ git revert cd123
```

{{< action >}}

Undo your most recent commit:

```text
$ git revert --no-edit HEAD
[master b2763fe] Revert "Added a note about the add command"
 1 file changed, 1 deletion(-)
```

Run `git log` to see the new commit.  Note the message indicating that it reverts the previous commit.

Now revert the revert to get things back to where you started at the beginning of this activity:

```text
$ git revert --no-edit HEAD
[master 39fa5fc] Revert "Revert "Added note about the 'git add' command""
 1 file changed, 1 insertion(+)
```

Note the commit message indicating that this reversion reverts the previous one.  Check the contents of `git.txt` to confirm that the double reversion worked as expected. (It should contain the line `The 'git add' command adds changes to the index`.)

{{< /action >}}