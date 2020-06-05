---
title: "Ignoring Files"
date: 2020-05-14T15:07:55-04:00
weight: 140
---

# Ignoring Files

Sometimes you want files in your respository directory, but not in the repository itself, and you don't want those files to show up in status messages.  You can use a `.gitignore` file to tell Git to ignore specific files.

A `.gitignore` file is a plain text file that contains one path<sup>[1](#fn1)</sup> on each line.  The paths may include globs.  Relative paths are relative to the `.gitignore` file.  The `.gitignore` file should be placed in the root directory of the repository.

Common items to include in a `.gitignore` file are backup files, compiled files (eg. `*.exe`, `*.class`, etc.), IDE configuration files, etc—anything that you do not want to track the history of in your repository.

The `.gitignore` file itself is usually tracked in the repository.

Anything after a `#` symbol in a `.gitignore` file until the end of the line is considered a comment and is ignored by Git.

Here is an example `.gitignore` file:

```sh
ignore.me  # Ignore files named ignore.me
foo/*      # Ignore all files inside the foo directory
*.bak      # Ignore all files ending with .bak
```

<div class="footnote"><a name="fn1">1</a> Technically, paths are only a subset of the possible values for each line of a .gitignore file, but you will probably only need to use paths (possibly with globs) as a beginner.  For more information, see the <a href="https://git-scm.com/docs/gitignore">Git documentation</a>.</div>