---
title: "Git Workflows"
weight: 2180
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Git Workflows

So far you have been working with two related repositories, pretending that each was 'owned' by a separate person on a team.  Of course, there might be any number of individuals on a team, each with their own repository clone.  Unfortunately, it can become difficult to coordinate changes if everyone is regularly committing to their repositories.

<figure style="width: 300px; margin:auto">
<img src="/images/workflow-1.png" alt="Distributed Workflow"><br>
<b>Figure: Distributed Repositories</b><br>In a truly distributed workflow, each team member is responsible for pulling changes from every other team member as needed.
</figure>

To simplify the workflow, one approach is to dedicate someone as a repository maintainer who is responsible for pulling all changes from everyone else's repositories.  Everyone else then regularly pulls from this individual to keep their repositories up to date.

<figure style="width: 300px; margin:auto">
<img src="/images/workflow-2.png" alt="Distributed Workflow with Repository Maintainer"><br>
<b>Figure: Distributed Repositories with Dedicated Maintainer</b><br>A simpler approach is for one team member to maintain a central repository from which everyone else pulls.
</figure>

The most common workflow is to host a central repository on a server accessible to everyone on the team.  This arrangement requires a particular configuration of the central repository which allows it to be *pushed* to instead of just pulled from.  We will discuss how this works in the next lessons.

<figure style="width: 300px; margin:auto">
<img src="/images/workflow-3.png" alt="Centralized Workflow"><br>
<b>Figure: Central Repository</b><br>The most common workflow is to have a central repository that everyone can pull from and push to.
</figure>
