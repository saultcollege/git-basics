---
title: "Dealing With Conflicts"
weight: 2070
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Dealing with Conflicts

## Goals

By the end of this lesson you should be able to 

- Understand Git's syntax for annotating conflicts during a merge
- Abort a merge using the `--abort` option of the `git merge` command
- Resolve and complete merges that encounter conflicts

## Creating a Conflict

To start, let's make some changes in our two branches that will result in a conflict.  Add lines to the end of `git-cheat-sheet.txt` in both branches:

{{< action >}}
1. In the `master` branch, add the following lines to `git-cheat-sheet.txt`:
`The 'git branch' command can be used to list and create branches` and 
`The 'git switch' command can be used to set the active branch`
2. Commit this change
    ```text
    $ git commit -am "Notes about the branch and switch commands"
    [master 37a381b] Notes about the branch and switch commands
     1 file changed, 2 insertions(+)
    ```
3. Switch to `mybranch`
    ```text
    $ git switch mybranch
    Switched to branch 'mybranch'
    ```
4. In the `mybranch` branch, add the following line to `git-cheat-sheet.txt`: `The 'git merge' command can be used to merge changes in two branches`
5. Commit this change
    ```text
    $ git commit -am "A note about the merge command"
    [mybranch ff2b08d] A note about the merge command
     1 file changed, 1 insertion(+)
    ```
{{< /action >}}

You should have noticed the `git-cheat-sheet.txt` in `mybranch` still does not have any of the new lines that have been added in `master`.  This is because when we merged previously we merged `mybranch` *into* `master` and not the other way around.

Your commit history now looks something like the figure below (but with different commit ids).  Note that each branch again has a new commit (the two commits you just made above).

<figure>
<img src="/images/branches-6.png" alt="Before a Conflict Merge">
<b>Figure: Before a Conflict Merge</b>
</figure>

## Merging with Conflicts

Now let's try merging these two branches again

{{< action >}}
Switch to `master` then merge in `mybranch`:

```text
$ git switch master
$ git merge -m "Merge mybranch into master" mybranch
Auto-merging git-cheat-sheet.txt
CONFLICT (content): Merge conflict in git-cheat-sheet.txt
Automatic merge failed; fix conflicts and then commit the result.
```
{{< /action >}}

Git indicates that a conflict has occurred, and tells us which files contain conflicts.  In our case there is a single file, but it is possible for conflicts to occur in multiple files or even multiple places in a single file.  Git also tells us to fix the conflicts and commit the result.

Before moving on, take a look at the current status of your repository:
{{< action >}}
```text
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   git-cheat-sheet.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
{{< /action >}}

Note that Git is warning us about 'unmerged paths'.  There are two courses of action:

1. Fix the conflict and commit the fix, or
2. Abort the merge using the `git merge --abort` command

Your repository is currently in a mid-merge state.

{{< hint warning >}}
**IMPORTANT:** If a merge fails due to conflicts, it is important to resolve the conflict either by aborting the merge or making a commit that contains the conflict resolution.  Failing to do so leaves your repository in an in-between state that will cause further difficulties.
{{< /hint >}}

## Aborting Conflicts

In the case of a merge conflict, the `--abort` option of the `git merge` command allows you to restore your repository to the state it was in before the merge, as in:

```sh
$ git merge --abort  # Abort the current merge
```

## Resolving Conflicts

To resolve conflicts, you must examine and edit the files that Git could not merge automatically.  Let's see what Git has done with `git-cheat-sheet.txt`:

```text
$ cat git-cheat-sheet.txt
Git Cheat Sheet

Git is a distributed version control system
Git records changes in files, not the current state of files
Changes in the working tree that have not been staged will not be committed


The 'git init' command is used to initialize a Git repository
The 'git add' command adds changes to the index
<<<<<<< HEAD
The 'git commit' command records on the active branch all changes that have been added the index
The 'git restore' command can be used to undo changes
The 'git branch' command can be used to list and create branches
The 'git switch' command can be used to set the active branch
=======
The 'git merge' command can be used to merge changes in two branches
>>>>>>> mybranch
```

Note that Git has added a few lines that start with either `<<<<<<<`, `=======`, or `>>>>>>>`.  You will eventually remove these lines, but Git has added them to make it easy to find points of conflict.

The content between the first `<<<<<<<` and the `=======` are the lines in the active branch (in this case `master`); the content from the `=======` to the final `>>>>>>>` are the lines from the incoming branch (in this case `mybranch`).  

Git was not able to decide automatically how to merge these lines, so it is now up to you to make the decision.  There are no restrictions—you may decide to keep all the lines, none of the lines, only the lines from one or the other of the branches, or some from both.  In some cases you may even need to reorder certain lines.  You need to carefully examine the lines in the conflict and decide how to resolve the conflict properly.  (You could even keep the conflict annotations, they are just text after all, but you would never want to.)

{{< hint info >}}
**NOTE:** You will also find that many development environments and text editors understand the Git conflict annotations, and add helpful UI elements to make resolving conflicts simpler.

For example, below is a screenshot of the UI when `git-cheat-sheet.txt` is opened using Visual Studio Code.  Note the colouring and the row of text buttons above the conflict; all these elements are generated by Visual Studio Code based on the Git annotations.

<figure>
<img src="/images/vscode-conflict.png" alt="VS Code Conflict">
<b>Figure: A Conflict in VS Code</b>
</figure>

{{< /hint >}}

In the present case we want to keep all the lines.  Let's complete this merge:

{{< action >}}
1. Open `git-cheat-sheet.txt` and remove the Git conflict annotations but leave all the lines from both branches.
2. Commit your changes
    ```text
    $ git commit -am "Merge mybranch into master"
    [master 6ba2205] Merge mybranch into master
    ```
3. Display the log
    ```text
    $ git log --oneline --graph
    *   6ba2205 (HEAD -> master) Merge mybranch into master
    |\  
    | * ff2b08d (mybranch) A note about the merge command
    * | 37a381b Notes about the branch and switch commands
    * |   737f014 Merge mybranch into master
    |\ \  
    | |/  
    | * 663e99a Title change
    * | 1ebc7b1 A note about the restore command
    * | 70b4290 A note about the commit command
    |/  
    * 08f4897 (tag: anothertag) Renamed git.txt
    * 714c41e Removed unnecessary files
    ...
    ```

{{< /action >}}

Your commit history graph now looks something like this:

<figure>
<img src="/images/branches-7.png" alt="After a Conflict Merge">
<b>Figure: After the Conflict Merge</b>
</figure>

And now you know the basics of branching and merging in Git!