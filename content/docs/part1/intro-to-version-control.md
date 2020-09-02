---
title: "Intro to Version Control"
weight: 10
---

# Intro to Version Control

## Goals
By the end of this lesson you should be able to
- Define what a Version Control System is
- Distinguish a distributed vs a centralized version control system

## The Purpose of Version Control

When working on a software program that is even somewhat complex you will often be working on features of your program that involve changes in many different files.  You may even be working on multiple features at once.  How can you keep track of which changes apply to which feature?  What if both features require changes in the same segment of code?

It is also often the case that other people are working on the program at the same time as you.  They may work on a separate copy of the code files and make changes, possibly in the same files and even same lines of code that you are making changes in.  How can you coordinate all these changes without drowning in confusion?  

A Version Control System<sup>[1](#fn1)</sup> (VCS) is the tool you need!  

Git is a VCS.

{{< hint info >}}
**NOTE:** Git is not the only VCS (although it is the most popular).  Some other VCSs you may encounter: [Mercurial](https://www.mercurial-scm.org/), [Subversion](https://subversion.apache.org/), [CVS](https://nongnu.org/cvs/).
{{< /hint >}}

<div class="footnote">
<a name="fn1">1</a>:  You may also encounter the term "Source Code Management" (SCM), which means the same thing as "Version Control System" (VCS).
</div>

## What is a Version Control System?

A VCS is a tool that makes it simple to track all changes in a set of files.  (This set of files along with its history of changes is usually called a 'repository'.)  Changes in a repository are tracked by instructing the VCS to take a 'snapshot' of the set of files at specific times chosen by the user.  Once a snapshot has been taken, a VCS will usually provide tools to examine any previous snapshot, compare any two snapshots, and revert files to the state they had in a previous snapshot.

This aspect of a VCS is similar to a backup system such as MacOS's Time Machine, which periodically saves the state of the files on a computer system and allows the user to revert any file to a previous state.  A VCS is different, though, in that the user manually triggers the saving, and backup systems like Time Machine don't have the ability to examine the exact differences and changes in files over time.

Another important aspect of a VCS that is different from a plain backup system is that it facilitates collaboration among teams of programmers by ensuring that two people don't overwrite each other's work when they make changes to the same lines in a file.  In fact, a VCS is often able to automatically merge changes made by multiple users to the same file(s).

{{< hint info >}}
**NOTE:** Usually the files stored by a VCS are text files such as the code files for a software program.  Binary files such as images and compiled code can be stored in a VCS as well, but comparison between different revisions of a binary file is often not possible.
{{< /hint >}}

## Centralized vs Distributed Version Control

There are two main categories of VCS: centralized and distributed.  Git is a distributed VCS.

{{< columns >}}

### Centralized

In a centralized VCS, the main repository of files is shared on a central server that programmers working on the files may connect to.  Changes made by individuals must be committed to this central repository using the VCS, and programmers must synchronize with this repository (again using the VCS) before their changes may be committed.

The history of changes in a centralized VCS is only stored in the central repository, meaning that individual programmers must communicate with the central server in order to do file comparisons and reversions.

Subversion and CVS are examples of centralized VCSs.

<figure>
<img src="/images/centralized-vcs.png" alt="Centralized VCS">
<b>Figure: Centralized VCS</b><br>No change history in local repositories  means every VCS operation requires communication with central server.
</figure>

<--->

### Distributed

In a distributed VCS the change history of the files in a repository are stored somewhere within each local copy of the repository.  Thus, file comparisons and reversions may be done without communicating with any external server!  

Furthermore, users may synchronize their file repositories with any other repository that shares the same history.  

The process of synchronizing changes is somewhat more complex than that of a centralized VCS, but the advantages outweigh the disadvantage of having to communicate with a central server for every VCS operation.

Git and Mercurial are examples of decentralized VCSs.

<figure>
<img src="/images/distributed-vcs.png" alt="Distributed VCS">
<b>Figure: Distributed VCS</b><br>
Complete change history in all repositories means they can be synchronized with any repository that shares the same history, and VCS operations may run locally.
</figure>

{{< /columns >}}


