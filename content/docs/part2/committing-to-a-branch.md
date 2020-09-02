---
title: "Committing to a Branch"
weight: 2030
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Committing to a Branch

## Goals

By the end of this lesson you should be able to
 
- Explain how branch pointers will update as you make commits

### Working with Branches

Right now, your repository looks something like the figure below (but your commit IDs will be different):

<figure style="width: 500px">
<img src="/images/branches-1.png" alt="Branches">
<b>Figure: Initial Branch Configuration</b>
</figure>

In the next few lessons you will experiment with how Git behaves as you work in different branches.  For now, let's commit a couple changes to the `master` branch and see the result.

{{< action >}}
1. Add the following line of text to the `git-cheat-sheet.txt` file: `The 'git commit' command records on the active branch all changes that have been added the index`.
2. Commit this change:
   ```text
   $ git commit -am "A note about the commit command"
   [master 70b4290] A note about the commit command
    1 file changed, 1 insertion(+)
   ```
3. Add another line of text to the `git-cheat-sheet.txt` file: `The 'git restore' command can be used to undo changes`.
4. Commit this change too:
   ```text
   $ git commit -am "A note about the restore command"
   [master 1ebc7b1] A note about the restore command
    1 file changed, 1 insertion(+)
   ```
5. View the log:
    ```text
    $ git log --oneline
    1ebc7b1 (HEAD -> master) A note about the restore command
    70b4290 A note about the commit command
    08f4897 (tag: anothertag, mybranch) Renamed git.txt
    714c41e Removed unnecessary files
    39fa5fc Revert "Revert "Added note about the 'git add' command""
    ...
    ```

Note the following:

- `master` points to the most recent commit
- `mybranch` points to the same commit that it did before

{{< /action >}}

As you make commits, those commits get appended to the active branch.  Other branches are left where they are.

The graph of commits in your repository now looks something like the figure below:

<figure style="width: 500px">
<img src="/images/branches-2.png" alt="Branches">
<b>Figure: Final Branch Configuration</b>
</figure>
