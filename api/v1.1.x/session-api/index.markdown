---
layout: default
title: Session API
---

# Session API
{:.no_toc}

* Content
{:toc}

## Api Summary

Method | Path     | Description
------ | -------- | -----------
POST   | /&lt;api&gt;/session | Logs user in
GET    | /&lt;api&gt;/session | Gets the current session data
DELETE | /&lt;api&gt;/session | Logs user out

## Log User In

**Method:** POST

**Path:** _/&lt;api&gt;/session_

**Parameters:**

Name                        | Type   | Description
--------------------------- | ------ | ---------------------------------
username                    | string | The user name  **mandatory**
password                    | string | The user password  **mandatory**

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
201  | _true_         | The user was successfully logged in
400  | _error object_ | Some parameters are missing
401  | _error object_ | The authentication failed
500  | _error object_ | Something wrong happened on the server side and the user could not be registered

## Get Session Data

**Method:** GET

**Path:** _/&lt;api&gt;/session_

**Response:**

Code | Value            | Meaning
---- | --------------   | -------
200  | _session object_ | The session data
401  | _error object_   | User is not logged in
500  | _error object_   | Something wrong happened on the server side

The session data object is as follows:

```json
{
  "name": "glambert",
  "roles": [ "blue_user" ]
}
```

## Log User Out

**Method:** DELETE

**Path:** _/&lt;api&gt;/session_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The user was successfully logged out
500  | _error object_ | Something wrong happened on the server side and the action could not be performed

