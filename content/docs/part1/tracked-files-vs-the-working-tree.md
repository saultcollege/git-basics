---
title: "Tracked Files vs the Working Tree"
date: 2020-05-12T15:23:18-04:00
weight: 40
---

# Tracked Files vs the Working Tree

## Goals

By the end of this lesson you should be able to...

- Define what is meant by the terms 'tracked file' and 'working directory' in Git
- Understand how the working directory of a Git repository relates to the repository itself

## Definitions

### Tracked File

A **tracked file** is a file for which Git is keeping track of change history.  This history is stored automatically by Git inside the `.git` folder, and it is this history of all tracked files that technically comprises a Git repository.

### Working Tree

The set of files actually on disk in your repository *directory* (aside from the files inside the `.git` directory) is called the **working tree** or **working directory**.  Think of the working tree as a copy of the repository plus any uncommitted changes you have made.

### Repository

Technically, a Git **repository** is *only* the history of changes of all tracked files which is managed automatically by Git inside the `.git` directory.  Untracked files and changes not yet committed are not part of the repository.

When you add a file to the working tree it is not yet a part of the repository (ie, it is untracked).  When you make a changes to a tracked file, you must commit that change in order to record it in the repository.

{{< hint info >}}
**NOTE:** 
You may find that the term 'repository' has a somewhat ambiguous meaning in real-world use.  When people speak of a 'Git repository' they often mean both their working tree and the repository proper.  It is useful, however, to understand the distinction between the two because it makes it easier to understand how Git works.
{{< /hint >}}