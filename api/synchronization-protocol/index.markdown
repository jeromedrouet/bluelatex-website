---
layout: default
title: Synchronization Protocol
---

# Synchronization Protocol
{:.no_toc}

* Contents
{:toc}

This protocol is derived from the original [mobwrite protocol](http://code.google.com/p/google-mobwrite/wiki/Protocol) by [Neil Fraser](https://neil.fraser.name/).

## Messages

The protocol uses json messages to communicate between peers. This section describes these messages.

### Synchronization Session

A synchronization session is a message that allows people to work on files for a given paper identifier.
It is composed of the name of the peer sending the message, the paper identifier on which we are working and a list of synchronization commands to apply to files in this paper

For example:

```json
{
  "peerId": "toto",
  "paperId": "v987fed987da70987f",
  "commands": [<command>]
}
```

### Commands

The following commands are available:

* Synchronisation Command

```json
  {
    "filename": "file1.tex",
    "revision": 432767,
    "action": <action>
  }
```
The synchronization commands work on a specific file of the paper at a specific revision. Thus they all are associated to a `filename` and a `revision`.
The possible values for `action` are described below.

* Broadcast Message

```json
{
  "from": "peer1",
  "json": <json value>,
  "filename": "file1"
}
```
It is used to send some use message to all connected peers.

* The `filename` field is optional and may be omitted.
* The `from` field may be used for compatibility with original Mobwrite protocol, where it is defined as follows: "The client identifiers should not be the user's ID, but rather a hash of this ID.".

Note: In the original mobwrite protocol, a client can have at most one broadcast message. In \BlueLaTeX, there is no such limitation.

Note: If there is any broadcast message in the pending queue of a peer, there
are always transmitted on the first synchronization message received.

### Synchronization Action

The following actions are available:

* send delta to the peer

```json
{
  "name": "delta",
  "revision": 4324523,
  "data": [ "=100", "-2", "+test", "=34" ],
  "overwrite": false
}
```

* send raw text to the peer

```json
{
  "name": "raw",
  "revision": 4324523,
  "data": "Complete raw text",
  "overwrite": false
}
```

* send paper deletion request to the peer

```json
{
  "name": "nullify"
}
```

## Compatibility With Legacy Mobwrite Protocol

This section will deal with compatibility issues between the synchronization protocol used in \BlueLaTeX and the [initial mobwrite version](http://code.google.com/p/google-mobwrite/wiki/Protocol).

### \BlueLaTeX -> mobwrite

```json
{
  "peerId": "toto",
  "paperId": "v987fed987da70987f",
  "commands": [
  {
    "filename": "file1.tex",
    "revision": 432767,
    "action": {
      "name": "delta",
      "revision": 4324523,
      "data": [ "=100", "-2", "+test", "=34" ],
      "overwrite": false
    }
  },
  {
    "filename": "file2.tex",
    "revision": 87432,
    "action": {
      "name": "raw",
      "revision": 4324523,
      "data": "Complete raw text",
      "overwrite": false
    }
  }]
}
```

gets converted to

```
U:toto
F:432767:v987fed987da70987f/file1.tex
d:4324523:=100-2+test=34
<blank>

U:toto
F:87432:v987fed987da70987f/file2.tex
r:Complete raw text
<blank>
```
and may be optimized to:

```
U:toto
F:432767:v987fed987da70987f/file1.tex
d:4324523:=100-2+test=34
F:87432:v987fed987da70987f/file2.tex
r:Complete raw text
<blank>
```

### mobwrite -> \BlueLaTeX

```
u:fraser
F:34:v987fed987da70987f/file1.tex
d:41:=200 -7 +Hello =100
F:53:v987fed987da70987f/file2.tex
d:90:=123 +Fool =296
<blank>
```

```json
{
  "peerId": "fraser",
  "paperId": "v987fed987da70987f",
  "commands": [
  {
    "filename": "file1.tex",
    "revision": 34,
    "action": {
      "name": "delta",
      "revision": 41,
      "data": [ "=200", "-7", "+Hello", "=100" ],
      "overwrite": false
     }
  },
  {
    "filename": "file2.tex",
    "revision": 53,
    "action": {
      "name": "delta",
      "revision": 90,
      "data": [ "=123", "+Fool", "=296" ],
      "overwrite": false
    }
  }]
}
```
