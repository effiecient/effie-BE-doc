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

# example Introduction

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

# links and folders

## read links or folders

```shell
curl --request GET \
  --url https://api.effie.boo/api/directory/christojeffrey \
  --header 'Authorization: token'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "path": "/",
  "data": {
    "type": "folder",
    "childrens": {
      "test": {
        "isPinned": false,
        "title": "test",
        "type": "folder",
        "shareConfiguration": {
          "isShared": false,
          "sharedPrivilege": "read"
        }
      },
      "itb": {
        "isPinned": false,
        "title": "itb",
        "type": "folder",
        "shareConfiguration": {
          "isShared": false,
          "sharedPrivilege": "read"
        }
      },
      "jeffery-was-here": {
        "isPinned": false,
        "link": "https://bing.com",
        "title": "jeffery-was-here",
        "type": "link",
        "shareConfiguration": {
          "isShared": false,
          "sharedPrivilege": "read"
        }
      },
      "ppl": {
        "isPinned": false,
        "title": "ppl",
        "type": "folder",
        "shareConfiguration": {
          "isShared": true,
          "sharedPrivilege": "write"
        }
      },
      "bing": {
        "isPinned": false,
        "link": "https://bing.com",
        "title": "bing",
        "type": "link",
        "shareConfiguration": {
          "isShared": false,
          "sharedPrivilege": "read"
        }
      }
    },
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### HTTP Request

`GET https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

### URL Parameters

| Parameter | required | Description                                                   |
| --------- | -------- | ------------------------------------------------------------- |
| username  | true     | The username of the user which directory wants to be accessed |

### Path Parameters

| Parameter | required | Description                                                                 |
| --------- | -------- | --------------------------------------------------------------------------- |
| path      | false    | The path to the folder or link. If not given, the root directory is assumed |

### Header Parameters

| Parameter     | required | Description                                                    |
| ------------- | -------- | -------------------------------------------------------------- |
| Authorization | false    | effie token. if not given, it can only access public directory |

## Create Link

```shell
  curl "https://api.effie.boo/api/directory/link" \
  -X POST \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/ppl", "link": "https://bing.com", "relativePath": "bing", "username": "christojeffrey"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "isPinned": false,
    "link": "https://bing.com",
    "title": "bing",
    "type": "link",
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/directory/link`

### Body Parameters

| Parameter      | required | Description                                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| path           | true     | The path to the folder or link                                                                                     |
| link           | true     | The link                                                                                                           |
| relativePath   | true     | The relative path of the link                                                                                      |
| username       | true     | The username of the user which directory wants to be accessed and written                                          |
| title          | false    | The title of the link. if not given, the title will be use relativePath                                            |
| isPinned       | false    | The isPinned of the link. if not given, the isPinned will be false                                                 |
| publicAccess   | false    | The publicPrivilege of the link. if not given, the publicAccess will be 'none'. possible values: none, read, write |
| personalAccess | false    | Is an array of object. The object contains username and access. if not given, the personalAccess will be empty     |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## Create Folder

```shell
  curl "https://api.effie.boo/api/directory/folder" \
  -X POST \
  -H Authorization: token \
  -H "Content-Type: application/json" \
  -d '{"path": "/ppl", "relativePath": "test", "username": "christojeffrey"}'

```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "isPinned": false,
    "title": "test",
    "type": "folder",
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/directory/folder`

### Body Parameters

| Parameter          | required | Description                                                                                        |
| ------------------ | -------- | -------------------------------------------------------------------------------------------------- |
| path               | true     | The path to the folder or link                                                                     |
| relativePath       | true     | The relative path of the link                                                                      |
| username           | true     | The username of the user which directory wants to be accessed and written                          |
| title              | false    | The title of the link. if not given, the title will be use relativePath                            |
| isPinned           | false    | The isPinned of the link. if not given, the isPinned will be false                                 |
| shareConfiguration | false    | The shareConfiguration of the link. if not given, the shareConfiguration will be {isShared: false} |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## update link

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
  "status": "SUCCESS",
  "data": {
    "isPinned": false,
    "link": "https://bing.com",
    "title": "bing",
    "type": "link",
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### Body Parameters

| Parameter          | required | Description                                                               |
| ------------------ | -------- | ------------------------------------------------------------------------- |
| username           | true     | The username of the user which directory wants to be accessed and written |
| path               | true     | The path to the folder or link                                            |
| relativePath       | true     | The relative path of the link                                             |
| link               | false    | The new link that will replace the previous one                           |
| title              | false    | The new title that will replace the previous one                          |
| isPinned           | false    | The new isPinned that will replace the previous one                       |
| shareConfiguration | false    | The new shareConfiguration that will replace the previous one             |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## update folder

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
  "status": "SUCCESS",
  "data": {
    "isPinned": false,
    "link": "https://bing.com",
    "title": "bing",
    "type": "link",
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### HTTP Request

`PATCH https://api.effie.boo/api/directory/folder`

### Body Parameters

| Parameter          | required | Description                                                               |
| ------------------ | -------- | ------------------------------------------------------------------------- |
| username           | true     | The username of the user which directory wants to be accessed and written |
| path               | true     | The path to the folder or link                                            |
| relativePath       | true     | The relative path of the link                                             |
| link               | false    | The new link that will replace the previous one                           |
| title              | false    | The new title that will replace the previous one                          |
| isPinned           | false    | The new isPinned that will replace the previous one                       |
| shareConfiguration | false    | The new shareConfiguration that will replace the previous one             |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |

## delete link or folder

```shell
  curl "https://api.effie.boo/api/directory/christojeffrey/ppl/bing" \
  -X DELETE \
  -H "Authorization: token"
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "data": {
    "isPinned": false,
    "link": "https://bing.com",
    "title": "bing",
    "type": "link",
    "shareConfiguration": {
      "isShared": false
    }
  }
}
```

### HTTP Request

`DELETE https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

### URL Parameters

| Parameter | required | Description                                                               |
| --------- | -------- | ------------------------------------------------------------------------- |
| username  | true     | The username of the user which directory wants to be accessed and written |
| path      | true     | The path to the folder or link including relativePath                     |

### Header Parameters

| Parameter     | required | Description |
| ------------- | -------- | ----------- |
| Authorization | true     | effie token |
