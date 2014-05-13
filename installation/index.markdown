---
layout: default
Title: Installation
---

Dependencies
------------

\BlueLaTeX requires several dependencies to run:

 - The server being written in Scala you will need a JVM in version 1.7 or higher,
 - Users and paper data are saved in a [couchdb](http://couchdb.apache.org) database version 1.2.0 or higher,
 - The daemon is started using [commons-daemon](http://commons.apache.org/proper/commons-daemon/). On Unix you will need [jsvc](http://commons.apache.org/proper/commons-daemon/jsvc.html), for Windows [procrun](http://commons.apache.org/proper/commons-daemon/procrun.html),
 - Finally if you want to compile \LaTeX documents, you will need a \LaTeX distribution installed on your system. [TeX Live](https://www.tug.org/texlive/) is probably the best choice for Unix systems, and [MiKTeX](http://miktex.org/) for Windows.

Binary Installation
-------------------

[Download the last version](/download/) of \BlueLaTeX, and extract the archive.
