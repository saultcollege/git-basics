---
title: "Fetching and Merging With Pull"
weight: 2160
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Fetching and Merging with Pull

## Goals

By the end of this lesson you should be able to 

- Use the `git pull` command to synchronize a repository with its remote in a single step

## A Summary of What You Know

In the previous lessons you have learned the concepts of how Git synchronizes repositories.  Let's summarize what you know:

- Git repositories may have shared commit histories
- Two repositories with shared histories can be synchronized by configuring 'remotes'
- When you clone a repository, Git automatically configures the original repository as a remote for the clone
- Git uses 'remote branches' to track the changes in a repository's remotes
- The `git fetch` command updates the remote branches for a remote
- The `git merge` command can be used to merge changes in a remote branch into a related local branch, bringing changes in the remote into the local working tree

There is a lot going on here!  Fortunately, once a remote has been configured, it is very simple to keep a repository synchronized with its remote using the `git pull` command.

## The Pull Command

The `git pull` command both fetches the latest commit history for a remote and merges changes from one of the remote branches for that remote into the corresponding local branch.

Since `git pull` must fetch commit history from a remote, Git must again be able to access the remote in some way in order to succeed.

```sh
# Format for the git pull command
$ git pull <remote_name> <branch_name>
```

The `<remote_name>` specifies which remote to synchronize with.  The `<branch_name>` is the specific branch to merge.

For example, assuming the active branch in a repository is `master`, running the command

```sh
$ git pull origin master
```

is essentially the equivalent of

```sh
$ git fetch origin
$ git merge origin/master
```

## Hands-on Example

Let's again make a change in `myrepo` that you will then synchronize with `clonerepo`, but this time instead of fetching and merging separately you will use `git pull` to synchronize all in one step.

{{< action >}}
1. Get into `myrepo` 
    ```text
    $ cd ../myrepo
    ```
2. Add the line `The 'git fetch' command retrieves the latest commit history from a remote` to `git-cheat-sheet.txt`
3. Commit this change
    ```text
    $ git commit -am "A note about the fetch command"
    git commit -am "A note about the fetch command"
    [master 6c4312f] A note about the fetch command
     1 file changed, 1 insertion(+)
    ```
{{< /action >}}

Your two repositories are once again out of sync with `clonerepo` 1 commit behind `myrepo`.  Now synchronize `clonerepo` using `git pull`:

{{< action >}}
1. Get into `clonerepo`
    ```text
    $ cd ../clonerepo
    ```
2. Synchronize using `git pull`
    ```text
    $ git pull origin master
    remote: Enumerating objects: 5, done.
    remote: Counting objects: 100% (5/5), done.
    remote: Compressing objects: 100% (3/3), done.
    remote: Total 3 (delta 1), reused 0 (delta 0)
    Unpacking objects: 100% (3/3), done.
    From /Users/rod/tmp/myrepo
    * branch            master     -> FETCH_HEAD
    3560cd0..6c4312f  master     -> origin/master
    Updating 3560cd0..6c4312f
    Fast-forward
    git-cheat-sheet.txt | 1 +
    1 file changed, 1 insertion(+)
    ```
3. Confirm that `git-cheat-sheet.txt` has the new line that was added in `myrepo`.

{{< /action >}}

And that's all there is to it.  Once you have a remote configured, it is easy to synchronize your repository to a remote using `git pull`.  Again, you may run into conflicts if you have committed changes to your repository that involve the same parts as the changes in the remote, but, again, you already know how to [deal with that]({{< ref "dealing-with-conflicts" >}}).

## What About the Other Direction?

You are probably wondering: what if I want to synchronize in the other direction and have changes I committed in `clonerepo` be merged into `myrepo`?  You will learn how in the next lesson.