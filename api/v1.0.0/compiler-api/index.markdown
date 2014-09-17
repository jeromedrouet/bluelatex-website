---
layout: default
title: Compiler API
---

# Compiler API
{:.no_toc}

* Content
{:toc}

This page describes how the paper compilation process is handled inside \BlueLaTeX.

## Background Compilation

Paper compilation in \BlueLaTeX is performed as a background task. No user action is needed anymore.

This task is started when the first author joins the compiler resource of a paper. It is stopped when the last author leaves the compiler resource.

By joining the compiler resource of a paper, the author subscribes to an update stream that sends results of the compilation (either the compiled paper, or the error log).

## Compilation Settings

Each paper may have specific compilation settings. These settings allow people to inform \BlueLaTeX how the compilation is to be performed:

* **compiler** tells \BlueLaTeX which compiler to use to compile the paper (latex, pdflatex, xelatex, lualatex, ...),
* **interval** tells \BlueLaTeX how long (in seconds) it must wait between two recompilations,
* **timeout** tells \BlueLaTeX after what timeout (in seconds) it must stops the current compilation pass, and (possibly) retry.
* ***synctex*** tells \BlueLaTeX to generate SyncTeX data when compiling the paper.
