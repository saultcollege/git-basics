---
title: "Remote Branches"
weight: 2138
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Remote Branches

## Goals

By the end of this lesson you should be able to 

- Describe what a remote branch is and how it relates to a repository with remotes
- Use the `--all` option of the `git branch` command to list branches, including remote branches

## What is a Remote Branch?

You already know that branches in Git can be used to track 'alternate histories' of changes in the files in a repository.

When working with remotes, Git automatically creates branches in the local repository that contain the change history of each remote.  These branches are called **remote branches**.  If a repository and its remote(s) are in sync then both a branch and its related remote branch(es) will point to the same commit.

{{< hint info >}}
**NOTE:** Since the intent of remote branches is for them to be a replica of a branch in a remote repository, Git will not allow you to switch to a remote branch using `git switch`<sup>[1](#fn1)</sup>.  You can, however, view the differences between two branches using `git diff`, as you will see in the next lesson.
{{< /hint >}}

{{< hint info >}}
**NOTE:** Remote branches are usually annotated with their remote name as a prefix, separated by a `/`.  For example, if a remote was named `origin` and it had a branch named `master`, it would be labelled `origin/master`.
{{< /hint >}}


<div class="footnote">
<a name="fn1">1</a>:  That said, there are ways in Git to get the contents of remote branches into your working tree, but that is beyond the scope of this tutorial.
</div>

## Hands-on Example

Consider the two repositories you have created, `myrepo` and `clonerepo`.  At this point both repositories should be perfectly in sync because you have not made any changes in either repository since you cloned.  In this case the `master` branch in `clonerepo` should point to the same commit as that of `myrepo`.

Recall again the log output for the two repositories:

{{< columns >}}
The `clonerepo` log output:

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

The `myrepo` log output:

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

Indeed, the `master` branch in both points to commit `6ba2`.  But take a closer look to that same commit in the `clonerepo` log output.  You should see there two branch labels that are not in the original `myrepo`: `origin/master` and `origin/HEAD`.  

The first of these labels is the remote branch in `clonerepo` that Git automatically configured when you cloned `myrepo`.  This branch is essentially a copy of the `master` branch of `myrepo` as it was when `clonerepo` was last synced with `myrepo`.  (Remember that `myrepo` is a remote named `origin` in `clonerepo`.)

The second label is simply indicating that `HEAD` in the remote points to `master`.  This becomes even more clear when you run the `git branch` command with the `--all` option to include remote branches in its display.

{{< action >}}
In `clonerepo` list the branches, including remotes

```text
$ git branch --all
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/mybranch
{{< /action >}}

Two more things to notice:

1. There *is* a remote branch for `origin/mybranch` (ie, `myrepo`'s `mybranch` branch) in `clonerepo`
2. There is *not* a local branch named `mybranch` in `clonerepo`

{{< hint warning >}}
**NOTE:** This is another instance where cloning and copying differ: in a clone, no *local* branches aside from `master` will exist by default (but there will be *remote* branches for each branch in the remote); in a copy, *all* local branches in the original will exist in the copy (but there will be no remote branches that were not already in the original).
{{< /hint >}}


You are now ready to learn how to keep a repository in sync with its remote(s)...