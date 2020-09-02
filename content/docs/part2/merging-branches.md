---
title: "Merging Branches"
weight: 2060
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Merging Branches

## Goals

By the end of this lesson you should be able to 

- Use the `git merge` command to combine the changes in two branches

## Merging

There will come a time when you want the changes in one branch to be incorporated into another.  Suppose in our example we would like to bring the `mybranch` changes into the `master` branch.  The `git merge` command will help you acheive this.

```sh
$ git merge -m "<message>" <branch>  # Merge the named branch into the active branch
```

The `-m` option is much like that of the `git commit` command: it is a place to note the reason for the merge.  As you will see, a merge will ultimately create a new commit and the merge message becomes that new commit's message.

{{< hint info >}}
**NOTE:** It is important to keep the direction of a merge in mind: `git merge <branch>` will merge the changes from `<branch>` *into* the active branch.  If you want to go in the opposite direction you would need to switch to `<branch>` first, then merge in the other branch.
{{< /hint >}}

Recall the state of your repository: in your `mybranch` branch you have changed the title in `git-cheat-sheet.txt`; in `master` you have added two new lines to the end of `git-cheat-sheet.txt`.  Let's see what happens when we merge `mybranch` into `master`:

{{< action >}}
Switch to `master` then merge `mybranch`

```text
$ git switch master
$ git merge -m "Merge mybranch into master" mybranch
Auto-merging git-cheat-sheet.txt
Merge made by the 'recursive' strategy.
 git-cheat-sheet.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Now examine the `git-cheat-sheet.txt` file.  The changes from both branches have been automatically applied!

What does your log look like now?

```text
$ git log --oneline --graph
*   737f014 (HEAD -> master) Merge mybranch into master
|\  
| * 663e99a (mybranch) Title change
* | 1ebc7b1 A note about the restore command
* | 70b4290 A note about the commit command
|/  
* 08f4897 (tag: anothertag) Renamed git.txt
* 714c41e Removed unnecessary files
* 39fa5fc Revert "Revert "Added note about the 'git add' command""
...
```

{{< /action >}}

As you can see, Git has automatically created a new commit with the merge message that you provided in the `git merge` command.  This commit is unlike other commits we have encountered so far because it has two 'parents': `663e` from `mybranch` and `1ebc` from `master` (your commit IDs will be different).  This indicates that the changes from both branches have been applied in the merge commit.

Here is how your commit history looks now:

<figure>
<img src="/images/branches-5.png" alt="After a Merge">
<b>Figure: A Merge Commit</b>
</figure>

Unfortunately, Git cannot automatically merge all changes.  Sometimes Git will force you to resolve conflicts manually. This usually occurs when changes in both branches being merged are made on the same line of a file.  Let's learn how to deal with this situation...