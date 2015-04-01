---
layout: default
title: Notifications API
---

# Notifications API
{:.no_toc}

* Content
{:toc}

## Api Summary

Method | Path                                                                 | Description
------ | -------------------------------------------------------------------- | -----------
GET    | /&lt;api&gt;/users/&lt;name&gt;/notifications                        | Retrieve the notifications settings
PATCH  | /&lt;api&gt;/users/&lt;name&gt;/notifications                        | Modify the notifications settings
GET    | /&lt;api&gt;/notifications                                           | Retrieve the notifications of the authenticated user
DELETE | /&lt;api&gt;/notifications                                           | Deletes the notifications of the authenticated user

## Get User Notifications Settings

**Method:** GET

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/notifications_

**Response:**

Code | Value              | Meaning | Headers
---- | ------------------ | ------- | -------
200  | _settings object_  | The user notifications settings| *ETag* contains the revision of the user settings (to be used when modifying them)
403  | _error object_     | Logged in users may not request password reset | N/A
500  | _error object_     | Something wrong happened on the server side | N/A

The user notifications settings is as follows:

```json
{
  "email_notifications": false,
  "api_notifications": true
}
```

## Modify User Notifications Settings

**Method:** PATCH

**Path:** _/&lt;api&gt;/users/&lt;name&gt;/notifications_

**Headers:** *If-Match* contains the revision of the user notifications settings to modify (as returned in the ETag header)

**Body:** A Json Patch document as per [RFC-6902](http://tools.ietf.org/html/rfc6902) that modifies the user data. A prerequisite is that the structure of the object must not be modified, only the values of standard fields (no new fields, no mandatory field removed, ...)

**Response:**

Code | Value          | Meaning | Headers
---- | -------------- | ------- | -------
200  | _true_         | The user data was successfully modified | *ETag* contains the new revision of the user notifications settings after modifications were applied
304  | _error object_ | Not enough data were sent to perform modification | N/A
401  | _error object_ | User must be authenticated | N/A
403  | _error object_ | Not authorized to modify the user notifications settings | N/A
404  | _error object_ | User does not exist | N/A
409  | _error object_ | No revision or an obsolete revision was provided in the request | N/A
500  | _error object_ | Something wrong happened on the server side and the action could not be performed | N/A

## Get User Notifications

**Method:** GET

**Path:** _/&lt;api&gt;/notifications_

**Response:**

Code | Value            | Meaning
---- | ---------------- | -------
200  | _notifications_  | The current user notifications
401  | _error object_   | Unauthenticated users have no notifications
500  | _error object_   | Something wrong happened on the server side

The user notifications are as follows:

```json
[
  {
    "id": "98214fe98da98c898",
    "timestamp": 1427000000,
    "username": "glambert",
    "message": "I added you as author to the paper 'Introduction to \\BlueLaTeX'"
  },
  {
    "id": "1001ea100a100cd901",
    "timestamp": 1420000000,
    "username": "lsatabin",
    "message": "I added you as reviewer to the paper 'What is a Paper?'"
  }
]
```

## Delete User Notifications

**Method:** DELETE

**Path:** _/&lt;api&gt;/notifications_

**Body:** A Json list of notification identifier strings to delete.

**Response:**

Code | Value            | Meaning
---- | ---------------- | -------
200  | _true_           | The notifications were correctly deleted
401  | _error object_   | Unauthenticated users have no notifications
500  | _error object_   | Something wrong happened on the server side
