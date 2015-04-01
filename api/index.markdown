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

## Sessions

**For now, only cookie sessions are supported.**

A client wishing to access the API must be authenticated for most of the operations (see the documentation for more details on what operation needs what permission).
An example session using curl looks like this:

```
USERNAME='test'
PASSWORD='my secret'

API_URL='http://localhost:8080/api'

# log into \Blue and save the cookie
curl -c /tmp/bluelatex.cookie -d "username=$USERNAME&password=$PASSWORD" $API_URL/session

# then query the list of papers for my logged in user
curl --cookie /tmp/bluelatex.cookie $API_URL/users/$USERNAME/papers

# each time you issue a request you must send the cookie, which is donne by using the --cookie option

# and logout
curl -X DELETE --cookie /tmp/bluelatex.cookie $API_URL/session
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

## Development API Documentation

**Warning**: This is a not yet stable API, things may break, change or disappear. It is mainly intended to have an overview of the future API.

* [User management](v1.1.x/users-api/)
* [Session management](v1.1.x/session-api/)
* [Paper management](v1.1.x/papers-api/)
* [Paper compilation](v1.1.x/compiler-api/)
* [Paper synchronization](v1.1.x/sync-api/)
* [Notifications](v1.1.x/notifications-api/)
