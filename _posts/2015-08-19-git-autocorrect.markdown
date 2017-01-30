---
title: Git's Autocorrect Feature
category: software
layout: post
---

The autocorrect feature in Git will automatically fix mistyped Git commands.
If, for example, you type: `git comit`, Git will continue assuming that you
meant to use the `commit` command.

To enable this feature, set `help.autocorrect` to `1`.

    $ git config --global help.autocorrect 1
