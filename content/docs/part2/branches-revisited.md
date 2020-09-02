---
title: "Branches Revisited"
weight: 2010
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Branches Revisited

In [Part 1]({{< ref "branches-and-heads" >}}) we introduced Git branches as pointers to specific commits.  When using Git, one branch is active at a time (the HEAD pointer in Git determines which is the active branch), and commits are appended to the commit being pointed to by the active branch.  

<figure style="width: 500px">
<img src="/images/commit-graph.gif" alt="Making Commits">
<b>Figure: Making Commits</b>  <br>On each commit, a new commit object is inserted where <code>master</code> points to, then the branch pointer is updated.
</figure>

All Git repositories are initialized with one branch named `master`, but you may create any number of branches and switch between them.  Git will automatically alter the contents of your working tree to be that of the active branch.  Furthermore, Git uses branches behind the scenes to manage the synchronization of multiple related repositories.  Let's see how that works!
