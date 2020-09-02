---
title: "Merging Remote Branches"
weight: 2150
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Merging Remote Branches

## Goals

By the end of this lesson you should be able to

- Use `git merge` to incorporate changes from a remote into local branches in a repository

## Merging Remote Branches

In the previous lesson you learned how to fetch the most recent change history from a remote into the corresponding remote branches of a local repository.  That step allowed you to examine the differences between a local repository and its remote.  

In this lesson you will learn how to merge the changes of a remote branch into its corresponding local branch.  

The good news is that you already know how to do this!  Since both the remote and local branches in question are just branches, the `git merge` command is all you need<sup>[1](#fn1)</sup>.  Simply make sure you are on the correct local branch, then merge in the remote branch.

{{< action >}}
1. Get into `clonerepo` and make sure you are on `master`
    ```text
    $ cd ../clonerepo
    $ git switch master
    Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
     (use "git pull" to update your local branch)
    ```
1. Merge the remote `master` branch into the local `master`
    ```text
    $ git merge -m "Merge remote into master" origin/master
    Updating 6ba2205..3560cd0
    Fast-forward (no commit created; -m option ignored)
     git-cheat-sheet.txt | 1 +
     1 file changed, 1 insertion(+)
    ```
1. Examine the contents of `git-cheat-sheet.txt` to confirm that the new line about the clone command is there.

{{< /action >}}

That's all there is to it!  Your working tree is now once again up to date with the remote `myrepo`.  You can confirm this with `git status` and `git log`:

{{< action >}}
Check the status and log of `clonerepo`:
```text
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

$ git log --oneline
3560cd0 (HEAD -> master, origin/master, origin/HEAD) A note about the clone command
6ba2205 Merge mybranch into master
ff2b08d (origin/mybranch) A note about the merge command
37a381b Notes about the branch and switch commands
737f014 Merge mybranch into master
663e99a Title change
```
{{< /action >}}  

As you can see, Git indicates that your `master` branch is up to date with `origin/master`, and in the log both of `master` and `origin/mater` are now pointing at the same commit, `3560`.

## What About Conflicts?

Of course, it is possible that you had made commits involving the same parts of files as those in the remote, in which case you might encounter a conflict that Git cannot automatically merge.  But you already know how to deal with conflicts too.  (Review the [Dealing with Conflicts]({{< ref "dealing-with-conflicts" >}}) lesson if you need to refresh your memory.)  

You deal with conflicts arising after merging a remote branch in exactly the same way as you do with conflicts from merging local branches: fix the conflicting regions manually then commit the fix to the local branch.

<div class="footnote">
<a name="fn1">1</a>:  See the <a href='{{< ref "merging-branches" >}}'>Merging Branches</a> lesson if you need to review how the <code>git merge</code> command works.
</div>

## A Simpler Way

You might be thinking that it seems like a lot of work to synchronize a repository with a remote—you have to manually synchronize remote branches then merge those branches into local branches if you want to incorporate the changes into your working tree.  

The truth is that it is usually possible to do both the fetching and merging in a single command, `git pull`, which you will learn about in the next lesson.  Hopefully understanding the underlying process of fetching and merging helps to demystify the `pull` command.
