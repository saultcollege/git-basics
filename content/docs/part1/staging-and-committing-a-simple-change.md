---
title: "Staging and Committing a Simple Change"
date: 2020-05-18T12:56:19-04:00
weight: 70
---

# Staging and Committing a Simple Change

## Goals

By the end of this lesson you should be able to...

- Make changes to the tracked files in a repository and commit those changes
- Explain what it means to 'stage changes' in a Git repository

## Make a Change

{{< action >}}
Open the `git.txt` file in a text editor of your choice, and add the following new line of text: `Git is a distributed version control system.`

Now check the status

```text
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   git.txt
no changes added to commit (use "git add" and/or "git commit -a")
```
{{< /action >}}

## Commit the Change

Since `git.txt` is a tracked file, Git sees that it has changed in comparison to the most recent revision of the file stored in the repository.  We can tell Git that we would like to commit this change by first marking the change using `git add` then committing that marked change using `git commit`:

{{< action >}}
Add and commit the change: 

```text
$ git add git.txt
$ git commit -m "Added a brief description"
[master 3f21652] Added brief description   # Your commit ID will be different
 1 file changed, 2 insertions(+)
```
{{</ action >}}

## Staging

Previously, you used `git add` to tell Git to track a new file.  Here you are using it to tell Git that you would like to record the changes to `git.txt` on the next commit.  In fact, the general purpose of the `git add` command is to inform Git of any changes (file additions or file alterations) that you would like to include in the next commit.

This process of marking changes that should be included in the next commit is called **staging**.  In Git, you must stage your changes before they can be committed.

Note that we are using the term *changes* for the thing that you are staging rather than *files*.  Let's talk about that...