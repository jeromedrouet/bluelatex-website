---
layout: default
title: Running \BlueLaTeX
---

There are two possibilities for running \BlueLaTeX, commons-daemon or systemd. We explain here both.

Running with commons-daemon
---------------------------

If you want to use the launcher to start \BlueLaTeX as a daemon, you need to have [commons-daemon](http://commons.apache.org/proper/commons-daemon/) installed.

On Unix you will need [jsvc](http://commons.apache.org/proper/commons-daemon/jsvc.html).

```shell
$ apt-get install jsvc
```

For Windows [procrun](http://commons.apache.org/proper/commons-daemon/procrun.html).

Let's say you installed \BlueLaTeX using the installation script, you can run the script provided in the distribution by running:

```shell
$ bluelatex-dir/init/jsvc/blue-start.sh
```

The options to pass to jsvc depend on where you installed your \BlueLaTeX instance and of your jsvc version.
Please refer to the [jsvc documentation](http://commons.apache.org/proper/commons-daemon/jsvc.html) for more details.

Once the server is started, you may access the web client at (by default): [http://localhost:8080/](http://localhost:8080/)

For Windows users, any help to document how it works with procrun is welcome. Do not hesitate to open a [pull request](https://github.com/gnieh/bluelatex-website/compare/) to propose the documentation.

Stopping the daemon with jsvc is quite similar to starting it:

```shell
$ bluelatex-dir/init/jsvc/blue-stop.sh
```
Troubleshooting: if `/usr/lib/jvm/default-java` does not exist, you will get a "Cannot locate Java Home"

Starting \BlueLaTeX with systemd
--------------------------------

A [systemd](http://freedesktop.org/wiki/Software/systemd/) unit is also provided in the distribution.
To use it, simply copy it into a standard `systemd` location such as `/etc/systemd/system/`.

Then you can start \BlueLaTeX using the standard [systemctl](http://www.freedesktop.org/software/systemd/man/systemctl.html) command.

```shell
$ cp init/systemd/bluelatex.service /etc/systemd/system/
$ sudo systemctl start bluelatex
$ sudo systemctl status bluelatex
$ sudo systemctl stop bluelatex
```

Troubleshooting: failing to copy the `.service` file yields a `Failed to issue method call: Unit bluelatex.service failed to load: No such file or directory.`
