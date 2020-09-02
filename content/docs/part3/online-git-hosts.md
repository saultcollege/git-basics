---
title: "Online Git Hosts"
weight: 2200
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Online Git Hosts

## Goals

By the end of this lesson you should be able to

- Use an online host such as GitHub or GitLab to host a central Git repository
- Synchronize a local repository with a remote on an online host

## GitHub and GitLab and Others

One of the most common ways to store a repository is by using a web host like [GitHub](https://github.com), [GitLab](https://about.gitlab.com/stages-devops-lifecycle/source-code-management/), or [others](https://alternativeto.net/software/github/).  These hosts allow you to create accounts on which you can store Git repositories.  You may then sync these repositories with any machine that has Git installed and access to the internet.  Many open source software projects are hosted in this way, allowing any developer to easily contribute.  (For example, you may find the code for [this website on GitHub](https://github.com/saultcollege/git-basics).)  Many of these hosts also offer a plethora of features useful in software development, but at the core there is always a way to host repositories.

{{< hint warning >}}
**NOTE:** Novice users often confuse Git with hosts like GitHub or GitLab.  They are not the same.  The former is the core version control system and the latter two are systems built on top of Git that provide tools and services for collaborating on software projects among teams and individuals.  You can use Git without ever interacting with a Git host (as you have in this tutorial until now).
{{< /hint >}}

## Hands-on Example

In this lesson you will use GitHub to host the repository that you have been working on throughout this tutorial.  However, the process would be very similar for any of the other online Git hosts.

{{< action >}}
1. Go to the [GitHub website](https://github.com) and log in or create a new account if you do not already have one.
1. Once logged in to GitHub you should be able to find a button to create a new repository.  Click this button.
1. You should be taken to a screen where you can enter some basic information about your repository.
1. Give your repository the name `git-basics-tutorial`
1. You may choose to make the repository public (anyone can view it and clone it) or private (only you and GitHub users you select may see it).
1. Do **not** add a README, .gitignore, or license file.  Doing so would intialize a new repository with a new commit history, but you will need to push an existing repository to this repository so you need the commit history to remain uninitialized for now.  (See the Shared Histories lesson.)
1. Now click the `Create Repository` button, after which you will be taken to the main repository page for your new hosted repository.
1. On the repository page you should be able to find a repository URL.  GitHub offers two URLs: an HTTPS URL or an SSH URL.  For now, copy the HTTPS URL as configuring an SSH connection is beyond the scope of this tutorial.
1. Use the URL you just copied as the URL for a new remote in `myrepo` (your URL will be slightly different)
    ```text
    $ git remote add github https://github.com/rmartin-sc/git-basics-tutorial.git
    ```
1. Push your repository to GitHub
    ```text
    $ git push github master
    Enumerating objects: 58, done.
    Counting objects: 100% (58/58), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (53/53), done.
    Writing objects: 100% (58/58), 5.55 KiB | 1.11 MiB/s, done.
    Total 58 (delta 18), reused 0 (delta 0)
    remote: Resolving deltas: 100% (18/18), done.
    To https://github.com/rmartin-sc/git-basics-tutorial.git
     * [new branch]      master -> master
1. If you now refresh your repository page on GitHub you should see the files in your repository there.  
1. Clicking on the `# commits` link near the top right of the list of files in your repository will take you to a page that displays the commit history of your repository, including dates and commit messages.
1. Clicking on an individual commit will take you to a page that displays the changes involved in that commit.

{{< /action >}}

There is much more that you could do in GitHub, but you can read the GitHub documentation to learn about that.  The main thing to know is that what you have in your GitHub repository is a true Git repository that you can push to and pull from.  You could clone this repository onto another computer if you needed to work on it from multiple devices.  If you made the repository public, other people could clone it as well.  It is just another repository with which you can interact using the Git commands you have learned in this tutorial.