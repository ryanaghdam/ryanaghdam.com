---
title: Basic spell check in Vim
layout: post
category: software
---

Vim 7 features built in spellchecking.  Enable and disable by setting `spell`
or `nospell`.

    :set spell
    :set nospell

Default key bindings:

- navigate to next misspelled word: `]s`
- navigate to previous misspelled word: `[s`
- open spelling suggestions for word under cursor: `z=`
