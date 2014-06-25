---
layout: default
Title: Configuration
---

Configuration File Layout
-------------------------

The \BlueLaTeX server is organized in a bunch of [OSGi](http://www.osgi.org/Main/HomePage) bundles making it really modular.
The configuration of each bundle is made in its own directory, with respect to this modular architecture.

The directory layout for configuration files is organized under one directory for each bundle.
The directory in which the configuration of a bundle lies is simply the bundle identifier.
Standard bundles are:
 - `org.gnieh.blue.common` the common utility bundle (http server, database configuration, ...),
 - `org.gnieh.blue.core` the core \BlueLaTeX features (user management, paper management, ...),
 - `org.gnieh.blue.sync` the standard \BlueLaTeX synchronization server,
 - `org.gnieh.blue.compile` the \LaTeX compilation bundle,
 - `org.gnieh.blue.web` the standard web client.

Below is detailed the configuration of each standard.
