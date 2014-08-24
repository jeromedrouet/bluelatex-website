---
layout: default
title: \BlueLaTeX Version 1.0.0-RC1 Released
category: release
tags: RC1 v1.0.0
---

Hi all,

We are glad to announce the release of \BlueLaTeX in its version 1.0.0-RC1.

This is the first version intended to become a stable version.
If no major problems are found on this version, it will become the official
stable release 1.0.0.

To test it, simply [download](/download/) a binary package, [install](/installation/) it, [configure](/configuration/) it and [run](/running/) it.

The main improvements since last milestone are:

 - Adding more system compilers, so that following compilers are available by
   default (#94):
   - latex,
   - pdflatex,
   - xelatex,
   - lualatex.
 - Improve configuration management, making configuration customizations easier
   to write (#55).
 - Making compilation of a paper explicit (#112). No background compilation is
   started, but processes are triggered by authors explicitly.
   Background processes can be enabled in the configuration if this is really
   wanted, but the default behavior is the more intuitive explicit one.
 - The web UI was greatly improved by (#83):
   - Adding tooltips on all buttons.
   - Removing useless entries from menus.
   - Allowing people to delete their account.
   - Upgrading versions of AngularJS, Ace.
   - Improving completion in the editor.
   - Improving SyncTeX support.
   - A lot more small-yet-awesome improvements.
 - Several bugs were fixed, among which these were critical:
   - Content could get lost when the window was abruptly closed (#108).
   - Data leak was possible by including content from other papers (#119).
   - Synchronization protocol badly encoded data sent as json objects (#107).
 - Several [other bugs were fixed](https://github.com/gnieh/bluelatex/issues?q=milestone%3A%22v1.0.0+Release+Candidate+1%22+is%3Aclosed).
 - This version is packaged as something that can be really installed,
   packaging and building of distribution was made much much easier, one more
   step toward a stable product (#49) that can be started as a real daemon (#100).
