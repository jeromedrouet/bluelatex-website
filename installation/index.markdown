---
layout: default
title: Installation
---

Installation and Start
======================

Dependencies
------------

\BlueLaTeX requires several dependencies to run:

 - The server being written in Scala you will need a JVM in version 1.7 or higher,
 - Users and paper data are saved in a [couchdb](http://couchdb.apache.org) database version 1.2.0 or higher,
 - You will also need to have access to an smtp server to validate user registrations, so you might need to install one on your server if you do not want ot use an external one,
 - Finally if you want to compile \LaTeX documents, you will need a \LaTeX distribution installed on your system. [TeX Live](https://www.tug.org/texlive/) is probably the best choice for Unix systems, and [MiKTeX](http://miktex.org/) for Windows.

Installation from Distribution Package
--------------------------------------

[Download the last version](/download/) of \BlueLaTeX, and extract the archive.

An installation script is provided in the distribution, simply run it as root:

```shell
$ cd bluelatex-<version>
$ sudo ./install.sh
```

\BlueLaTeX is installed in `/opt/bluelatex-<version>`, and the configuration is located at `/etc/opt/bluelatex`.

You can now [configure](/configuration/) \BlueLaTeX to your needs and then [start it](/running/).
