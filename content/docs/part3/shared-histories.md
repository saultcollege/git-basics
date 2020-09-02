---
title: "Shared Histories"
weight: 2135
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Shared Histories

## Goals

By the end of this lesson you should be able to 

- Explain what is meant by two repositories having a shared history

## What is a Shared History?

In the previous lesson we saw that two repositories may be synchronized with each other if one of them is configured as a remote of the other.  

It is important to note, however, that repositories can only be synchronized if they have a **shared history**.  When you clone a repository or copy it, the history of the original repository remains intact in the clone/copy (inside the `.git` directory), thus Git is able to synchronize the clone/copy with the original.

Let's take a look at the logs of your two repositories to see precisely what is meant by a 'shared history'.

{{< columns >}}
Recall the output of the log for the `clonerepo` repository:

```text
$ cd ../clonerepo
$ git log --oneline
6ba2205 (HEAD -> master, origin/master, origin/HEAD) Merge mybranch into master
ff2b08d (origin/mybranch) A note about the merge command
37a381b Notes about the branch and switch commands
737f014 Merge mybranch into master
663e99a Title change
1ebc7b1 A note about the restore command
70b4290 A note about the commit command
08f4897 (tag: anothertag) Renamed git.txt
714c41e Removed unnecessary files
39fa5fc Revert "Revert "Added note about the 'git add' command""
b2763fe Revert "Added note about the 'git add' command"
87af010 Added note about the 'git add' command
7d7596a Added another change tracking description
312fabf Added a description about Git change tracking
9d52001 Added more files and text
3f21652 Added brief description
dde186d Added .gitignore file
17f9667 Initial commit
```
<--->

Compare that with the log for the `myrepo` repository:

```text
$ cd ../myrepo
$ git log --oneline
6ba2205 (HEAD -> master) Merge mybranch into master
ff2b08d (mybranch) A note about the merge command
37a381b Notes about the branch and switch commands
737f014 Merge mybranch into master
663e99a Title change
1ebc7b1 A note about the restore command
70b4290 A note about the commit command
08f4897 (tag: anothertag) Renamed git.txt
714c41e Removed unnecessary files
39fa5fc Revert "Revert "Added note about the 'git add' command""
b2763fe Revert "Added note about the 'git add' command"
87af010 Added note about the 'git add' command
7d7596a Added another change tracking description
312fabf Added a description about Git change tracking
9d52001 Added more files and text
3f21652 Added brief description
dde186d Added .gitignore file
17f9667 Initial commit
```

{{< /columns >}}

Note that the sequence of commit IDs in both logs is exactly the same.  This is the key fact that makes the histories of these two repositories 'shared'.

Suppose you created a new directory and initialized it as a new git repository (using `git init`) but did the exact same sequence of changes as you have done to get to the state that `myrepo` is in now.  This new repository would have the same content in the working tree, but it would **not** share a history with `myrepo` or `clonerepo` because it would have a different sequence of commit IDs.

{{< hint warning >}}
**NOTE:** As a general rule: you should never use `git init` to initialize a repository when you could clone or copy instead because `git init` starts a brand new commit history.  If you ever encounter error messages like `no common commits` or `refusing to merge unrelated histories` it is likely that you **initialized** a new repository when you should have **cloned** or **copied** an existing one. 
{{< /hint >}}

This knowledge will be helpful when you want to start working with repositories from hosts like GitHub or GitLab.

Now let's talk about 'Tracking Branches'...






