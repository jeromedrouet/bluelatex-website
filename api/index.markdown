---
layout: default
title: Restful API
---

# Restful API
{:.no_toc}

* Contents
{:toc}

\BlueLaTeX exposes its features through a Rest Api. This Api serves several purposes, such as managing user related data, papers, snychronization, ...
Client applications wishing to interact with a \BlueLaTeX instance must use this API

You can find below the different pages containing the documentation of the Api.

## API Prefix

By default, the API is accessible under the `api` path prefix.
In the documentation pages, this prefix is denoted as `<api>` which is a paceholder for whatever prefix you configured on your \BlueLaTeX instance (it may be empty).

## Response Type

Unless specified otherwise the Rest Api accepts and returns Json values

## Error Response

In case of an error, a json error object is returned with the appropriate HTTP response code. The format of the error object is as follows:

```json
{
  "name": "unable_to_register",
  "description": "Something went wrong when registering the user glambert. Please retry"
}
```

## Synchronization Protocol

The synchronization protocol is based on [mobwrite](http://code.google.com/p/google-mobwrite) and was adapted to integrate more smoothly in our JSON based API.
You can find the description of the protocol [in this documentation](synchronization-protocol/).

## Complete API Documentation

* [User management](v1.0.0/users-api/)
* [Session management](v1.0.0/session-api/)
* [Paper management](v1.0.0/papers-api/)
* [Paper compilation](v1.0.0/compiler-api/)
* [Paper synchronization](v1.0.0/sync-api/)

