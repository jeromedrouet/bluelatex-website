---
layout: default
title: User API
---

# User API
{:.no_toc}

* Content
{:toc}

## Api Summary

Method | Path                             | Description
------ | -------------------------------- | --------------------------------------------
GET    | /&lt;api&gt;/users                     | Gets list of users
POST   | /&lt;api&gt;/users                     | Registers a new user
GET    | /&lt;api&gt;/users/&lt;name&gt;/reset  | Generates a password reset token
POST   | /&lt;api&gt;/users/&lt;name&gt;/reset  | Performs password reset
GET    | /&lt;api&gt;/users/&lt;name&gt;/info   | Gets the user data
PATCH  | /&lt;api&gt;/users/&lt;name&gt;/info   | Modifies the user data
PATCH  | /&lt;api&gt;/users/&lt;name&gt;/permissions   | Modifies the user custom permissions
GET    | /&lt;api&gt;/users/&lt;name&gt;/permissions   | Gets permission sets available to the user
GET    | /&lt;api&gt;/users/&lt;name&gt;/papers | Gets the list of papers shared with the user
DELETE | /&lt;api&gt;/users/&lt;name&gt;        | Deletes the authenticated user

## Get User List

**Method:** GET

**Path:** _/&lt;api&gt;/users_

**Parameters:**

Name | Type   | Description
---- | ------ | -----------
name | string | The user name, only returns users whose name starts with the given value **optional**

**Response:**

Code | Value                | Meaning
---- | -------------------- | -------
201  | _list of user names_ | The list of matching users
401  | _error object_       | User is not authenticated
500  | _error object_       | Something wrong happened on the server side and the user list could not be returned

## Register User

**Method:** POST

**Path:** _/&lt;api&gt;/users_

**Parameters:**

Name                        | Type   | Description
--------------------------- | ------ | ---------------------------------
username                    | string | The user name  **mandatory**
first\_name                 | string | The user first name **mandatory**
last\_name                  | string | The user last name **mandatory**
email\_address              | string | The user email address **mandatory**
affiliation                 | string | The user affiliation (university, company, ...) **optional**
recaptcha\_response\_field  | string | The ReCaptcha response field **optional** if no captcha configured on the server, **mandatory** otherwise
recaptcha\_challenge\_field | string | The ReCaptcha challenge field **optional** if no captcha configured on the server, **mandatory** otherwise

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
201  | _true_         | The user was successfully registered
400  | _error object_ | Some parameters are missing
401  | _error object_ | The captcha did not verify
409  | _error object_ | A user with the same name already exists
500  | _error object_ | Something wrong happened on the server side and the user could not be registered

## Generate Password Reset Token

**Method:** GET

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/reset_

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The password reset token was successfully created and sent
403  | _error object_ | Logged in users may not request password reset
500  | _error object_ | Something wrong happened on the server side

## Perform Password Reset

**Method:** POST

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/reset_

**Parameters:**

Name                        | Type   | Description
--------------------------- | ------ | ---------------------------------
reset\_token                | string | The reset token **mandatory**
new\_password1              | string | The new password **mandatory**
new\_password2              | string | The new password (repeated) **mandatory**

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The password was successfully reset
400  | _error object_ | Some parameters are missing
500  | _error object_ | Something wrong happened on the server side and the action could not be performed

## Get User Data

**Method:** GET

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/info_

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _user object_  | The user data | *ETag* contains the revision of the user data (to be used when modifying them)
403  | _error object_ | Logged in users may not request password reset | N/A
500  | _error object_ | Something wrong happened on the server side | N/A

The user object is as follows:

```json
{
  "name": "glambert",
  "first_name": "Gérard",
  "last_name": "Lambert",
  "email": "gerard@lambert.org",
  "affiliation": "University of Gnieh"
}
```

## Modify User Data

**Method:** PATCH

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/info_

**Headers:** *If-Match* contains the revision of the user data to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the user data. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The user data was successfully modified | *ETag* contains the new revision of the user data after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modify the user data | N/A
404  | _error object_ | User does not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get Available Permission Sets

**Method:** GET

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/permissions_

**Parameters:**

Name       | Type    | Description
---------- | ------- | -----------
names_only | boolean | Whether to return the set of permission names **optional**. Default is **false**.

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _permission object_  | The permission data | *ETag* contains the revision of the permission data (to be used when modifying them)
500  | _error object_ | Something wrong happened on the server side | N/A

The permission data object is as follows:

```json
{
  "public": {
    "author": ["read", "write", ...],
    "reviewer": ["read"],
    "guest": [],
    "other": [],
    "anonymous": [],
  }
}
```

## Modify Custom Permissions

**Method:** PATCH

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/permissions_

**Headers:** *If-Match* contains the revision of the permission data to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the permission data. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The permission data was successfully modified | *ETag* contains the new revision of the permission data after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized  | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get User Papers

Returns the list of papers the user is involved into, along with the role for each paper.

**Method:** GET

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/papers_

**Response:**

Code | Value               | Meaning
---- | ------------------- | -------
200  | _user role object_  | The array of roles and papers user is involved into
401  | _error object_      | User must be authenticated
500  | _error object_      | Something wrong happened on the server side

The user rule object is as follows:

```json
{
  "paper": "432f209d21090e09c09b0aa",
  "name": "Efficiently Writing Rest Api Documentation",
  "creation_date": "2014-06-20T17:57:21.902",
  "role": "author"
}
```

Possible roles are:
* *author* the user may edit the paper,
* *reviewer* the user may read the paper but not modify it.

## Delete User

**Method:** DELETE

**Path:** _/&lt;api&gt;/users/&lt;name&gt;_

**Parameters:**

Name                        | Type   | Description
--------------------------- | ------ | ---------------------------------
recaptcha\_response\_field  | string | The ReCaptcha response field **optional** if no captcha configured on the server, **mandatory** otherwise
recaptcha\_challenge\_field | string | The ReCaptcha challenge field **optional** if no captcha configured on the server, **mandatory** otherwise

**Response:**

Code | Value          | Meaning
---- | -------------- | -------
200  | _true_         | The user was removed
401  | _error object_ | Captcha did not verify or user could not be authenticated
403  | _error object_ | The user still owns papers (single author of a paper)
500  | _error object_ | Something wrong happened on the server side

