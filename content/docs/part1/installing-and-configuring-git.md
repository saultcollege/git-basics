---
title: "Installing and Configuring Git"
date: 2020-05-12T13:51:01-04:00
weight: 20
---

# Installing and Configuring Git

## Goals

By the end of this lesson you should be able to...
- Install Git
- Adjust and view basic configurations in Git
- Find documentation on any aspect of Git you don't already know

## Installation

Now that you know the basic concepts of [Version Control]({{< ref "intro-to-version-control.md" >}}) you can get started with Git!

{{< action >}}
1. Download the Git installer appropriate for your device from the [Git website](https://git-scm.com/downloads)
1. Run the installer using the default configurations when prompted.
1. Open your favourite command line shell<sup>[1](#fn1)</sup> and enter the command `git`.  (If you installed Git on Windows, use the Git Bash shell which should now be on your system.)  
{{</ action >}}

If you have installed Git correctly on your system you should see a message that explains the basic usage of the `git` command.

<div class="footnote"><a name="fn1">1</a>: If you are unsure what a command line shell is or how to use one, <a href="https://saultcollege.github.io/shell-basics/" target="_blank">this tutorial</a> should help!</div>

## Configuration

There are a few configuration items you will want to set before you begin.  Git configuration can be done using the `git config` command.  The general format for this command is as follows:

```sh
# Config command format
git config [--global] <name> <value>
```

{{< hint info >}}
**NOTE:** See [this reminder](https://saultcollege.github.io/shell-basics/#a-note-on-documentation)  of the use of square and angle brackets in command line documentation.
{{< /hint >}}

There are many options that can be configured, and each one has a specific name.  For example, `user.name` and `user.email` which you will use in the activity below.  Each option can be assigned a value by replacing `<value>` with the value you choose.

The `--global` option will apply the configuration to *all* Git repositories on your system, which is often what you want.  You can, however, have the configuration apply to only the Git repository in the current working directory by not including the `--global` option.

### User Info

{{< action >}}
Set your name and email address by issuing the following commands, (replacing the name and email address with yours):
```text
$ git config --global user.name "Your Name"
$ git config --global user.email "your_email@address.com"
```
{{</ action >}}

{{< hint info >}}
**NOTE:** In code blocks like the one above, you should not type the initial `$` as it is meant to indicate the shell prompt.  If there are lines that do not begin with `$`, they are the expected output of the command. 
{{< /hint >}}

Git uses the `user.name` and `user.email` values to determine who made which changes in any repository.

### Editor

There are certain scenarios in which Git requires you to input text using a text editor.  The default editor is `vi`, but unless you are already familiar with the use of `vi` you will probably want to change it to something easier to use such as `nano`:

{{< action >}}
Set the default text editor used by Git with this command: 

```sh
$ git config --global core.editor nano
```
{{</ action >}}

### Line Endings

Different operating systems represent the end of a line of text in different ways, which can cause problems in repositories that are being contributed to by people using different operating systems.  There are a couple options that can be used to prevent these issues.

{{< action >}}
Prevent issues with line endings using these two configuration options.

If you are on a Windows device:
```sh
$ git config --global core.autocrlf true
$ git config --global core.safecrlf true
```

If you are on a Mac/Linux/Unix device:
```sh
$ git config --global core.autocrlf input
$ git config --global core.safecrlf true
```
{{< /action >}}

{{< hint info >}}
**NOTE:** The `crlf` in the option names above refer to the 'carriage return' (`cr`) and 'line feed' (`lf`) characters used to represent the end of a line of text.  You may also encounter these characters in your programs in the form of `\r` and `\n` respectively.
{{< /hint >}}

### Viewing Configuration

You can view the current value for any configuration option using a command like `git config <name>`, as in

```sh
$ git config user.name
Rodney Martin
```

You can also view all explicitly configured options using the `--list` option:

```sh
$ git config --list
```

### Version

You can see which version of Git is on your system using the `--version` option:

```bash
$ git --version
git version 2.24.0
```

## Getting Help

Git comes with extensive built-in documentation that can be accessed via the `git help` command.  

You may also get help for specific sub-commands using

```sh
$ git help <subcommand>
```

For example, in the previous section you were only introduced to a few of the many configuration options in Git.  If you ever wanted to know more, a good place to start would be the command

```sh
$ git help config
```

For a more detailed explanation of any of the commands and concepts introduced in this tutorial, the official [Pro Git Book](https://git-scm.com/book/en/v2) is also an excellent resource.