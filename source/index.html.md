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

check if effie token is valid. to get metadata about the user

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
    "photoURL": "https://cdn.effie.boo/api/users/username/photo"
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

## Login

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
| photoURL  | true     | The photoURL from google  |

## Register

> example request

```shell
  curl "https://api.effie.boo/api/users/register" \
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

`POST https://api.effie.boo/api/users/register`

### Header Parameters

| Parameter     | required | Description              |
| ------------- | -------- | ------------------------ |
| Authorization | true     | access token from google |

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |
| photoURL  | true     | The photoURL from google  |
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

| Parameter      | required | Description                                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| path           | true     | The path to the folder or link                                                                                     |
| relativePath   | true     | The relative path of the link                                                                                      |
| username       | true     | The username of the user which directory wants to be accessed and written                                          |
| link           | true     | The link                                                                                                           |
| title          | false    | The title of the link. if not given, the title will be use relativePath                                            |
| isPinned       | false    | The isPinned of the link. if not given, the isPinned will be false                                                 |
| publicAccess   | false    | The publicPrivilege of the link. if not given, the publicAccess will be 'none'. possible values: none, read, write |
| personalAccess | false    | Is an array of object. The object contains username and access. if not given, the personalAccess will be empty     |

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

| Parameter      | required | Description                                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| path           | true     | The path to the folder or link                                                                                     |
| relativePath   | true     | The relative path of the link                                                                                      |
| username       | true     | The username of the user which directory wants to be accessed and written                                          |
| title          | false    | The title of the link. if not given, the title will be use relativePath                                            |
| isPinned       | false    | The isPinned of the link. if not given, the isPinned will be false                                                 |
| publicAccess   | false    | The publicPrivilege of the link. if not given, the publicAccess will be 'none'. possible values: none, read, write |
| personalAccess | false    | Is an array of object. The object contains username and access. if not given, the personalAccess will be empty     |

## Read Links or Folders

> example request

```shell
curl --request GET \
  --url https://api.effie.boo/api/directory/christojeffrey/itb/ppl \
  --header 'Authorization: token'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "path": "/itb",
    "relativePath": "ppl",
    "type": "folder",
    "isPinned": false,
    "title": "ppl",
    "createdOn": "2020-12-12T14:00:00.000Z",
    "lastModified": "2020-12-12T14:00:00.000Z",
    "lastModifiedBy": "christojeffrey",
    "publicAccess": "none",
    "personalAccess": [],
    "children": [
      {
        "relativePath": "figma",
        "type": "folder",
        "isPinned": false,
        "title": "test",
        "createdOn": "2020-12-12T14:00:00.000Z",
        "lastModified": "2020-12-12T14:00:00.000Z",
        "lastModifiedBy": "christojeffrey",
        "publicAccess": "none",
        "personalAccess": []
      }
    ]
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

## Update Link

### HTTP Request

`PATCH https://api.effie.boo/api/directory/link`

```shell
  curl "https://api.effie.boo/api/directory/link" \
  -X PATCH \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/ppl", "link": "https://bing.com", "relativePath": "bing", "username": "christojeffrey"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### Body Parameters

| Parameter      | required | Description                                                                                                  |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| username       | true     | The username of the user which directory wants to be accessed and written                                    |
| path           | true     | The path to the folder or link                                                                               |
| relativePath   | true     | The relative path of the link                                                                                |
| link           | false    | The new link that will replace the previous one                                                              |
| title          | false    | The new title that will replace the previous one                                                             |
| isPinned       | false    | The new isPinned that will replace the previous one                                                          |
| publicAccess   | false    | The new publicPrivilege that will replace the previous one                                                   |
| personalAccess | false    | The new personalAccess that will replace the previous one. only value thats inside the array will be updated |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## Update Folder

```shell
  curl "https://api.effie.boo/api/directory/link" \
  -X PATCH \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/ppl", "link": "https://bing.com", "relativePath": "bing", "username": "christojeffrey"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS"
}
```

### HTTP Request

`PATCH https://api.effie.boo/api/directory/folder`

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

### Body Parameters

| Parameter      | required | Description                                                               |
| -------------- | -------- | ------------------------------------------------------------------------- |
| username       | true     | The username of the user which directory wants to be accessed and written |
| path           | true     | The path to the folder or link                                            |
| relativePath   | true     | The relative path of the link                                             |
| link           | false    | The new link that will replace the previous one                           |
| title          | false    | The new title that will replace the previous one                          |
| isPinned       | false    | The new isPinned that will replace the previous one                       |
| publicAccess   | false    | The new publicPrivilege that will replace the previous one                |
| personalAccess | false    | The new personalAccess that will replace the previous one                 |

## delete link or folder

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
