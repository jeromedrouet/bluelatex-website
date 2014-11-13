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

## Api Summary

Method | Path                                               | Description
------ | -------------------------------------------------- | -----------
GET    | /&lt;api&gt;/compilers                             | Get list of available compilers
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/compiled/pdf   | Get the compiled paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/compiled/log   | Get the compilation log
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/compiled/png   | Get the image rendering of the compiled paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/compiled/pages | Get the number of pages in the compiled paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/compiler       | Get the compiler settings for the given paper
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/compiler       | Trigger compilation or register to compilation channel
PATCH  | /&lt;api&gt;/papers/&lt;paperid&gt;/compiler       | Modify the compiler settings
DELETE | /&lt;api&gt;//papers/&lt;paperid&gt;/compiler       | Cleanup compilation directory
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/synctex        | Get the generated SyncTeX data

## Get Compiler List

**Mehtod:** GET

**Path:** _/&lt;api&gt;/compilers_

**Response:**

Code | Value           | Meaning
---- | --------------- | -------
200  | _compiler list_ | List of available compilers. An array of compiler names
401  | _error object_  | User could not be authenticated
500  | _error object_  | Something wrong happened on the server side

## Get Compiled Paper

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiled/pdf_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _pdf file_     | The compiled pdf file
401  | _error object_ | User has no right to see the compiled paper
404  | _error object_ | No compiled pdf file was found
500  | _error object_ | Something wrong happened on the server side

## Get Compilation Log

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiled/log_

**Response:**

Code | Value              | Meaning
---- | ------------------ | -------
200  | _compilation log_  | The compilation log file (text file)
401  | _error object_     | User has no right to see the compilation log
404  | _error object_     | No compilation log file was found
500  | _error object_     | Something wrong happened on the server side

## Get Png Rendered Page

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiled/png_

**Parameters:**

Name    | Type | Description
------- | ---- | -----------
page    | int  | The page to render **mandatory**
density | int  | The page rendering quality **optional**

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _rendered png_ | The requested page rendered as png image
401  | _error object_ | User has no right to see the compiled paper
404  | _error object_ | No rendered png file was found for the requested page
500  | _error object_ | Something wrong happened on the server side

## Get Number of Pages

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiled/pages_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _int_          | The number of pages in the compiled version
401  | _error object_ | User has no right to see the compiled paper
404  | _error object_ | No compiled pdf file was found
500  | _error object_ | Something wrong happened on the server side

## Get the Compiler Settings

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiler_

**Parameters:**

Name    | Type | Description
------- | ---- | -----------
page    | int  | The page to render **mandatory**
density | int  | The page rendering quality **optional**

**Response:**

Code | Value               | Meaning | Headers
---- | ------------------- | ------- | -------
200  | _compiler settings_ | The compiler settings | *ETag* contains the revision of the compiler settings (to be used when modifying them)
401  | _error object_      | User has no right to see the compiler settings | N/A
404  | _error object_      | Compiler settings were not found | N/A
500  | _error object_      | Something wrong happened on the server side | N/A

A compiler settings object is as follows:
```json
{
  "compiler": "pdflatex",
  "timeout": 30,
  "interval": 15
}
```

## Trigger Compilation

**Mehtod:** POST

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/compiler_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The paper was successfully compiled.
304  | _false_        | The paper was not modified since last compilation and was not recompiled
401  | _error object_ | User has no right to compile the paper
500  | _error object_ | Something wrong happened on the server side
503  | _error object_ | No compilation task is started

Depending on the server configuration, sending **POST** request to this resource either triggers a new compilation if none is already started (explicit compilation) or registers to the compilation channel (background compilation). In case of background compilation, the server answers when the last compilation ends. This uses long polling to notify client when the paper is compiled.

## Modify the Compiler Settings

**Mehtod:** PATCH

**Path:** _/papers/&lt;paperid&gt;/compiler_

**Headers:** *If-Match* contains the revision of the compiler settings to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the compiler settings. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The compiler settings were successfully modified | *ETag* contains the new revision of the compiler settings after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modifiy the paper data | N/A
404  | _error object_ | Compiler settings do not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Cleanup Compilation Directory

**Mehtod:** DELETE

**Path:** _/&lt;api&gt;//papers/&lt;paperid&gt;/compiler_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The compilation data were successfully removed
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modifiy the paper data | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get SyncTeX data

**Mehtod:** GET

**Path:** _/papers/&lt;paperid&gt;/synctex_

**Response:**

Code | Value                     | Meaning                                     | Headers
---- | ------------------------- | ------------------------------------------- | -------
200  | _gziped synctex file_     | The generated SyncTeX data                  | _Content-Type_ is _application/gzip_
401  | _error object_            | User has no right to see the SyncTeX data   | N/A
404  | _error object_            | No compiled SyncTeX file was found          | N/A
500  | _error object_ | Something wrong happened on the server side            | N/A
