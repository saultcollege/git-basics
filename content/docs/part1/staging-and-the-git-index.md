---
title: "Staging and the Git Index"
date: 2020-05-14T14:05:19-04:00
weight: 90
---

# Staging and the Git Index

## Goals

By the end of this lesson you should be able to...

- Explain what the Git Index is and how it relates to the `git add` and `git commit` commands
- Stage only specific files among any number that have changes in the working tree

## The Git Index 

So far you have learned the basic pattern of committing files to a Git repository:

1. Make changes in your working tree
2. Stage the changes you want to commit using `git add`
3. Commit all staged changes `git commit`

When you use the `git add` command, you are *adding* changes (hence `git add`) to something called the **Git Index**.  When a `git commit` command is issued, the changes staged in the index are incorporated into the main repository.  Thus, immediately after a commit the index and the repository have the exact same state.

<figure style="width:300px; margin:auto">
<img src="/images/the-git-index.png" alt="The Git Index"><br>
<b>Figure: The Git Index</b><br>Changes in the working tree can be staged to the index using <code>git add</code>; changes staged in the index can be stored in the repository using <code>git commit</code>.
</figure>

{{< action >}}
Add the following text to `a.txt`: `Here is some new text`.

Do a commit:

```sh
$ git commit
Changes not staged for commit:
	modified:   a.txt
no changes added to commit
```

There are changes in the working tree, but they have not been added to the index (ie, staged), therefore Git does not commit any changes.


{{< /action >}}


## Why is the Index a Thing?

It may seem strange at first to have this extra step of adding changes to the index before actually committing them.  This does require additional work, but in exchange you get a great amount of flexibility in precicely which changes to include in a commit.

For example, suppose you were working on a new feature in your program that involves changes to files `A` and `B`, and in doing so you discovered and fixed a software bug in file `C`.  You may want to commit the bug fix separately from your feature code.  The `git add` command gives you the ability to stage only file `C` so that when you commit, only the changes to `C` and *not* the changes to `A` and `B` are included in the commit.

{{< hint info >}}
**NOTE:** It is even possible to add a specific subset of the changes within a single file using the `-i` (interactive) option of the `git add` command.  This option is beyond the scope of this tutorial, but if you are interested in using this feature read the [official Git documentation](https://git-scm.com/book/en/v2/Git-Tools-Interactive-Staging).
{{< /hint >}}

{{< action >}}
In addition to the change you made to `a.txt` in the activity above, add the following text to the `git.txt` file: `The 'git add' command adds changes to the index.`

Now stage *only* the changes in `git.txt` and check the status:
```text
$ git add git.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   git.txt
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   a.txt
```

Git tells you which changes are staged to be committed and which are not.  If you were to run a `git commit` now you would commit only the changes staged in the index—but don't do that yet!

{{< /action >}}

