---
layout: default
title: \BlueLaTeX Version 1.0.4 Released
category: release
tags: v1.0.4
---

Hi all,

Two weeks after the last patch release, we are glad to make a new one available today.

This is an important one, as it fixes a bug in the implementation of the synchronization protocol which caused content to be lost or duplicated in some cases with high latency networks or disconnections.

The web client has also been improved to avoid some surprising behaviors.

The exact [changelog](https://github.com/gnieh/bluelatex/blob/v1.0.4/changelog/v1.0.x.markdown#version-104) is:

 - Fix the guarantee delivery part in case of disconnection or high latency network (issue #188)
 - Hold the scroll position when several authors are editing a file concurrently (issue #185)
 - Restore cursor position when changing file (issue #181)
 - Fix script loading order to avoid display problems on slow networks (issue #189)
 - Re-enable use of standard key bindings in web browser (issue #171)
 - Fix PDF rendering on small displays (issue #182)
 - Fix upgrade script to create missing installation directory

Nothing should break, no configuration is to change, to update from a previous version, follow the instruction [from the documentation](/installation/#upgrade).

You can retrieve the new version in the [download section](/download/). .rpm and .deb packages should be available soon, stay tuned for this by following us on [twitter](https://twitter.com/bluelatex_team).

Thanks again to the contributors of this version, for your feedback on the previous version and your contributions on this one.

We would be happy to get feedback so that further versions can bring you anything you want in a real-time collaborative editor!
Do not hesitate to [contact us](/community/) if you have questions, problems or ideas.

The \BlueLaTeX Team.
