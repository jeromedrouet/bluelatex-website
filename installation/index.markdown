---
layout: default
title: Installation
---

Installation and Start
======================

Dependencies
------------

\BlueLaTeX requires several dependencies to run:

 - The server being written in Scala you will need a JVM (version 1.7 or higher for the binary distribution, 1.6 or higher if you build it from source),
 - Users and paper data are saved in a [couchdb](http://couchdb.apache.org) database version 1.2.0 or higher,
 - You will also need to have access to a SMTP server to validate user registrations, so you might need to install one on your server if you do not want to use an external one,
 - Finally if you want to compile \LaTeX documents, you will need a \LaTeX distribution installed on your system. [TeX Live](https://www.tug.org/texlive/) is probably the best choice for Unix systems, and [MiKTeX](http://miktex.org/) for Windows.

Installation from Binary Distribution Package
---------------------------------------------

[Download the last version](/download/) of \BlueLaTeX, and extract the archive.

An installation script is provided in the distribution, simply run it as root:

```shell
$ cd bluelatex-<version>
$ sudo ./install.sh
```

\BlueLaTeX is installed in `/opt/bluelatex-<version>`, and the configuration is located at `/etc/opt/bluelatex`.

Installation From the Source
----------------------------

You can either download the packaged sources of the last release on the [download page](/download/) or [clone the current master](https://github.com/gnieh/bluelatex).

You need [sbt](http://scala-sbt.org) to build and package a distribution.
Then, in the root directory of the repository simply run:

```shell
$ sbt 'project blue-dist' makeDistribution
```

The dependencies will be downloaded, everything will be compiled and the distribution will be packed in `blue-dist/target/bluelatex-<version>`.

If you encounter any problem to compile \BlueLaTeX, please refer to the [developer corner](/developers/).

And Then
--------

You can now [configure](/configuration/) \BlueLaTeX to your needs and then [start it](/running/).
