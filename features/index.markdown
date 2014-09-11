---
layout: default
title: Features and Advantages
---

Features and Advantages
=======================

* Contents
{:toc}

Features
--------

\BlueLaTeX provides a full-featured server that allows you to create, manage and collaboratively edit documents written in \LaTeX.
A web client is also provided to use the features provided by the server directly in your browser.
A Restful API exposes all possible operations that can be performed on the server side, which makes it possible to use any editor that can communicate with this API.

The current \BlueLaTeX server provides following services:

 - user management
 - document management with role management (author, reviewer)
 - real-time document synchronization between clients
 - document compilation on the server
 - download the source archive of your document with all resources you need to compile it locally

The current \BlueLaTeX web client provides following services:

 - user and document management through a web application
 - a collaborative editor with:
   - syntax highlighting
   - auto-completion of common \LaTeX control sequences
   - SyncTeX synchronization between editor and compiled document

Advantages
----------

You can download and install \BlueLaTeX locally.
This way, you keep your data (users, documents, ...) on your infrastructure, no connection to any external service is required.

It is also designed in a modular way which allows you to have a server exposing the only services you need.
For example the module responsible for \LaTeX paper compilation can be omitted if you do not use the web client but a native client with \LaTeX compilers installed locally.

This makes it also possible to extend the server with new features that better fit into your workflow.
