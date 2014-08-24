---
layout: default
title: Welcome!
---
\BlueLaTeX aims to provide a tool chain to easily write documents collaboratively.

The first intended audience of \BlueLaTeX is the academic world (for now!), by integrating concepts and lifecycles particularly well-suited for these kind of documents, but it can be used for any other kind of document.

\BlueLaTeX is still in beta version and not intended for production yet. Any [feedback](community/) is welcome to help it making a great application!

News
====

{% for post in site.posts limit:5 %}
<li class="post">
  <a href="{{ post.url }}">{{ post.title }}</a> <span class="light">(published on {{ post.date }})</span>
</li>
{% endfor %}

Try it Out!
===========

You can create a test account and try it out at <http://demo.bluelatex.org>.

**Note**: This reflect the current state of \BlueLaTeX and is not production-ready. Accounts may be deleted at any time, and papers may be deleted as well.

Contents
========

 - [Download \BlueLaTeX](/download/)
 - [Install \BlueLaTeX](/installation/)
 - [Configure \BlueLaTeX](/configuration/)
 - [Run \BlueLaTeX](/running/)
 - [Blog](/blog/)
 - [Roadmap](/roadmap/)
 - [Developer Corner](/developers/)
 - [Community & Contributions](/community/)
