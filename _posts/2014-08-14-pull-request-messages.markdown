---
title: Effective Pull Request Messages
layout: post
category: software
excerpt: A template for writing informative pull requests to improve the effectiveness and speed of code reviews.
---

My team has a policy that states each pull request should be reviewed by at
least two developers and a QA engineer.  In the past, pull requests had been
submitted completely devoid of a description field; the title was automatically
generated from the branch name.  After vetting, a simple comment was left by
reviewers stating that it was "good to merge" ("GTM").

Not only was it sometimes unclear _why_ each pull request was opened, but it was
also difficult to tell which pull requests had been reviewed and which ones
needed another set of eyes.

In an effort to resolve some of these issues, I made a template for opening pull
requests.

The template has the following sections, most of which are used only when
applicable:

*Description* -- a paragraph or two that describes the changes introduced by the
pull request.  The prose should be be written for a product manager; it should
resemble the language found in a user story.  If significant code changes, such
as refactoring, are made then additional paragraph(s) of text should be
targeted for engineers.

*Acceptance Criteria* -- a list explicitly enumerating each user-facing change.
These should be specific and should *not* assume the reader infers any
side-effects or behavior.  The accuracy of this section reduces uncertainty
during testing.

*Dependencies* -- a list of pull requests or other items that are depended upon.

*Test Scenarios* -- a list of step-by-step scenarios to test. This section
somewhat duplicates the acceptance criteria, but can be helpful when working on
edge cases.

*Screenshots* -- screenshots can be helpful to product owners when reviewing
stories.  You can drag-and-drop images into your browser window when editing a
pull request description.

*Reviewers* -- use the [task list][GFMTaskList] feature to create a bulleted
list of those who need to review your pull request. The status of the check
boxes is displayed wherever the pull request is referenced.

After switching to this template, we found that it was much easier to check the
status of *all* open pull requests on the Pull Requests page.  It also became
easier to hound and shame those who needed to review open pull requests.

[hub]: https://github.com/github/hub
[GFMTaskList]: https://github.com/blog/1375%0A-task-lists-in-gfm-issues-pulls-comments
