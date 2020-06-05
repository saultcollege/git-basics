---
title: "Tags"
date: 2020-06-05T12:01:09-04:00
weight: 88
---

# Tags

## Goals

By the end of this lesson you should be able to

- Label specific commits using the `git tag` command
- Remove existing tags

## Overview

Using the `git tag` command you can give a label to any commit.  This can be helpful for marking certain important commits.

For example, it is common practice when writing software to tag each commit that corresponds to a major version release.  You might tag the commit that is your initial software release with the label `v1.0`.  Later, you might tag another commit as `v1.1`, and so on.

In most Git commands, anywhere that you can refer to a commit ID you can enter a tag name instead.  Git automatically translates that tag name to the correct commit ID.

<figure style="width: 500px">
<img src="/images/tags.png" alt="Tags">
<b>Figure: Tags</b>  <br>Tags are just labels for specific commits.  In this figure, commit <code>9d52</code> could also be referred to as <code>v1.0</code> in many Git commands.  Note that here, tag <code>v1.1</code> points to the same commit as <code>HEAD</code> (and <code>master</code>).
</figure>

{{< hint info >}}
**NOTE:** There are quite a few rules for valid tag names.  These rules can be found in the [Git documentation](https://git-scm.com/docs/git-check-ref-format#_description), but in general sticking to standard version numbers like the ones you have encountered here, or basic alpha-numeric names is always safe.
{{< /hint >}}

## Adding Tags

You can tag a commit by providing a tag name and an optional commit ID as arguments to the `git tag` command.  If you do not specify a commit ID the default is to tag HEAD (usually the most recent commit).

```sh
# Format for adding a tag
$ git tag <tagname> [<commit_id>]
```

**Examples**

```sh
# Tag the most recent commit with the label 'foo'
git tag foo

# Tag commit 3d11 with the label 'foo'
git tag foo 3d11
```

{{< action >}}

Tag your most recent commit with a label of your choice:

```sh
$ git tag mytag
```

Choose one of your previous commits and give it a tag of your choice (your commit ID will be different than the one shown below):

```sh
$ git tag anothertag 7d7596a
```

{{< /action >}}

## Listing Tags

Running `git tag` by itself will list all existing tags.

{{< action >}}
List your existing tags:

```sh
$ git tag
mytag         # You should see here the tag names you chose
anothertag
```
{{< /action >}}

Tags will also be noted in `git log`:

{{< action >}}

Run a `git log` and note that your tags are marked beside the corresponding commit:

```text
$ git log --oneline
8916e31 (HEAD -> master, tag: mytag) Made some content changes
9d52001 Added more files and text
7d7596a (tag: anothertag) Added another change tracking description
312fabf Added a description about Git change tracking
3f21652 Added brief description
17f9667 Initial commit
```


{{< /action >}}

## Removing Tags

Tags can be removed using the `-d` (delete) option, as in

```sh
# Format for deleting tags
$ git tag -d <tagname>
```

{{< action >}}
Delete one of the tags you just created:

```text
$ git tag -d mytag
Deleted tag 'mytag' (was b2763fe)
```
{{< /action >}}

Now that you have a better understanding of the underlying structure of your repository, let's go into a bit more detail about what is happening when you stage changes...