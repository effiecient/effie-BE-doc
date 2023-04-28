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

### HTTP Request

`POST https://api.effie.boo/api/auth`

### Body Parameters

| Parameter | required | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| token     | true     | The effie token to check. given from login or register |

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

# Users

## check

used to check if a user has been registered

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

## login

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

## register

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

# links and folders

## read links or folders

### HTTP Request

`GET https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

## write link

### HTTP Request

`POST https://api.effie.boo/api/directory/link`

## write folder

### HTTP Request

`POST https://api.effie.boo/api/directory/folder`

## update link

### HTTP Request

`PATCH https://api.effie.boo/api/directory/link`

## update folder

### HTTP Request

`PATCH https://api.effie.boo/api/directory/folder`

## delete link or folder

### HTTP Request

`DELETE https://api.effie.boo/api/directory/<username>/<path>/<to>/<folder>/<or>/<link>`

```

```
