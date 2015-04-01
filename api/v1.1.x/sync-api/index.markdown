---
layout: default
title: Synchronization API
---

# Synchronization API
{:.no_toc}

* Content
{:toc}

## Api Summary

Method | Path                             | Description
------ | -------------------------------- | -----------
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/sync     | Send a synchronization session
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/q        | Send a synchronization session (legacy mobwrite version)

## Synchronization session

**Method:** POST

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/sync_

**Body:** A valid [synchronization session](../../synchronization-protocol/).

**Response:**

Code | Value           | Meaning
---- | --------------- | -------
200  | _sync session_  | Synchronization session (see the [protocol description](../../synchronization-protocol/))
500  | _sync object_   | Something wrong happened on the server side

## Synchronization session (legacy mobwrite protocol)

**Method:** POST

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/q_

**Body:** A [mobwrite synchronization session](http://code.google.com/p/google-mobwrite/wiki/Protocol).

**Response:**

Code | Value           | Meaning
---- | --------------- | -------
200  | _mobwrite_      | Mobwrite session (see the [Mobwrite protocol description](http://code.google.com/p/google-mobwrite/wiki/Protocol))
500  | _sync object_  | Something wrong happened on the server side
