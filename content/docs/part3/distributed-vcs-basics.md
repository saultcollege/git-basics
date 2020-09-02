---
title: "Distributed VCS Basics"
weight: 2110
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Distributed VCS Basics

Git is a distributed version control system, meaning that you may have many copies of a repository and Git will help you keep all the copies in sync.  Having just learned about branches in Git you might wonder why you would want multiple copies of a repository.  Why not just use one repository with multiple branches?

The reason is that often you will be working with a team of people, and each individual will need a copy of the repository on their computer.  Another common need is to be able to work on a repository from multiple devices, perhaps a work computer and a personal computer at home—each device can have a copy of the repository.  

Git will help you make sure that changes made in one copy get applied correctly in other copies.

<figure style="width:400px" >
<img src="/images/distributed-vcs.png" alt="Distributed VCS">
<figcaption>
<b>Figure: Distributed VCS</b></figcatpion>
</figure>

So how can you manage multiple copies of the same repository using Git?  Read on to find out!