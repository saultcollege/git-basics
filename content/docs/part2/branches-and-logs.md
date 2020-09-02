---
title: "Branches and Logs"
weight: 2050
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Branches and Logs

## Goals

By the end of this lesson you should be able to

- Use the `--all` option of the `git log` command to display commits regardless of which branch is active
- Use the `--graph` option of the `git log` command to give a better visualization of the commit graph

## Using the `--all` Option

{{< action >}}
Switch back to the `mybranch` branch and view the log output
```text
$ git switch mybranch
$ git log --oneline
08f4897 (HEAD -> mybranch, tag: anothertag) Renamed git.txt
714c41e Removed unnecessary files
39fa5fc Revert "Revert "Added note about the 'git add' command""
b2763fe Revert "Added note about the 'git add' command"
...
```

Note that `HEAD` is indeed pointing to `mybranch`.
But oh no!  Where did the two most recent commits on `master` go?
{{< /action >}}

When you run `git log` on a specific branch, it will display any commits previous to the most recent one on the active branch.  If you want to see *all* commits, even those subsequent to the most recent one on the active branch, the `--all` option can be useful:

{{< action >}}
Show the log using the `--all` option
```text
$ git log --all --oneline
1ebc7b1 (master) A note about the restore command
70b4290 A note about the commit command
08f4897 (HEAD -> mybranch, tag: anothertag) Renamed git.txt
714c41e Removed unnecessary files
39fa5fc Revert "Revert "Added note about the 'git add' command""
b2763fe Revert "Added note about the 'git add' command"
...
```

Ah ha!  There's `master` and the two most recent commits.  They were never lost, Git just doesn't display them in the log by default while the `mybranch` branch is active.
{{< /action >}}

## Using the `--graph` Option

Let's make a change in our `mybranch` branch:

{{< action >}}
1. With the `mybranch` branch active, change the first line of `git-cheat-sheet.txt` from just `Git` to `Git Cheat Sheet`
2. Commit this change:
    ```text
    $ git commit -am "Title change"
    [mybranch 663e99a] Title change
     1 file changed, 1 insertion(+), 1 deletion(-)
    ```
{{< /action >}}

At this point, your commit history graph looks something like this:

<figure style="width: 500px">
<img src="/images/branches-4.png" alt="Branches">
<b>Figure: Commits to Branches</b> Both the master and mybranch branches have had commits made to them since their branch point at commit 08f4.
</figure>

As an aside, it should now be more clear why branches are called branches.  As you add commits to a branch the chain of commits branches off from the branch point.  In the example here, commit `08f4` is the most recent common commit between `master` and `mybranch`.  There has been 1 commit to the `mybranch` branch, and 2 commits to the `master` branch since that common commit.

This branching graph can be displayed by the `git log` command using the `--graph` option!  Compare the output of the `git log` command with and without the `--graph` option:

{{< columns >}}

**Without the `--graph` option**

```text
$ git log --all --oneline
663e99a (HEAD -> mybranch) Title change
1ebc7b1 (master) A note about the restore command
70b4290 A note about the commit command
08f4897 (tag: anothertag) Renamed git.txt
714c41e Removed unnecessary files
...
```
<--->

**With the `--graph` option**
```text
$ git log --all --oneline
* 663e99a (HEAD -> mybranch) Title change
| * 1ebc7b1 (master) A note about the restore command
| * 70b4290 A note about the commit command
|/  
* 08f4897 (tag: anothertag) Renamed git.txt
* 714c41e Removed unnecessary files
...
```
{{< /columns >}}

Git has added some ASCII graphics to help visually separate the commits of different branches.  An `*` marks each commit. Branch points are marked using the character sequence `|/`, and commits in the same branch are indented to the same level and connected with a line of `|` characters.


{{< hint info >}}
**NOTE:** While the branch graph can be displayed using command line Git using the `--graph` option as shown above, this is a use case where Git GUIs are superior.  Below, for example, is how our repository looks using a free GUI called Sublime Merge.

<figure>
<img src="/images/sublime-merge.png" alt="Sublime Merge">
<b>Figure: Sublime Merge</b>
</figure>

Not only is the commit graph easier to understand, you can also see in the same screen exactly what changed in the selected commit.

{{< /hint >}}