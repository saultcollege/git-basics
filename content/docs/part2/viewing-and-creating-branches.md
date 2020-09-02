---
title: "Viewing and Creating Branches"
weight: 2020
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Viewing and Creating Branches

## Goals

By the end of this lesson you should be able to

- Use the `git branch` command to view, create, and delete branches in a repository
- Use the `git log` command to see which commits branches are pointing to

## The Branch Command

### Listing and Creating Branches

The `git branch` command can be used to list or create branches.

```sh
$ git branch                     # list all branches in the repository
$ git branch <name> [<commit_id>]  # create a branch with the given name
```

When you create a new branch it will point to the commit specified by `<commit_id>`.  If no `<commit_id>` is specified it will point to the same commit as `HEAD`.

{{< action >}}
List the branches in your repository:

```text
$ git branch
* master
```

You have only one branch named `master`.  The `*` indicates the current active branch.

Now create two new branches, one named `mybranch` pointing at `HEAD` and one named `temp` pointing at a previous commit of your choice, then list them:
```sh
$ git branch mybranch
$ git branch temp b2764  # You will need to use a different commit ID
$ git branch
* master
  mybranch
  temp
```

You now have three branches.  The `master` branch is still the active branch.

{{< / action >}}

### Examining Branches using the Log

Recall that the `git log` command indicates any objects that are pointing to each commit.

{{< action >}}
Confirm that your new branches are pointing at the expected commits:

```text
$ git log --oneline
08f4897 (HEAD -> master, tag: anothertag, mybranch) Renamed git.txt
714c41e Removed unnecessary files
39fa5fc Revert "Revert "Added note about the 'git add' command""
b2763fe (temp) Revert "Added note about the 'git add' command"
87af010 Added note about the 'git add' command
...
```

Note the following:

- `HEAD` is pointing to `master` (this is what makes `master` the active branch)
- `mybranch` and `master` point to the same commit
- `temp` points to a previous commit

{{< /action >}}

As you can see, the log output indicates which commit each branch is 

### Deleting Branches

The `--delete` or `-d` option can be used to remove a branch, as in

```sh
# Format for deleting a branch
$ git branch -d <name>
```

{{< action >}}
Delete the `temp` branch you just created

```text
$ git branch -d temp
Deleted branch temp (was b2763fe).
```

{{< /action >}}
