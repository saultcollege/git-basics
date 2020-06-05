---
title: "Git GUIs"
date: 2020-06-05T11:33:45-04:00
weight: 145
---

# Git GUIs

In this tutorial we have focused on using command line Git, which is an important skill for programmers to obtain because it allows you to use Git anywhere it is installed.  (Git is primarily a command line application.)

However, there are many Graphical User Interfaces (GUIs) for Git.  The Git website maintains a long [list of available Git GUIs](https://git-scm.com/downloads/guis/).  You should be able to point any of these GUIs at any Git repository directory and use Git via the GUI.

<figure>
<img src="/images/git-gui.png" alt="A Git GUI">
<b>Figure: A Git GUI</b><br>This is a screenshot of Git Extensions, a free cross-platform Git GUI, showing the changes made in a specific file at a specific commit.  Also easily visible: Commit messages and IDs, and commit authors.
</figure>

Most popular programming text editors and development environments also have some degree of built-in Git integration.

Now that you are familiar with the basic concepts of Git you should find any of these GUIs fairly intuitive.  The same process is followed: make working tree changes, stage any changes you would like to commit, then commit all staged changes.

## When a GUI is Better

For many Git operations, running a simple command in a shell is simpler than loading up a GUI and finding the right buttons to click, however there are some ways in which a GUI can make working with Git much easier:

- Viewing the differences between revisions is often nicer in a GUI
- Selecting specific changes to stage (including selecting only some changes but not others within a single file) is often more intuitive with a GUI
- GUIs usually have a graphical presentation of the commit history, which can make it easier to visualize and understand