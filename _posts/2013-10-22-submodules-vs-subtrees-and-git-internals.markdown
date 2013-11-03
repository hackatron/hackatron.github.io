---
layout: post
title: Submodules VS Subtrees and Git internals
description: We started asking ourselves which is the best approach between submodules and subtrees but we soon realized we can't compare them without knowing how git works internally.
---

Today we read how git internals work trying to better understand git subtrees. We found a new world! We suggest every git user to take a look at [Git Internals - Git Objects](http://git-scm.com/book/en/Git-Internals-Git-Objects), it explains in detail what happens when you run `git add` and `git commit`.

While [Nicola](http://twitter.com/breezeight) was leading the presentation this is a clumsy attempt at taking notes by [Giovanni](http://twitter.com/johnnyaboh).

![Git Submodules](/images/git_submodules_vs_git_subtrees_01.png)

![Git Subtrees](/images/git_submodules_vs_git_subtrees_02.png)

![Git Objects](/images/git_submodules_vs_git_subtrees_03.png)