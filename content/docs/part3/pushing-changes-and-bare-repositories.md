---
title: "Pushing Changes and Bare Repositories"
weight: 2190
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Pushing Changes and Bare Repositories

## Goals

By the end of this lesson you should be able to

- Use the `git push` command to send changes from a repository to a remote
- Explain the difference between a bare repository and a regular repository
- Explain why it is necessary for a remote to be a bare repository in order to push to it
- Create bare repositories using the `--bare` option of the `git init` and `git clone` commands

## The Push Command

So far you have used the `git pull` command to synchronize repositories by fetching changes from a remote into your repository.  It is also possible to send your changes to a remote using the `git push` command.  

```sh
# Format for the git push command
$ git push <remote_name> <branch_name>
```

Suppose you had a remote named `origin` and you wanted to push your latest commits on the `master` branch to this remote.  The following command would append your commits to the `master` branch on the remote:

```sh
$ git push origin master
```

However, unlike the `git pull` command there are no remote branches involved.  Commits are sent directly from a local branch in one repository to a local branch in another repository.  This has the effect of causing the index and working tree of the remote to be inconsistent with its commit history, which now includes the pushed commits.

You might wonder why Git doesn't just update the index and working tree too, but remember that the remote is probably owned by another person who may be actively making changes to their working tree. They may not be happy to have other people be able to overwrite their work with a push.  But even if just the commit history is updated, it would still require some work for them to integrate your pushed changes into their working tree, which they may not be ready to do.  Git takes the pragmatic approach of refusing to push to regular repositories.

{{< action >}}
Try pushing to a regular repository:
1. Get into `clonerepo`
    ```text
    $ cd ../clonerepo
    ```
2. Add the line `The 'git pull' command fetches and merges changes from a remote` to `git-cheat-sheet.txt`
3. Commit the change
    ```text
    $ git commit -am "A note about the pull command"
    [master 79bb24a] A note about the pull command
     1 file changed, 1 insertion(+)
    ```
4. Try pushing the change to `myrepo`
    ```text
    $ git push origin master
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 385 bytes | 385.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0)
    remote: error: refusing to update checked out branch: refs/heads/master
    remote: error: By default, updating the current branch in a non-bare repository
    remote: is denied, because it will make the index and work tree inconsistent
    remote: with what you pushed, and will require 'git reset --hard' to match
    remote: the work tree to HEAD.
    remote: 
    remote: You can set the 'receive.denyCurrentBranch' configuration variable
    remote: to 'ignore' or 'warn' in the remote repository to allow pushing into
    remote: its current branch; however, this is not recommended unless you
    remote: arranged to update its work tree to match what you pushed in some
    remote: other way.
    remote: 
    remote: To squelch this message and still keep the default behaviour, set
    remote: 'receive.denyCurrentBranch' configuration variable to 'refuse'.
    To /Users/rod/tmp/myrepo
    ! [remote rejected] master -> master (branch is currently checked out)
    error: failed to push some refs to '/Users/rod/tmp/myrepo'
    ```

    Git refuses to push to `myrepo` because it is a regular repository.
{{< /action >}}

So how can we set up a repository to push to?  With something called a bare repository.

## Bare Repositories

A bare repository is one with no index or working tree.  It is essentially nothing but the `.git` directory of a regular repository.  You might wonder at first why you would want a bare repository if there is no working tree in which to work.  But you *can* pull from and push to a bare repository.

Since bare repositories have no working tree or index there are no concerns about consistency problems as discussed above.  Thus, Git allows you to push to bare repositories, making them very useful as central repositories.

You can create bare repositories using the `--bare` option of either the `git init` or `git clone` commands.

{{< hint info >}}
**NOTE:** It is convention to give bare repositories a name ending with `.git`
{{< /hint >}}

{{< action >}}
Make a bare clone of `myrepo`

$ cd ..   # Get into the parent directory of myrepo
$ git clone --bare myrepo myrepo.git
Cloning into bare repository 'myrepo.git'...
done.
{{< /action >}}

You should now have a directory named `myrepo.git` that is a bare clone of `myrepo`.  If you examine the contents of `myrepo.git` you should see that it is very similar to the contents of the `.git` folder in `myrepo`.

Now try pushing that change from before to this bare repository:

{{< action >}}
1. Get into `clonerepo`
    ```text
    $ cd clonerepo
    ```
2. Add `myrepo.git` as a remote (you will need to use a different path according to your directory structure)
    ```text
    $ git remote add central /Users/rog/tmp/myrepo.git
    ```
3. Push the changes you made previously to this central remote
    ```text
    $ git push central master
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 385 bytes | 385.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0)
    To /Users/rod/tmp/myrepo.git
        6c4312f..79bb24a  master -> master
4. Get into `myrepo` (not `myrepo.git`)
    ```text
    $ cd ../myrepo
    ```
5. Add `myrepo.git` as a remote (you will need to use a different path according to your directory structure)
    ```text
    $ git remote add central /Users/rog/tmp/myrepo.git
    ``` 
6. Pull the changes from the central remote
    ```text
    $ git pull central master
    From /Users/rod/tmp/myrepo
     * branch            master     -> FETCH_HEAD
     * [new branch]      master     -> central/master
    Updating 6c4312f..79bb24a
    Fast-forward
     git-cheat-sheet.txt | 1 +
     1 file changed, 1 insertion(+)
7. Confirm that the note about the pull command has been merged into `git-cheat-sheet.txt` in `myrepo`.
{{< /action >}}

If all went well, you successfully created a bare repository, pushed a change to it from one repository and then pulled that change into another repository.  You could now treat `myrepo.git` as a central repository to which everyone working on this repository must synchronize using `git pull` and `git push`.

## Pull Before You Push

Before moving on, there is one more thing you should know about pushing:  Git will also refuse to push to a repository that has more recent commits than that of your remote branch for that repository.

Imagine the following sequence:

1. You pull the most recent changes from a central remote
1. You commit some changes to your repository
1. Meanwhile, another team mate pushes changes they have made to the same central repository
1. You try to push your changes to the central repository

Or this sequence:

1. You have cloned a central repository to both a work computer and a home computer
1. You commit and push some changes to the central repository from your work computer
1. Later, on your home computer you commit some changes and try to push these changes to the central repository

In both of these sequences, the final push will fail.  In the first case, someone else has pushed commits that you have not yet fetched into your remote branch that tracks the remote repository.  In the second case, you yourself pushed commits to the remote from one computer but you have not yet fetched them into the repository on your other computer.

The fix in both cases is to do a pull first.  Once you pull (and resolve any merge conflicts if necessary) then your remote branch and the remote repository will have the same commit history, allowing Git to push your commits to the remote repository without creating conflicts on the remote.  (It may, of course, create conflicts for other people when they pull your changes from the remote.  But they will need to resolve those conflicts in their local repositories before they can push their changes up to the central repository.)

In the next lesson you will learn how to host remote repositories using online services such as GitHub.