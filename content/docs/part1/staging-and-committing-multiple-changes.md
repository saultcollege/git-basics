---
title: "Staging and Committing Multiple Changes"
date: 2020-05-18T14:14:41-04:00
weight: 80
---

# Staging and Committing Multiple Changes

## Goals

By the end of this lesson you should be able to...

- Make multiple changes in a working tree and commit all those changes in a single commit.
- Use the `git commit --all` option to stage **and** commit all changes in the working tree.

## Make Some Changes

So far you have committed each change you have made in your working tree separately, but this is not typical.  

Usually, commits are performed after some set of related changes have been completed such as the completion of a bug fix or a new feature in a program.  Such changes may involve altering many files and possibly the addition of new files or the removal of unnecessary files.  All these changes may be recorded in a single commit.

The general pattern is:

- Make changes in your working tree
- Stage any changes that should be committed using `git add`
- Commit all staged changes at once using `git commit`

{{< action >}}
1. Use a text editor to add the following text to your `git.txt` file: `The 'git init' command initializes a new Git repository`

2. Add two new files to your working tree, then check the status of your repository:

    ```text
    $ touch a.txt b.txt
    $ git status
    On branch master
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   git.txt
    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt
    no changes added to commit (use "git add" and/or "git commit -a")
    ```
{{< /action >}}

## Stage the Changes

Git sees that you have modified `git.txt` (a tracked file) and that there are two new untracked files `a.txt` and `b.txt`.

{{< action >}}
Stage all changes in `.txt` files then check the status again:

```text
$ git add *.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   a.txt
	new file:   b.txt
	modified:   git.txt
```
{{< /action >}}

Here you staged all your changes at once using a glob path (`*.txt`).  Git indicates that all the changes you have made are now staged to be committed.  (Note again that Git tells you how unstage these changes if you want to.  We will try that soon.)

## Commit the Staged Changes

For now, go ahead and commit all these changes at once.

{{< action >}}
Commit your staged changes:

```text
$ git commit -m "Added more files and text"
[master 9d52001] Added more files and text
 3 files changed, 3 insertions(+)
 create mode 100644 a.txt
 create mode 100644 b.txt
```
{{< /action >}}

## Staging and Committing Multiple Changes With One Command

Often you want to stage and commit *all* changes in your work tree.  Instead of running a `git add` then a `git commit`, the `--all` option of the `git commit` command allows you stage *and* commit in a single command:

```sh
# Format for --all option
$ git commit --all -m <message>
```

The above command will automatically stage all changes in your work tree and then commit those staged changes.

{{< hint warning >}}
**NOTE:** The `--all` option does *not* automatically add previously untracked files, so if your working tree changes involve the addition of new files then you still need to run a `git add`.
{{< /hint >}}

{{< action >}}
1. Edit at least two files in your working tree and save your changes
2. Use the `--all` option to stage and commit all those changes at once:
  ```text
  $ git commit --all -m "Made some content changes"
  ```
{{< /action >}}

You have now made several commits to this repository.  Each commit added a new set of changes to your respository.  Let's take a closer look at that history of changes...