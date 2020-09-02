---
title: "Cloning Repositories"
weight: 2120
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Cloning Repositories

## Goals

By the end of this lesson you should be able to 

- Use the `git clone` command to clone a repository

## The Clone Command

In order to copy a repository the usual approach is to use the `git clone` command:

```sh
# Format of the clone command
$ git clone <original> [<copy>]
```

`<original>` is the path to the repository being copied, and `<copy>` is the path to copy to.  If `<copy>` is not specified then Git will give the copy the same name as the original and place it in the current working directory.

{{< hint warning >}}
**NOTE:** Cloning is **not** the same as simply copying the repository directory.  We will discuss the reasons as we encounter them.
{{< /hint >}}

{{< action >}}
Clone your repository and call it `clonerepo`

```sh
$ cd ../  # navigate to the directory containing your myrepo folder
          # (you may need to use a different path for the cd command)
$ git clone myrepo clonerepo
Cloning into 'clonerepo'...
done.
```
{{< /action >}}

If you run an `ls` you should now see both the `myrepo` and `clonerepo` directories.

Let's investigate this cloned repository a bit...

{{< action >}}
Do a `git status` in both `myrepo` and `clonerepo`:

```sh
$ cd myrepo
$ git status
On branch master
nothing to commit, working tree clean

$ cd ../clonerepo
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

Now check the log:

```text
$ git log --oneline
6ba2205 (HEAD -> master, origin/master, origin/HEAD) Merge mybranch into master
ff2b08d (origin/mybranch) A note about the merge command
37a381b Notes about the branch and switch commands
737f014 Merge mybranch into master
...
```

{{< /action >}}

Notice the extra line of text `Your branch is up to date with 'origin/master'` in the status of the cloned repository.  Notice also three new labels, `origin/master`, `origin/HEAD`, and `origin/mybranch` in the log.

We will discuss the meaning of these new labels in the next few lessons...