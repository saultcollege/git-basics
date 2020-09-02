---
title: "Adding Remotes"
weight: 2170
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: true
---

# Adding Remotes

## Goals

By the end of this lesson you should be able to use the `git remote` command to

- List the configured remotes for a repository
- Inspect information about a specific remote
- Add new remotes to a repository

## The Remote Command

The `git remote` command can be used to inspect the properties of a repository's remotes.

```sh
$ git remote              # List all configured remotes
$ git remote show <name>  # Display information about a specific remote
```

{{< action >}}
1. Get into `clonerepo`
    ```text
    $ cd ../clonerepo
    ```
2. List the remotes
    ```text
    $ git remote
    origin
    ```
3. Show the details of the remote `origin`
    ```text
    $ git remote show origin
    * remote origin
    Fetch URL: /Users/rod/tmp/myrepo  # Your path will be different
    Push  URL: /Users/rod/tmp/myrepo  # Your path will be different
    HEAD branch: master
    Remote branch:
        master tracked
    Local branch configured for 'git pull':
        master merges with remote master
    Local ref configured for 'git push':
        master pushes to master (local out of date)
    ```
{{< /action >}}

As you can see, the plain `git remote` command displays a list of the names of all configured remotes.  Currently you have only one named `origin` that was configured automatically when you cloned `clonerepo` from `myrepo`.

We will ignore most of the output of the `git remote show` command except to point out that the Fetch and Pull URLs are the paths to the `myrepo` repository from which you cloned `clonerepo`.  If you had cloned from a host like GitHub, this path would be a GitHub URL instead.

Now try the same in `myrepo`:

{{< action >}}
1. Get into `myrepo`
    ```text
    $ cd ../myrepo
    ```
2. List the remotes
    ```text
    $ git remote
    ```
{{< /action >}}

There are no remotes in `myrepo`!

## Adding Remotes

Suppose you wanted to be able to pull changes from `clonerepo` into `myrepo`.  This should be possible because the two repositories have a shared history.  But at the moment, `myrepo` does not have any remotes.  This can be changed, however, using the `git remote add` command.

```sh
# Format for the git remote add command
$ git remote add <remote_name> <remote_url>
```

You can choose the name of the remote by providing an value for `<remote_name>`.  The `<remote_url>` can be a path or a URL.

{{< action >}}
1. Add a new remote named `theclone` to `myrepo`<br>
    **NOTE:** You will need to use different path appropriate to your system
    ```text
    $ git remote add theclone /Users/rod/tmp/clonerepo
    ```
2. List the remotes again
    ```text
    $ git remote
    theclone
    ```
3. Show the details of the remote `theclone`
    ```text
    $ git remote show theclone
    * remote theclone
    Fetch URL: /Users/rod/tmp/clonerepo
    Push  URL: /Users/rod/tmp/clonerepo
    HEAD branch: master
    Remote branch:
        master new (next fetch will store in remotes/theclone)
    Local ref configured for 'git push':
        master pushes to master (up to date)
    ```
{{< /action >}}

The `myrepo` repository is now configured with a remote pointing to `clonerepo`.  This means that any changes committed to `clonerepo` can now be merged into `myrepo` by running, for example, `git pull theclone master` from the `myrepo` working tree.

Now might be a good time to do some experimentation on your own to really make sure you understand the concepts you have learned so far:

{{< action >}}
1. Initialize a brand new repository
1. Create some new files in the repository and commit them
1. Clone the repository
1. Add the clone as a remote to the original repository
1. Commit changes in the clone and pull them into the original
1. Commit non-conflicting changes in both repositories, then try pulling each of the changes into the other repository
1. Commit conflicting changes in both repositories, then pull the changes into the clone and resolve the conflict

{{< /action >}}

