---
title: "Changes, Not Files"
date: 2020-05-21T10:15:57-04:00
weight: 75 
---

# Changes, Not Files

## Goal

By the end of this lesson you should be able to...

- Explain what it means for Git to record changes rather than whole file state

## Git Records Changes

It is very important to understand that when working with Git you are dealing in *changes* rather than files.  You stage changes using `git add` and you commit those changes to the repository using `git commit`.  Those changes may involve adding a whole new file, but usually they are just insertions and/or deletions of lines within files.

This is another way in which Git is different than a simple backup—when you commit Git does not simply record the current state of a file, it records how that file changed since the last commit.  Specifically, it records *only* the changes that you have staged using `git add`.

{{< action >}}
Add the following text to `git.txt`: `Git records changes in files, not the current state of files`

Stage this change and check the status:

```text
$ git add git.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   git.txt
```

Now add another line to `git.txt`: `Changes in the working tree that have not been staged will not be committed.`

Check the status again:
```text
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   git.txt
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   git.txt
```
{{</ action >}}

Notice that `git.txt` has both staged and unstaged changes!  This is because you changed `git.txt` again *after* you staged its changes.  

## No Really, Git Records Changes
It may feel strange at first to stage a file and then not have all the changes to that file be included in the next commit, but you will get used to it.  Always remember: when you run `git add` you are not staging the *file* you are staging the *changes* to the file since the last time you staged.  If you make further changes you will have to stage those changes too.

{{< hint info >}}
**NOTE:** If all this business of staging before committing feels like unnecessary work, don't worry—you will soon learn about the power that comes with this process, plus some shortcuts that will make staging and committing simpler in many situations.
{{< /hint >}}

{{< action >}}
Do a commit then check the status again:

```text
$ git commit -m "Added a description about Git change tracking"
[master 312fabf] Added a description about Git change tracking
 1 file changed, 1 insertion(+)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   git.txt
no changes added to commit (use "git add" and/or "git commit -a")
```
{{< /action >}}

The staged change to `git.txt` has now been committed, but the the unstaged change remains uncommitted—it is still in your working tree, but it has not yet been recorded to the repository.  Go ahead and commit it now...

{{< action >}}
Add and commit the most recent change to `git.txt`:

```text
$ git add git.txt
$ git commit -m "Added another change tracking description"
[master 7d7596a] Added another change tracking description
 1 file changed, 1 insertion(+)
 ```
{{< /action >}}

Great!  Let's try a somewhat more complex set of changes...