---
title: "Track a New File"
date: 2020-05-19T16:05:58-04:00
weight: 45
---

# Track a New File

## Goals

By the end of this lesson you should be able to...

- Use the `git add` command to tell Git which new files in your working tree to start tracking


## Tracking Files

{{< action >}}
In your `myrepo` directory, create a file named 'git.txt' that contains some text, then check the repository status:

```text
$ echo "Git" > git.txt   # Add the word "Git" to a file named git.txt
$ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	git.txt
nothing added to commit but untracked files present (use "git add" to track)
```
{{</ action >}}

Note the new 'Untracked files' section in the status output.  Git sees that `git.txt` is there but it is not tracking its change history—it is part of the working tree, but not part of the repository.

Note also the `git add <file>...` message in the status output.  Git is quite good at giving you hints about what may need to be done, and this is one example.

## Add

You can tell Git to track new files using the `git add` command.

```sh
# Add command format
git add <files>
```

You may specify a single file path, or a set of file paths (each path separated by a space), and the paths may contain globs (eg. `*.txt` to add all files ending in `.txt` or `foo/*` to add all files in a directory named `foo`.)

{{< action >}}
Add the `git.txt` file to be tracked, then check the status again:

```text
$ git add git.txt
$ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   git.txt
```
{{< /action >}}

The `git.txt` file is now being tracked, meaning that Git will detect any changes to the file.  But note that it has not yet been 'committed', meaning it is still not yet part of the repository<sup>[1](#fn1)</sup>!  Let's fix that now...

<div class="footnote"><a name="fn1">1</a>: It may seem strange that the file is not part of the repository even after adding it using <code>git add</code>, but the workflow will make more sense soon.  Keep reading!</div>