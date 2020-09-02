---
title: "Fetching Updates for Remote Branches"
weight: 2140
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Fetching Updates for Remote Branches

## Goals

By the end of this lesson you should be able to 

- Use the `git fetch` command to get the most recent change history from a remote
- Use the `git status` and `git log` commands to determine the state of a repository compared with the last time it was synchronized with its remote(s)
- Use the `git diff` command to see the differences between a local branch and a corresponding remote branch

## Synchronizing Repositories

As two related repositories receive commits they become out of sync.  In order to synchronize a repository with one of its remotes there are two main steps:

1. Update the related remote branches.  Ie, obtain all commits in the remote that are not in the corresponding remote branches in your local repository.
2. Merge the remote branches into their related local branches.

In this lesson we will focus on the first step.

## The Fetch Command

The `git fetch` command updates the remote branches for a remote so that they contain the most recent commit history in the remote.  Like clone, this command requires that Git can access the remote repository, either on a local disk or over the internet.

```sh
# Format for the git fetch command
$ git fetch <remote_name>
```

The `<remote_name>` is simply the name of the remote for which you want to update its remote branches.

## Hands-on Example

Imagine that you are a programmer working on a repository that you have cloned from a team mate.  This is much like the situation we are in with `clonerepo` and `myrepo`:  you could think of `myrepo` as your team mate's repository and `clonerepo` as your repository.  Of course, `myrepo` would usually be on a completely separate computer (your team mate's) but we are keeping things all in one place here so it is easy for you to inspect what is happening on both ends of this scenario.

{{< hint warning >}}
**IMPORTANT:** Pay careful attention to which repository you should be working in for the activities in the next several lessons.  You will be working in both `myrepo` and `clonerepo` at different times.
{{< /hint >}}

### Make a Commit in the Remote

{{< action >}}
Suppose your team mate makes a change their repository, `myrepo`.

1. Get into the `myrepo` repository
   ```text
   $ cd ../myrepo
   ```
1. Add the line `The 'git clone' command clones a repository and configures a remote` to `git-cheat-sheet.txt`
1. Commit your change:
   ```text
   $ git commit -am "A note about the clone command"
   [master 3560cd0] A note about the clone command
   1 file changed, 1 insertion(+)
   ```

   Note the commit ID, `3560`
{{< /action >}}

Your team mate's repository is now different from yours: they have made one commit that your repository does not have.  Let's see what your repository looks like right now:

{{< action >}}
1. Get into the `clonerepo` repository
   ```text
   $ cd ../clonerepo
   ```
1. Check the status and log output
   ```text
   $ git status
   On branch master
   Your branch is up to date with 'origin/master'.

   nothing to commit, working tree clean
   $ git log --oneline
   6ba2205 (HEAD -> master, origin/master, origin/HEAD) Merge mybranch into master
   ff2b08d (origin/mybranch) A note about the merge command
   37a381b Notes about the branch and switch commands
   737f014 Merge mybranch into master
   663e99a Title change
   ...
   ```
{{< /action >}}

Hmm, commid ID `3560` is not there.  

### Fetch Changes From the Remote

You need to fetch in order to see the remote changes your local repository.  Try that now!

{{< action >}}
1. Fetch any changes from the remote:
   ```sh
   $ git fetch origin
   remote: Enumerating objects: 5, done.
   remote: Counting objects: 100% (5/5), done.
   remote: Compressing objects: 100% (3/3), done.
   remote: Total 3 (delta 1), reused 0 (delta 0)
   Unpacking objects: 100% (3/3), done.
   From /Users/rod/tmp/myrepo   # Your path here will be different
   * branch            master     -> FETCH_HEAD
      6ba2205..3560cd0  master     -> origin/master
   ```
1. Check the status again:
   ```text
   $ git status
   On branch master
   Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
   (use "git pull" to update your local branch)

   nothing to commit, working tree clean
   ```
{{< /action >}}

Now that you have fetched the changes from the remote, Git can tell you that your `master` branch is 1 commit behind the related remote branch!  You can confirm this by examining the log output:

{{< action >}}
1. Display the full log for `clonerepo`:
   ```text
   $ git log --oneline --all
   3560cd0 (origin/master, origin/HEAD) A note about the clone command
   6ba2205 (HEAD -> master) Merge mybranch into master
   ff2b08d (origin/mybranch) A note about the merge command
   37a381b Notes about the branch and switch commands
   737f014 Merge mybranch into master
   663e99a Title change
   ...
   ```
{{< /action >}}

Aha!  There's that new commit, and you can see the remote branch points to it, but your local `master` branch is still pointing to the previous commit (hence, your branch is 1 commit behind `origin/master`).  

### Compare Local and Remote Branches

Finally, you can compare the differences between `master` and its corresponding remote `origin/master` using the `git diff` command and naming the two branches as arguments:

{{< action >}}
1. Show the differences between `master` and `origin/master`:
   ```text
   $ git diff master origin/master
   diff --git a/git-cheat-sheet.txt b/git-cheat-sheet.txt
   index 878b2e6..0153588 100644
   --- a/git-cheat-sheet.txt
   +++ b/git-cheat-sheet.txt
   @@ -12,3 +12,4 @@ The 'git restore' command can be used to undo changes
   The 'git branch' command can be used to list and create branches
   The 'git switch' command can be used to set the active branch
   The 'git merge' command can be used to merge changes in two branches
   +The 'git clone' command clones a repository and configures a remote
   ```
{{< /action >}}

The diff output<sup>[1](#fn1)</sup> indicates the addition of one line to get from the contents in `master` to the contents in `origin/master`.

<div class="footnote">
<a name="fn1">1</a>:  See the <a href='{{< ref "seeing-what-changed#reading-diff-output" >}}'>Seeing What Changed</a> lesson if the output of the diff command is unfamiliar to you.
</div>

## Up Next: Merging

You now know how to get the latest changes from any remote into the remote branches of your repository using `git fetch`.  And you can compare your repository's state with that of its remote(s) using the `git status`, `git log`, and `git diff` command.  

Next you will learn how to incorporate those changes into a local branch...