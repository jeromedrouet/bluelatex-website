---
layout: default
title: Running \BlueLaTeX
---

Running with commons-daemon
---------------------------

If you want to use the launcher to start \BlueLaTeX as a daemon, you need to have [commons-daemon](http://commons.apache.org/proper/commons-daemon/) installed.
On Unix you will need [jsvc](http://commons.apache.org/proper/commons-daemon/jsvc.html), for Windows [procrun](http://commons.apache.org/proper/commons-daemon/procrun.html).

The launcher is packaged in the `bin` directory as `blue-launcher.jar`.

Let's say you installed \BlueLaTeX using the installation script, you can run the script provided in the distribution by running:
```shell
$ bluelatex-dir/init/jsvc/blue-start.sh
```

The options to pass to jsvc depends on where you installed your \BlueLaTeX instance and of your jsvc version.
Please refer to the [jsvc documentation](http://commons.apache.org/proper/commons-daemon/jsvc.html) for more details.

Once the server is started, you may access the web client at (by default): [http://localhost:8080/](http://localhost:8080/)

For Windows users, any help to document how it works with procrun is welcome. Do not hesitate to open a [pull request](https://github.com/gnieh/bluelatex-website/compare/) to propose the documentation.

Stopping the daemon with jsvc is quite similar to starting it:

```shell
$ bluelatex-dir/init/jsvc/blue-stop.sh
```

Starting \BlueLaTeX with systemd
--------------------------------

A [systemd](http://freedesktop.org/wiki/Software/systemd/) unit is also provided in the distribution.
To use it, if you installed \BlueLaTeX with the provided [installation script](/installation/), simply copy the file `init/systemd/bluelatex.service` into a standard `systemd` location such as `/etc/systemd/system/`.

Then you can start \BlueLaTeX using the standard [systemctl](http://www.freedesktop.org/software/systemd/man/systemctl.html) command.

```shell
$ sudo systemctl start bluelatex
$ sudo systemctl status bluelatex
$ sudo systemctl stop bluelatex
```
