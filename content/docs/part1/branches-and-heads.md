---
title: "Branches and Heads"
date: 2020-05-22T14:00:24-04:00
weight: 86
---

# Branches and Heads

## Goals

By the end of this lesson you should be able to...

- Explain what a branch is in Git
- Explain what `HEAD` refers to in a Git repository

## Repository Internals

In the previous lesson you noticed that certain commits are labeled with text like `(HEAD -> master)` which indicated that the `master` branch was pointing to that commit, and that `HEAD` was pointing to the `master` branch.  

In order to understand this better let's take a look at exactly how Git represents each commit in the repository:

<figure style="width: 400px">
<img src="/images/repo-internals.png" alt="Repository Internals">
<b>Figure: Inside a Repository</b>  <br>A representation of the repository you have been working on in the activities for this tutorial
</figure>

Aside from storing the set of changes you made in each commit, Git is also maintaining a graph like the one in the figure above.  Each commit is a node in the graph pointing to the commit that came before it.

There are also some other kinds of pointers...

## Branches

We can now give a precise definition for a Git branch:  it is a pointer to the commit that the next commit on that branch will point to.  Ie, a branch points to the 'parent' of the next commit on that branch.  It's as simple as that.

## HEAD

Like a branch, `HEAD` is just another pointer.  There is only one `HEAD` per repository.  `HEAD` usually<sup>[1](#fn1)</sup> points to the branch where the next commit will be added.  There may be multiple branches in a repository, and `HEAD` determines which branch commits will be added to.

<figure style="width: 400px">
<img src="/images/repo-with-branches.png" alt="A Repository with a Branch">
<b>Figure: Branches and HEAD</b> <br>This repository has a branch named <code>mybranch</code>.  But since <code>HEAD</code> is pointing to the <code>master</code> branch commits will be added to the <code>master</code> branch.
</figure>

<div class="footnote"><a name="fn1">1</a>: <code>HEAD</code> may also point directly at commits, in which case it is referred to as a 'detached head', but that is beyond the scope of this tutorial</div>

## What Really Happens When You Commit

When you run `git commit` a new commit object is created that points to the commit indicated by `HEAD` via the branch pointer.  The branch pointer is then updated to point to the new most recent commit. As you make a sequence of commits you continue to extend the current branch.

<figure style="width: 500px">
<img src="/images/commit-graph.gif" alt="Making Commits">
<b>Figure: Making Commits</b>  <br>On each commit, a new commit object is inserted where <code>master</code> points to, then the branch pointer is updated.
</figure>

{{< hint info >}}
**NOTE:** The [Explain Git with D3](http://onlywei.github.io/explain-git-with-d3/#commit) web page was used to create the above animation.  It is also a helpful learning tool that you may use!
{{< /hint >}}

For now we will stick with the single default `master` branch, but as a preview to get you excited: you will eventually learn that you can create any number of branches at any commit in the repository, and you can move `HEAD` to wherever you like, allowing you to create 'alternate histories' of the files in your repository.  

For example, suppose you have been asked to implement a feature in a program and you would like to experiment with two different approaches.  You could create two branches, one for each approach.  Git will allow you to work on both simultaneously, switching back and forth and making commits to either one at will.  Once you have determined which approach you prefer you will be able to merge the change history of that branch into the master branch—and you will be able to do this even if other team members have been adding commits to the master branch while you have been working on the feature branch, **and** Git will help you make sure that all of this is done without introducing conflicts!

But that's all for later.  

Let's talk about one more kind of 'pointer' in a Git repository...