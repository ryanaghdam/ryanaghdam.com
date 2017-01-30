---
title: Opening All Modified Files in Vim
layout: post
category: software
---

Git's `ls-files` command can be used with Vim's `-p` flag to open all modified
files in Vim.

    $ vim -p `git ls-files -m`

Vim's `-p` flag will open a tab for each following argument.

Git's `ls-files` subcommand will list files that meet specific criteria in Git
repository.  In the example above, the `-m` flag is used to show modified
files.

Untracked files can also be included by specifying the `-o` parameter which
includes "others".  "Others" includes untracked files, so you may want to add
the `--exclude-standard` flag.

    $ vim -p `git ls-files -mo --exclude-standard`

