---
title: "Initializing a Git Repository"
date: 2020-05-13T13:56:07-04:00
weight: 30
---

# Initializing a Git Repository

## Goals

By the end of this lesson you should be able to...

- Use the `git status` command to view the current repository state of any directory
- Use the `git init` command to initialize a new Git repository directory

## Status

The `git status` command can be used to show information about a Git repository.

```sh
# Check the Git status
$ git status
```  

{{< action >}}
In your shell, change to a directory that you would like to work in for this tutorial ([create a new directory](https://saultcollege.github.io/shell-basics/#mkdir--rmdir) if you like) then run `git status`.

```bash
$ cd ~  # You may choose a different directory
$ git status
fatal: not a git repository (or any of the parent directories): .git
```
{{</ action >}}

Note that the `git status` command notifies you if your shell is not currently inside a Git repository directory.  Let's make one now!

## Init

The `git init` command is how you initialize a Git repository.  It has the following format:

```sh
# Initialization command format
git init [<path>]
```  

If you run `git init` without any other arguments then the current directory becomes a Git repository directory.

If you include a path argument then a new directory at that path will be created, and that directory becomes a Git repository directory.

{{< action >}}
In the directory you chose in the activity above, initialize a new git repository named 'myrepo':
```sh
$ git init myrepo
Initialized empty Git repository in /Users/rod/tmp/myrepo/.git/
```
{{< /action >}}

{{< hint info >}}
**NOTE:** The output you see will probably have a different path.
{{< /hint >}}

A new directory named `myrepo` has been created, and inside of this directory is another directory named `.git`.  The `myrepo` directory will contain all files in this repository (and possibly some that are not part of the repository—more on this in a bit).

The `.git` directory is where Git stores the configuration and change history for your repository.   It can be interesting to peek at the files inside the `.git` directory, but usually Git manages these files for you, and you should not alter them directly.

{{< hint info >}}
**NOTE:** It is easy to turn a Git repository directory into a plain directory: simply delete the `.git` folder!  But be careful, because doing so will also eliminate the change history for the files and you will no longer be able to compare with or revert to previous revisions of the files using Git.
{{< /hint >}}

Now that you have initialized a Git repository, let's check its status again.

{{< action >}}
Navigate into the `myrepo` directory, then check the status:

```text
$ cd myrepo
$ git status
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```
{{< /action >}}  

#### What is a branch?

The first line of output says that you are on the 'master' branch of the repository.  We will not concern ourselves for now with branches except to say that every Git repository has at least one branch which is named 'master' by default.  (It is possible to create other branches which represent 'alternate histories' of the files in your repository, but we will look at that in Part 2 of this tutorial.)  For now, we will stick to using only the master branch.

#### What is a commit?

The second line says that your repository has no 'commits'.  For now, think of a commit as Git's name for a 'snapshot' of the set of files in your repository.  Every time you tell Git to take such a snapshot it will create a 'commit' which has a unique ID, and it will record the state of all tracked files in the repository.  The ID can be used in the future to examine the state of any tracked file in the repository at the time when the commit with that ID was made.

#### What does it mean for Git to track a file?

Read on!
