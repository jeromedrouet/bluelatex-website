---
layout: default
Title: Installation
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

Binary Installation
-------------------

[Download the last version](/download/) of \BlueLaTeX, and extract the archive.

To start the \BlueLaTeX server, simply run the `blue-server-start` script in the `bin` directory.

Starting \BlueLaTeX as a daemon
-------------------------------

If you want to use the launcher to start \BlueLaTeX as a daemon, you need to have [commons-daemon](http://commons.apache.org/proper/commons-daemon/) installed.
On Unix you will need [jsvc](http://commons.apache.org/proper/commons-daemon/jsvc.html), for Windows [procrun](http://commons.apache.org/proper/commons-daemon/procrun.html).

The launcher is packaged in the `bin` directory as `blue-launcher.jar`.
Let's say you installed \BlueLaTeX and put the [configuration](/configuration/) in `/opt/bluelatex`, to start it you would simply type:

```shell
/usr/bin/jsvc \
  -wait 10 \
  -java-home /usr/lib/jvm/default-java \
  -cwd /opt/bluelatex
  -cp bin/famework.jar:bin/launcher.jar:bin/commons-daemon.jar \
  -user bluelatex \
  -pidfile /var/run/bluelated.pid \
  -outfile /tmp/bluelatex.out \
  -errfile /tmp/bluelatex.err \
  org.gnieh.blue.launcher.Main
```

The options to pass to jsvc depends on where you installed your \BlueLaTeX instance and of your jsvc version.
Please refer to the [jsvc documentation](http://commons.apache.org/proper/commons-daemon/jsvc.html) for more details.

For Windows users, any help to document how it works with procrun is welcome. Do not hesitate to open a [pull request](https://github.com/gnieh/bluelatex-website/compare/) to propose the documentation.

Stopping the daemon with jsvc is quite similar to starting it:

```shell
/usr/bin/jsvc \
  -wait 10 \
  -java-home /usr/lib/jvm/default-java \
  -cwd /opt/bluelatex
  -cp bin/famework.jar:bin/launcher.jar:bin/commons-daemon.jar \
  -user bluelatex \
  -pidfile /var/run/bluelated.pid \
  -stop \
  org.gnieh.blue.launcher.Main
```

Starting \BlueLaTeX with systemd
--------------------------------

**TODO**
