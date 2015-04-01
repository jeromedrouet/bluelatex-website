---
layout: default
title: Papers API
---

# Papers API
{:.no_toc}

* Content
{:toc}

## Api Summary

Method | Path                                                                 | Description
------ | -------------------------------------------------------------------- | -----------
POST   | /&lt;api&gt;/papers                                                  | Create a new paper
DELETE | /&lt;api&gt;/papers                                                  | Delete a paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/info                             | Get the paper data
PATCH  | /&lt;api&gt;/papers/&lt;paperid&gt;/info                             | Modify the paper data
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/roles                            | Get the paper roles
PATCH  | /&lt;api&gt;/papers/&lt;paperid&gt;/roles                            | Modify the paper roles
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/files/resources                  | Get the list of resources associated to this paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt; | Get a resource associated to this paper
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt; | Upload a new resource associated to this paper
DELETE | /&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt; | Delete a resource associated to this paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/files/synchronized               | Get the list of synchronized files for this paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/zip                              | Get a tarball of the paper source files (both synchronized and resources)
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/join                             | Join the paper
POST   | /&lt;api&gt;/papers/&lt;paperid&gt;/part                             | Leave the paper
GET    | /&lt;api&gt;/papers/&lt;paperid&gt;/permissions                      | Retrieve the list of permissions of a paper
PATCH  | /&lt;api&gt;/papers/&lt;paperid&gt;/permissions                      | Modify the list of permissions of a paper

## Create paper

**Mehtod:** POST

**Path:** _/&lt;api&gt;/papers_

**Parameters:**

Name         | Type   | Description
------------ | ------ | ---------------------------------
paper\_name  | string | The paper name used for further reference **madantory**
paper\_title | string | The paper title  **mandatory**
template     | string | The template to use **optional**

**Response:**

Code | Value              | Meaning
---- | ------------------ | -------
201  | _paper identifier_ | The paper was successfully created
400  | _error object_     | Some parameters are missing
401  | _error object_     | User could not be authenticated
500  | _error object_     | Something wrong happened on the server side and the user could not be registered

## Delete Paper

**Mehtod:** DELETE

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The paper was successfully deleted
401  | _error object_ | User could not be authenticated
403  | _error object_ | Authenticated user has no sufficient rights to delete the paper
500  | _error object_ | Something wrong happened on the server side

## Get the Paper Data

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/info_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _paper object_ | The paper data | *ETag* contains the revision of the paper data (to be used when modifying them)
401  | _error object_ | User could not be authenticated | N/A
404  | _error object_ | The paper could not be found | N/A
500  | _error object_ | Something wrong happened on the server side | N/A

A paper object is as follows:

```json
{
  "name": "Writing Good Documentation",
  "creation_date": "2014-06-20T17:57:21.902"
}
```

## Modify the Paper Data

**Mehtod:** PATCH

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/info_

**Headers:** *If-Match* contains the revision of the paper data to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the paper data. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The paper data was successfully modified | *ETag* contains the new revision of the paper data after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modifiy the paper data | N/A
404  | _error object_ | Paper does not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get the Paper Roles

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/roles_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _paper object_ | The paper data | *ETag* contains the revision of the paper roles (to be used when modifying them)
401  | _error object_ | User could not be authenticated | N/A
404  | _error object_ | The paper could not be found | N/A
500  | _error object_ | Something wrong happened on the server side | N/A

A paper object is as follows:

```json
{
  "authors": [ "glambert", "pprince" ],
  "reviewers": []
}
```

## Modify the Paper Roles

**Mehtod:** PATCH

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/roles_

**Headers:** *If-Match* contains the revision of the paper roles to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the paper roles. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The paper roles was successfully modified | *ETag* contains the new revision of the paper roles after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modify the paper data | N/A
404  | _error object_ | Paper does not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get the Paper Resource List

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/files/resources_

**Response:**

Code | Value           | Meaning
---- | --------------- | -------
200  | _resource list_ | The list of resource names associated to this paper
401  | _error object_  | User must be authenticated
403  | _error object_  | Not authorized to get the list of resources
500  | _error object_  | Something wrong happened on the server side and the action could not be performed

## Get a Paper Resource

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt;_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _resource_     | The resource associated to this paper | *Content-Type* is the mime type of the resource
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to get the resource | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Upload a Paper Resource

**Mehtod:** POST (multipart or not)

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt;_

**Parts or Body:** the resource to upload

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The resource was successfully uploaded to the paper
204  | _error object_ | No file sent
401  | _error object_ | User must be authenticated
403  | _error object_ | Not authorized to upload the resource
500  | _error object_ | Something wrong happened on the server side and the action could not be performed

## Delete a Paper Resource

**Mehtod:** DELETE

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/files/resources/&lt;resource&gt;_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _resource_     | The resource associated to this paper
401  | _error object_ | User must be authenticated
403  | _error object_ | Not authorized to delete the resource
500  | _error object_ | Something wrong happened on the server side and the action could not be performed

## Get List of Synchronized Files

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/files/synchronized_

**Response:**

Code | Value           | Meaning
---- | --------------- | -------
200  | _resource list_ | The list of synchronized file names for this paper
401  | _error object_  | User must be authenticated
403  | _error object_  | Not authorized to get the list of files
500  | _error object_  | Something wrong happened on the server side and the action could not be performed

## Get Zipball of the project

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/zip_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _zip file_     | The paper source files and resources zipped | *Content-Type* is application/zip
401  | _error object_ | User must be authenticated
403  | _error object_ | Not authorized to get the zipball
500  | _error object_ | Something wrong happened on the server side and the action could not be performed

## Join a Paper

**Mehtod:** POST

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/join_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | Client joined the paper
401  | _error object_ | User has no sufficient rights to join the paper
500  | _error object_ | Something wrong happened on the server side and the user could not be registered

## Leave a Paper

**Mehtod:** POST

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/part_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | Client left the paper
401  | _error object_ | User has no sufficient rights to leave the paper
500  | _error object_ | Something wrong happened on the server side and the user could not be registered

## Get the Paper Permissions

**Mehtod:** GET

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/permissions_

**Response:**

Code | Value                | Meaning | Headers
---- | -------------------- | ------- | -------
200  | _permissions object_ | The paper permissions | *ETag* contains the revision of the paper permissions (to be used when modifying them)
401  | _error object_       | User could not be authenticated | N/A
404  | _error object_       | The paper could not be found | N/A
500  | _error object_       | Something wrong happened on the server side | N/A

A permission object is as follows:

```json
{
  "author": [ "edit", "delete", "compile", "configure", "publish", "download", "read", "view", "comment", "chat", "fork", "change"-"phase" ]
  "reviewer": [ "compile", "view", "comment" ]
  "guest": [ "compile", "view" ]
  "other": []
  "anonymous": []
}
```

## Modify the Paper Permissions

**Mehtod:** PATCH

**Path:** _/&lt;api&gt;/papers/&lt;paperid&gt;/permissions_

**Headers:** *If-Match* contains the revision of the permissions data to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the paper data. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The paper permissions was successfully modified | *ETag* contains the new revision of the permissions data after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modifiy the paper data | N/A
404  | _error object_ | Paper does not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A
