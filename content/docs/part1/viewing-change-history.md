---
title: "Viewing Change History"
date: 2020-05-22T11:53:35-04:00
weight: 85
---

# Viewing Change History

## Goals

By the end of this lesson you should be able to...

- View the change history of a repository using the `git log` command
- Obtain the ID for a particular commit

## Log

The `git log` command displays the change history of a repository.

{{< action >}}
Show the change history for your repository:
```text
$ git log

commit 8916e313a6fa3b38ba8674d1b2a7635f4581ef17
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Tue May 23 16:56:18 2020 -0400

    Made some content changes

commit 9d52001ee1d4c3acafb3ed78a4d7150f69f604a0
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Tue May 22 16:56:18 2020 -0400

    Added more files and text

commit 7d7596afd8f34ed4e393472ab66842ef9f0d6fbf (HEAD -> master)
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Thu May 21 10:56:08 2020 -0400

    Added another change tracking description

commit 312fabf299fbb0db418f2e7b941cb485b5c37826
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Thu May 21 10:51:43 2020 -0400

    Added a description about Git change tracking

commit 3f216521b6355ee4e767e7bee78f5ea6a9a31dab
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Mon May 18 14:07:28 2020 -0400

    Added brief description

commit 17f96677bef6833850eeaa5d4a7d01828a71a3c0
Author: Rodney Martin <rod@pennyjar.ca>
Date:   Thu May 14 14:52:20 2020 -0400

    Initial commit
```
{{< /action >}}

The default output of `git log` is a list of commits starting at the most recent one.  You are shown

- The ID for each commit (a 32-digit hexadecimal number)
- The author of the commit (set with the `user.name` and `user.email` [configurations]({{< ref "installing-and-configuring-git.md#user-info" >}}))
- The date and time at which the commit was made
- The commit message

Here is where the commit messages you have been setting on each commit are most useful: they can help you see at a glance what changes were made in each commit.  Do yourself and your team mates a favour and always use meaningful commit messages!

### Condensed Log Output

The `--oneline` option can be used to display a condensed change history, as in 

```sh
$ git log --oneline
```

{{< action >}}
Show the condensed change history for your repository:

```sh
$ git log --oneline
8916e31 (HEAD -> master) Made some content changes
9d52001 Added more files and text
7d7596a Added another change tracking description
312fabf Added a description about Git change tracking
3f21652 Added brief description
17f9667 Initial commit
```
{{< /action >}}

The condensed output shows only the commit IDs and messages (another reason to use meaningful commit messages).

You probably noticed the text `(HEAD -> master)` in the `git log` output.  This text is indicating that the `master` branch is pointing to commit `7d75`, and that `HEAD` is pointing to the `master` branch.  Let's talk more about what this means...