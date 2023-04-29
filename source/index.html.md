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

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# example Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Auth

## check auth

```shell
curl "https://api.effie.boo/api/auth" \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{"token": "token"}'
```

> The above command returns JSON structured like this:

> if success, return username with photoURL

```json
{
  "success": true,
  "username": "username",
  "photoURL": "https://cdn.effie.boo/api/users/username/photo"
}
```

> if false, return message

```json
{
  "success": false,
  "message": "message"
}
```

### HTTP Request

`POST https://api.effie.boo/api/auth`

### Body Parameters

| Parameter | required | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| token     | true     | The effie token to check. given from login or register |

# Users

## check

used to check if a user has been registered

```shell
  curl "https://api.effie.boo/api/users/check" \
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
    "isRegistered": true // or false
  }
}
```

### HTTP Request

`POST https://api.effie.boo/api/users/check`

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |

### Header Parameters

| Parameter     | required | Description                    |
| ------------- | -------- | ------------------------------ |
| Authorization | true     | access token from google login |

## login

```shell
  curl "https://api.effie.boo/api/users/login" \
  -X POST \
  -H "Authorization: auth" \
  -H "Content-Type: application/json" \
  -d '{"uid": "uid", "photoURL": "photoURL"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "token": "effieToken",
  "username": "username",
  "message": "Login successful"
}
```

### HTTP Request

`POST https://api.effie.boo/api/users/login`

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |
| photoURL  | true     | The photoURL from google  |

### Header Parameters

| Parameter     | required | Description              |
| ------------- | -------- | ------------------------ |
| Authorization | true     | access token from google |

## register

```shell
  curl "https://api.effie.boo/api/users/register" \
  -X POST \
  -H "Authorization: auth" \
  -H "Content-Type: application/json" \
  -d '{"uid": "uid", "photoURL": "photoURL", "username": "username"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "SUCCESS",
  "token": "effieToken",
  "username": "username",
  "message": "User registered"
}
```

### HTTP Request

`POST https://api.effie.boo/api/users/register`

### Body Parameters

| Parameter | required | Description               |
| --------- | -------- | ------------------------- |
| uid       | true     | The uid from google login |
| photoURL  | true     | The photoURL from google  |
| username  | true     | The username              |

### Header Parameters

| Parameter     | required | Description              |
| ------------- | -------- | ------------------------ |
| Authorization | true     | access token from google |

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

# error

will return below in general

```json
{
  "status": "ERROR",
  "message": "error message"
}
```
