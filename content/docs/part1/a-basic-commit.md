---
title: "A Basic Commit"
date: 2020-05-14T14:34:21-04:00
weight: 50
---

# A Basic Commit

## Goals

By the end of this lesson you should be able to...

- Use the `git commit` command to commit to a repository any changes that were marked with `git add`
- Add meaningful commit messages to all commits

## Commit

You just marked one kind of change in your repository: the addition of a file.  The `git commit` command is used to record changes in your working tree that you have marked with the `git add` command.

{{< hint info >}}
**NOTE:** In this case there is a single change to commit, but soon you will see that you can commit whole sets of changes in a single commit.
{{< /hint >}}

Here is the format for the `git commit` command:

```sh
git commit -m <message>
```

## Commit Messages

Every commit will be annotated with the user name and email set in your [Git configuration]({{< ref "installing-and-configuring-git.md#user-info" >}}), plus a commit message which you can specify using the `-m` option.

{{< hint info >}}
**NOTE:** If you fail to include a commit message using the `-m` option, Git will open the default command line editor and force you to add a message there.  See [this note]({{< ref "installing-and-configuring-git.md#editor" >}}) regarding how to set the default editor.
{{< /hint >}}

Commit messages should be a brief summary of the changes involved in the commit.

{{< columns >}}
**Examples of good commit messages**
- "Fixed bug #23523"
- "Implemented feature XYZ"
- "Corrected some spelling"
- "Made the sorting function much faster"

<--->

**Examples of bad commit messages**
- "commit"
- "done"
- "asdf"
- "I hate commit messages"

{{</ columns >}}

Using meaningful commit message will prove helpful when you are browsing the change history of your repository—you will be able to see at a glance what the changes in each commit achieve.

{{< action >}}
Do a commit!

```text
$ git commit -m "Initial commit"
[master (root-commit) 17f9667] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 git.txt
```
{{< /action >}}

Note that the commit output gives you:
- a commit ID (`17f9667` here, but yours will be different)
- The number files that were changed in the commit
- The number of lines (insertions/deletions) that were changed in the commit
- Which specific files were changed in the commit

Git has now recorded the fact that `git.txt` was added to the repository.  As long as the `.git` folder remains in your `myrepo` directory (ie, as long as the `myrepo` directory remains a Git working tree) you will always be able to go back to this moment and examine how `git.txt` looked at the time of this commit.  You will also be able to compare the differences between any future committed revision of `git.txt` with this revision.

{{< action >}}
Before moving on, check the status of your repository once more:

```sh
$ git status
On branch master
nothing to commit, working tree clean
```
{{< /action >}}

Here Git is indicating that the set of files in your working tree are exactly the same as the set of files in the most recent commit of the repository—there are no uncommitted changes and no untracked files in your working tree.

Before moving on, let's spend a bit of time talking about commit IDs...