---
title: "Seeing What Changed"
date: 2020-05-22T10:57:57-04:00
weight: 95
---

# Seeing What Changed

## Goals

By the end of this lesson you should be able to...

- Use the `git show` and `git diff` commands to inspect changes recorded in your repository

## Show

The `git show` command shows all the changes that were made in a particular commit.

```sh
# Format for git show
git show [<commit_id>]
```

If no commit ID is specified, the commit indicated by `HEAD` is used.

{{< action >}}
Show the changes in the most recent commit:

```text
$ git show
commit 7d7596afd8f34ed4e393472ab66842ef9f0d6fbf (HEAD -> master)
Author: Rodney Martin <rod@email.com>
Date:   Thu May 21 10:56:08 2020 -0400

    Added another change tracking description

diff --git a/git.txt b/git.txt
index 99de68c..35fd8aa 100644
--- a/git.txt
+++ b/git.txt
@@ -2,6 +2,7 @@ Git
 
 Git is a distributed version control system
 Git records changes in files, not the current state of files
+Changes in the working tree that have not been staged will not be committed
 
 
 The 'git init' command is used to initialize a Git repository

```
{{< /action >}}

The output of `git show` includes the commit information that you have already encountered with `git log`, but it also includes a 'diff'.  A diff is a record of only the changes between one set of files and another.

## Reading Diff Output

The output of a diff may seem like random symbols at first but it all has meaning.  You do not need to know all the details except for the following<sup>[1](#fn1)</sup>: 

Lines starting and ending with `@@` indicate a chunk of lines in the file that have changed in some way.  Below each `@@` heading will be any number of lines, some of which begin with a `-` or `+`.  Such lines are deletions or insertions, respectively, when comparing the two revisions of the file in question.  Lines that do not begin with a `-` or `+` are just context around the insertions and deletions being shown.

Thus, in the output above Git is indicating that in commit `7d75` `git.txt` had a single insertion: the line `Changes in the working tree that have not been staged will not be committed`.

Let's look at a more complicated example.  Suppose there were two revisions of a file, A and B

{{< columns >}}

A

```
Hello, world!

This is some text.
There are several lines of text.
This is the last line of text.
```

<--->

B

```
MY DOCUMENT

Hello, world!

This is some more text.
There are several lines of text.
```

{{</ columns >}}

Here is what the diff for these two revisions would look like:

```diff
diff --git a/a.txt b/a.txt
index 94e1883..2ceb5b9 100644
--- a/a.txt
+++ b/a.txt
@@ -1,5 +1,6 @@
+MY DOCUMENT
+
 Hello, world!
 
-This is some text.
+This is some more text.
 There are several lines of text.
-This is the last line of text.
```

You can see here the three different kinds of changes you can make to a file:  Insertions, deletions, and modifications.  Insertions and deletions are simply chunks that all start with either `+` or `-` respectively.  Modifications are indicated with one set of deletions followed immediately by one set of insertions, as you can see in the change from `This is some text.` to `This is some more text.`.

<div class="footnote"><a name="fn1">1</a>: If you would like to learn more about how to read a diff <a href="https://stackoverflow.com/a/2530012/1030345">this StackOverflow answer</a> is a good place to start</div>

## Diff

The `git diff` command can be used to examine the difference between revisions of a file.

### Working Tree vs Index

The default behaviour of `git diff` is to compare the unstaged changes with the staged changes of a file.

```sh
# Compare all changes
git diff

# Compare all changes in a file named foo.txt
git diff foo.txt

# Compare all changes in a directory named foo
git diff foo/*
```

### Working Tree vs Most Recent Commit

You can specify `HEAD` as the specifc commit to compare with instead of the index.  (If term `HEAD` is not familiar see [this page]({{< ref "branches-and-heads.md" >}}).)

```sh
# Compare all changes
git diff HEAD

# Compare all changes in a file named foo.txt
git diff HEAD foo.txt

# Compare all changes in a directory named foo
git diff HEAD foo/*
```

### Working Tree vs Older Commit

You can specify a commit ID as the specifc commit to compare with instead of the index.  You may use a [unique prefix]({{< ref "viewing-change-history.md#commit-ids" >}}) of any commit ID.  (Your commit IDs will be different than the one used below.)

```sh
# Compare all changes
git diff 2e44

# Compare all changes in a file named foo.txt
git diff 2e44 foo.txt

# Compare all changes in a directory named foo
git diff 2e44 foo/*
```

### Staged Changes vs Most Recent Commit

The `--staged` option allows you to compare staged changes instead of working tree changes.  Staged changes are compared with the most recent commit.

```sh
# Compare all changes
git diff --staged

# Compare all changes in a file named foo.txt
git diff --staged foo.txt

# Compare all changes in a directory named foo
git diff --staged foo/*
```

### Staged Changes vs Older Commit

Just like the normal command you can include a commit ID to pick a specific commit other than the most recent one to compare with.

```sh
# Compare all changes
git diff --staged 2e44

# Compare all changes in a file named foo.txt
git diff --staged 2e44 foo.txt

# Compare all changes in a directory named foo
git diff --staged 2e44 foo/*
```

### One Commit vs Another Commit

Finally, you can specify two commit IDs to show the differences between those two commits.


```sh
# Compare all changes
git diff 2e44 f33d

# Compare all changes in a file named foo.txt
git diff 2e44 f33d foo.txt

# Compare all changes in a directory named foo
git diff 2e44 f33d foo/*
```

{{< action >}}
Use the `git diff` command in its various formats to examine the differences between various parts of your repository, index, and working directory.
{{< /action >}}