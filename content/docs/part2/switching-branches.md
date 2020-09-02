---
title: "Switching Branches"
weight: 2040
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Switching Branches

## Goals

By the end of this lesson you should be able to

- Use the `git switch` command to switch between branches in a Git repository

## The Switch Command

The `git switch` command can be used to switch between branches.

```sh
$ git switch <branch_name>
```

{{< hint info >}}
**NOTE:** If you read Git documentation on the internet you will encounter many sites that use the `git checkout` command to switch branches.  This command had become overloaded with functionality so the Git developers have recently split its functionality into two new commands, `git switch` and `git restore`.  You already encounterd `git restore` in the [Undoing Changes]({{< ref "undoing-changes.md" >}}) lesson.  This lesson deals with `git switch`.
{{< /hint >}}

What does it mean to switch branches?  Two main things happen:

1. The `HEAD` pointer now points to the branch that was switched to
2. Git sets the contents of all files in the working tree and index to be the same as those of the commit pointed to by the branch that was switched to.

Let's see this in action.  Right now, your commit history looks something like this:

<figure style="width: 500px">
<img src="/images/branches-2.png" alt="Branches">
<b>Figure: Initial Branch Configuration</b>
</figure>

After switching to the `mybranch` branch it will look like the figure below, and your working tree contents will have chnaged.

<figure style="width: 500px">
<img src="/images/branches-3.png" alt="Branches">
<b>Figure: Branch Configuration After Switch</b>
</figure>

Try it yourself:

{{< action >}}
Switch to the `mybranch` branch, and display the log

```text
$ git switch mybranch
Switched to branch 'mybranch'
$ git branch
master
* mybranch
```

Notice that `mybranch` is now the active branch as indicated by the `*` in the output of the `git branch` command.

Examine the contents of the `git-cheat-sheet.txt` file.  What happened to the lines you added in the previous lesson?!
{{< /action >}}

Git has set the contents of all the files in your working tree to be the same as those of the commit pointed to by the branch you switched to!

This aspect of branches can seem unsettling when you first encounter it.  Git beginners sometimes worry about losing work they have done by switching branches, but their worries are unfounded.  All the information is still in the **repository**; Git has simply updated the contents of your **working tree**.

Let's confirm that by switching back to the `master` branch:

{{< action >}}
Switch back to the `master` branch
```text
$ git switch master
Switched to branch 'master'
$ git branch
* master
mybranch
```

Confirm that `git-cheat-sheet.txt` again contains the new lines from the previous lesson.

{{< /action >}}

## Enlightenment is Near!

Once you get comfortable with this aspect of Git, you are near to Git enlightenment!  Now, when you want to try something experimental in your code you should think nothing of creating a new branch in which to try things out.  If things don't go well, you can just delete the branch and resume with whatever state your code was in on the `master` branch.  And what if your experiments do work?  You will learn in the next few lessons how to merge changes from one branch into another.

Before moving on, though, let's take a look at the log output as we switch branches...