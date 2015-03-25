---
layout: default
title: \BlueLaTeX Version 1.0.5 Released
category: release
tags: v1.0.5
---

Hi all,

After a few months without activity, \BlueLaTeX is coming back to life.

This new minor release fixes a really annoying bug in the synchronization server implementation. Even if the fix is a [one character diff](https://github.com/gnieh/bluelatex/commit/faa2c69abf3c9d37c2efc65c9e6a56307c0e4a97#diff-fb76f6492408fe4b6582c4cb15f510d9) it changes a lot the behavior of the protocol (and it makes it actually correct).

A huge thank you to Thomas who found and fixed it!

This release is 100% Thomas' work, thank you again.

The exact [changelog](https://github.com/gnieh/bluelatex/blob/v1.0.5/changelog/v1.0.x.markdown#version-105) is:

 - Fix synchronization bug that may lead to data loss (issue #188)
 - Fix cursor appearing in multiple files (issue #196)
 - Fix persistent cursor after an author left the paper (issue #195)
 - Cleanup error and wraning upon compilation (issue #201)
 - Improvements in the UI

Nothing should break, no configuration is to change, to update from a previous version, follow the instruction [from the documentation](/installation/#upgrade).

You can retrieve the new version in the [download section](/download/). .rpm and .deb packages should be available soon, stay tuned for this by following us on [twitter](https://twitter.com/bluelatex_team).

Thanks again to the contributors of this version, for your feedback on the previous version and your contributions on this one.

We would be happy to get feedback so that further versions can bring you anything you want in a real-time collaborative editor!
Do not hesitate to [contact us](/community/) if you have questions, problems or ideas.

The \BlueLaTeX Team.
