---
title: Commit Message Style Guide
layout: post
category: software
---

Sometimes when I come across a particularly grotesque line of code I’ll use
[`git-blame`](https://git-scm.com/docs/git-blame) in the hopes that I’ll find a
descriptive commit message.  More often than not, though, it’ll look something
like this:

```
commit 5eaf00ddebac1e1016c4a8b23c4bdeadbea79916
Author: Lazy Developer <slob@company.com>
Date:   Wed Aug 17 15:54:52 2016 -0400

    changes
```

The commit message is useless, but `git-blame` isn’t; I know who needs to be
taken off of the Christmas card list.

Good commit messages provide documentation for each feature and line of code.
Commit messages that describe the desired result of each code change can help
other developers make sure they’re not inadvertently breaking any
functionality[^1].

Using a single well-written commit message per change makes it easy to use
powerful tools like [git-bisect](https://git-scm.com/docs/git-bisect) and even
simple ones like [git-log](https://git-scm.com/docs/git-log).

The first line of a Git commit message is a brief summary of the change.  It
should complete the sentence: "This commit will...".

The subject should:

- Be a 50 character phrase[^2]
- Start with a capital letter
- _not_ end with punctuation
- Concisely describe the change

A blank line separates the subject and body. It is required, otherwise the
message will be incorrectly parsed by `git-log` and GitHub.

The body describes the change in detail.  It should not only discuss
what has changed but also why it has changed.  If it helps, you may use
bullet points or other plain-text formatting to help convey your
message.

The body should:

- Answer _how_ and _why_; not necessarily what.
- Have 72-character lines
- Be written in paragraph form


Optionally, the commit message may end with references to any Trello cards,
GitHub Issues, JIRA tickets -- anything that is relevant to this change.

{% include image.html image="Screen Shot 2016-08-18 at 10.49.11 AM.png" caption="Editing a commit message in vim" %}

## Commit Message Hall of Shame

- "Renaming."
- "changes"
- "Added right func"
- "one more"
- "updates"
- "WIP"[^3]
- "merge"
- "remove test"
- "WIP"[^4]
- "retry"
- "I hope it works."[^5]
- "relaxing"

[^1]: It should cause a unit test to fail, though!
[^2]: 72 is the absolute maximum.
[^3]: Oops.  This one was me.
[^4]: Me, again.
[^5]: Also me.
