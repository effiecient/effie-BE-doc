---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Effie API
---

# Introduction

documentation for the Effie API
[effie](https://effie.boo)

# Auth

## Check Auth

check if effie token is valid. to get metadata about the user. will give new updated token with new expiry date. So this endpoint is also used to update token. will update photoURL too.

> example request

```shell
curl "https://api.effie.boo/api/auth" \
  -X GET \
  -H "Authorization: auth"
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "username": "username",
    "photoURL": "https://cdn.effie.boo/api/users/username/photo",
    "token": "token"
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/auth`

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

# Users

## Check Google Account

check if the uid given in the body is registered with effie.

> example request

```shell
  curl "https://api.effie.boo/api/users/check-google" \
  -X POST \
  -H "Authorization: auth" \
  -H "Content-Type: application/json" \
  -d '{"uid": "uid"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    // true or false
    "isRegistered": true
  }
}
```

used to check if a google account is registered with effie

### HTTP Request

`POST https://api.effie.boo/api/users/check-google`

### Header Parameters

| Parameter     | required | Description                    |
| ------------- | -------- | ------------------------------ |
| Authorization | true     | access token from google login |

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |

## Login Google

login to effie using google account

> example request

```shell
  curl "https://api.effie.boo/api/users/login-google" \
  -X POST \
  -H "Authorization: auth" \
  -H "Content-Type: application/json" \
  -d '{"uid": "uid"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "token": "effieToken",
    "username": "username",
    "photoURL": "https://cdn.effie.boo/api/users/username/photo"
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/users/login-google`

### Header Parameters

| Parameter     | required | Description              |
| ------------- | -------- | ------------------------ |
| Authorization | true     | access token from google |

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |

## Register Google

register to effie using google account

> example request

```shell
  curl "https://api.effie.boo/api/users/register-google" \
  -X POST \
  -H "Authorization: auth" \
  -H "Content-Type: application/json" \
  -d '{"uid": "uid", "username": "username"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "token": "effieToken",
    "username": "username",
    "photoURL": "https://cdn.effie.boo/api/users/username/photo"
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/users/register-google`

### Header Parameters

| Parameter     | required | Description              |
| ------------- | -------- | ------------------------ |
| Authorization | true     | access token from google |

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |
| username  | true     | The username              |

# Links and Folders

## Create Link

> example request creating 'ppl' link in '/itb' directory

```shell
  curl "https://api.effie.boo/api/directory/link" \
  -X POST \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/itb", "relativePath": "ppl", "username": "christojeffrey", "link": "https://google.com"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### HTTP Request

`POST https://api.effie.boo/api/directory/link`

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

### Body Parameters

| Parameter    | required | Description                                                                                                        |
| ------------ | -------- | ------------------------------------------------------------------------------------------------------------------ |
| path         | true     | The path to the folder or link                                                                                     |
| relativePath | true     | The relative path of the link                                                                                      |
| username     | true     | The username of the user which directory wants to be accessed and written                                          |
| link         | true     | The link                                                                                                           |
| title        | false    | The title of the link. if not given, the title will be use relativePath                                            |
| isPinned     | false    | The isPinned of the link. if not given, the isPinned will be false                                                 |
| publicAccess | false    | The publicPrivilege of the link. if not given, the publicAccess will be 'none'. possible values: none, read, write |

## Create Folder

> example request creating 'ppl' folder in '/itb' directory

```shell
  curl "https://api.effie.boo/api/directory/folder" \
  -X POST \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/itb", "relativePath": "ppl", "username": "christojeffrey"}'

```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### HTTP Request

`POST https://api.effie.boo/api/directory/folder`

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

### Body Parameters

| Parameter    | required | Description                                                                                                        |
| ------------ | -------- | ------------------------------------------------------------------------------------------------------------------ |
| path         | true     | The path to the folder or link                                                                                     |
| relativePath | true     | The relative path of the link                                                                                      |
| username     | true     | The username of the user which directory wants to be accessed and written                                          |
| title        | false    | The title of the link. if not given, the title will be use relativePath                                            |
| isPinned     | false    | The isPinned of the link. if not given, the isPinned will be false                                                 |
| publicAccess | false    | The publicPrivilege of the link. if not given, the publicAccess will be 'none'. possible values: none, read, write |

## Read Links or Folders

> example request

```shell
curl --request GET \
  --url https://api.effie.boo/api/directory/christojeffrey/itb \
  --header 'Authorization: token'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "createdAt": "2023-05-09T11:05:24.824Z",
    "personalAccess": [],
    "isPinned": false,
    "publicAccess": "none",
    "lastModifiedBy": "christojeffrey",
    "id": "BKIeWzFTQKE186zG51Vg",
    "type": "folder",
    "title": "root",
    "linkCount": 0,
    "children": [
      {
        "createdAt": "2023-09-05T16:05:01.190Z",
        "personalAccess": [],
        "isPinned": false,
        "publicAccess": "none",
        "lastModifiedBy": "christojeffrey",
        "linkCount": 2,
        "id": "pu1eQdkNLqBqXVjwjtZS",
        "lastModified": "2023-09-19T15:30:32.279Z",
        "type": "folder",
        "title": "archived",
        "folderCount": 5,
        "relativePath": "archived"
      },
      {
        "createdAt": "2023-05-21T06:40:33.268Z",
        "personalAccess": [],
        "isPinned": false,
        "publicAccess": "none",
        "lastModifiedBy": "christojeffrey",
        "linkCount": 2,
        "id": "JBlXqP4g2NC9FExdzR85",
        "lastModified": "2023-07-20T10:51:43.794Z",
        "type": "folder",
        "title": "effie",
        "folderCount": 0,
        "relativePath": "effie"
      }
    ],
    "lastModified": "2023-09-21T20:32:18.443Z",
    "folderCount": 2,
    "path": "/",
    "relativePath": ""
  }
}
```

### HTTP Request

`GET https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

### Header Parameters

| Parameter     | required | Description                                                    |
| ------------- | -------- | -------------------------------------------------------------- |
| Authorization | false    | effie token. if not given, it can only access public directory |

### URL Parameters

| Parameter | required | Description                                                                 |
| --------- | -------- | --------------------------------------------------------------------------- |
| username  | true     | The username of the user which directory wants to be accessed               |
| path      | false    | The path to the folder or link. If not given, the root directory is assumed |

## Update Link or Folder

### HTTP Request

`PATCH https://api.effie.boo/api/directory/update/<username>/<location>`

```shell
  curl "https://api.effie.boo/api/directory/christojeffrey/tes" \
  -X PATCH \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"newRelativePath": "testing"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### Body Parameters

| Parameter       | required | Description                                                |
| --------------- | -------- | ---------------------------------------------------------- |
| link            | false    | The new link that will replace the previous one            |
| title           | false    | The new title that will replace the previous one           |
| isPinned        | false    | The new isPinned that will replace the previous one        |
| publicAccess    | false    | The new publicPrivilege that will replace the previous one |
| newRelativePath | false    | The new relativePath that will replace the previous one    |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## Move Link or Folder

### HTTP Request

`PATCH https://api.effie.boo/api/directory/update/<username>/<location>`

```shell
  curl "https://api.effie.boo/api/directory/christojeffrey/tes" \
  -X PATCH \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"newPath": "/archived"}'
```

### Body Parameters

| Parameter | required | Description  |
| --------- | -------- | ------------ |
| newPath   | true     | The new path |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## Delete Link or Folder

```shell
  curl "https://api.effie.boo/api/directory/christojeffrey/ppl/bing" \
  -X DELETE \
  -H "Authorization: token"
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### HTTP Request

`DELETE https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

### URL Parameters

| Parameter | required | Description                                                               |
| --------- | -------- | ------------------------------------------------------------------------- |
| username  | true     | The username of the user which directory wants to be accessed and written |
| path      | true     | The path to the folder or link including relativePath                     |
