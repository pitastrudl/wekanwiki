# Wekan REST API

The REST API allows you to control and extend Wekan with ease.

If you are an end-user and not a dev or a tester, [create an issue](https://github.com/wekan/wekan/issues/new) to request new APIs.

> All API calls in the documentation are made using `curl`.  However, you are free to use Java / Python / PHP / Golang / Ruby / Swift / Objective-C / Rust / Scala / C# or any other programming languages.

## Production Security Concerns
When calling a production Wekan server, ensure it is running via HTTPS and has a valid SSL Certificate. The login method requires you to post your username and password in plaintext, which is why we highly suggest only calling the REST login api over HTTPS. Also, few things to note:

* Only call via HTTPS
* Implement a timed authorization token expiration strategy
* Ensure the calling user only has permissions for what they are calling and no more

# Summary

### Authentication
| Url | Short Description |
| :--- | :--- |
| `/users/login` | [Authenticate with the REST API.](#login) |

### Users
| Url | Short Description |
| :--- | :--- |
| `/users/register` | [Register a new user.](#user-register) |
| `/api/users` | [Create a new user.](#user-create) |
| `/api/users/:id` | [Deletes an existing user.](#user-delete) |
| `/api/users/:id` | [Gets a user's information.](#user-information) |
| `/api/users` | [All of the users.](#user-list) |
| `/api/user` | [Gets a loggued-in user.](#user-loggued-in) |

---

# Login
| URL | Requires Auth | HTTP Method |
| :--- | :--- | :--- |
| `/users/login` | `no` | `POST` |

## Payload

### Authentication with username
| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `username` | `myusername` | Required | Your username |
| `password` | `my$up3erP@ssw0rd` | Required | Your password |

### Authentication with email
| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `email` | `my@email.com` | Required | Your email |
| `password` | `my$up3erP@ssw0rd` | Required | Your password |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**

## Example Call - As Form Data
```bash
curl http://localhost:3000/users/login \
     -d "username=myusername&password=mypassword"
```

```bash
curl http://localhost:3000/users/login \
     -d "email=my@email.com&password=mypassword"
```


## Example Call - As JSON
```bash
curl -H "Content-type:application/json" \
      http://localhost:3000/users/login \
      -d '{ "username": "myusername", "password": "mypassword" }'
```

```bash
curl -H "Content-type:application/json" \
      http://localhost:3000/users/login \
      -d '{ "email": "my@email.com", "password": "mypassword" }'
```


## Result
```json
{
  "id": "user id",
  "token": "string",
  "tokenExpires": "ISO encoded date string"
}
```

## Result example
```json
{
  "id": "XQMZgynx9M79qTtQc",
  "token": "ExMp2s9ML1JNp_l11sIfINPT3wykZ1SsVwg-cnxKdc8",
  "tokenExpires": "2017-12-15T00:47:26.303Z"
}
```

# User Register
| URL | Requires Auth | HTTP Method |
| :--- | :--- | :--- |
| `/users/register` | `no` | `POST` |

## Payload

| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `username` | `myusername` | Required | Your username |
| `password` | `my$up3erP@ssw0rd` | Required | Your password |
| `email` | `my@email.com` | Required | Your email |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**

## Example Call - As Form Data
```bash
curl http://localhost:3000/users/register \
     -d "username=myusername&password=mypassword&email=my@email.com"
```


## Example Call - As JSON
```bash
curl -H "Content-type:application/json" \
      http://localhost:3000/users/register \
      -d '{ "username": "myusername", "password": "mypassword", "email": "my@email.com" }'
```


## Result
```json
{
  "id": "user id",
  "token": "string",
  "tokenExpires": "ISO encoded date string"
}
```

## Result example
```json
{
  "id": "XQMZgynx9M79qTtQc",
  "token": "ExMp2s9ML1JNp_l11sIfINPT3wykZ1SsVwg-cnxKdc8",
  "tokenExpires": "2017-12-15T00:47:26.303Z"
}
```

# User Create
| URL | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/users` | `yes` | `POST` |

## Payload

| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `username` | `myusername` | Required | Your username |
| `password` | `my$up3erP@ssw0rd` | Required | Your password |
| `email` | `my@email.com` | Required | Your email |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**

## Example Call - As Form Data
```bash
curl  -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      -X POST \
      http://localhost:3000/api/users \
      -d "username=myusername&password=mypassword&email=my@email.com"
```

## Example Call - As JSON
```bash
curl  -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      -H "Content-type:application/json" \
      -X POST \
      http://localhost:3000/api/users \
      -d '{ "username": "myusername", "password": "mypassword", "email": "my@email.com" }'
```

## Example of all steps of create user

1) Login

```
curl http://example.com/users/login \
     -d "username=YOUR-USERNAME-HERE&password=YOUR-PASSWORD-HERE"
```

As response you get your id and token:

```
"id":"YOUR-ID-HERE","token":"YOUR-TOKEN-HERE","tokenExpires":"2017-12-23T21:07:10.395Z"}
```

2) Create user. Works both when serf-register enabled and disabled.

```
curl  -H "Authorization: Bearer YOUR-TOKEN-HERE" \
      -H "Content-type:application/json" \
      -X POST \
      http://example.com/api/users \
      -d '{ "username": "tester", "password": "tester", "email": "tester@example.com", "fromAdmin": "true" }'
```

As reply you get new user's id.

```
{"id":"NEW-USER-ID-HERE"}
```

3) You can get user details with your new user's id:

```
curl -H "Authorization: Bearer YOUR-TOKEN-HERE" \
      http://example.com/api/users/NEW-USER-ID-HERE
```

## Result

Returns the id of the created user.


```json
{
  "_id": "user id"
}
```

## Result example
```json
{
  "_id": "EnhMbvxh65Hr7YvtG"
}
```

# User Delete

> IMPORTANT : Should not be used as long as [this bug](https://github.com/wekan/wekan/issues/1289) exists. 

| URL | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/users/:id` | `yes` | `DELETE` |

## Parameters
| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `id` | `BsNr28znDkG8aeo7W` | Required | The id of the user to delete. |

## Example Call
```bash
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      -X DELETE \
      http://localhost:3000/api/users/EnhMbvxh65Hr7YvtG    
```

## Example Result

Returns the id of the deleted user.

```json
{
  "_id": "EnhMbvxh65Hr7YvtG"
}
```

# User Information
Retrieves information about a user.

| URL | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/users/:id` | `yes` | `GET` |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**
 * **Only the admin user (the first user) can call the REST API.**

## Example Call
```bash
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      http://localhost:3000/api/users/XQMZgynx9M79qTtQc
```

## Result example
```json
{
  "_id": "XQMZgynx9M79qTtQc",
  "createdAt": "2017-09-13T06:45:53.127Z",
  "services": {
    "password": {
      "bcrypt": "$2a$10$CRZrpT4x.VpG2FdJxR3rN.9m0NbQb0OPsSPBDAZukggxrskMtWA8."
    },
    "email": {
      "verificationTokens": [
        {
          "token": "8rzwpq_So2PVYHVSfrcc5f5QZnuV2wEtu7QRQGwOJx8",
          "address": "my@email.com",
          "when": "2017-09-13T06:45:53.157Z"
        }
      ]
    },
    "resume": {
      "loginTokens": [
        {
          "when": "2017-09-13T06:45:53.265Z",
          "hashedToken": "CY/PWeDa3fAkl+k94+GWzCtpB5nPcVxLzzzjXs4kI3A="
        },
        {
          "when": "2017-09-16T06:06:19.741Z",
          "hashedToken": "74MQNXfsgjkItx/gpgPb29Y0MSNAvBrsnSGQmr4YGvQ="
        }
      ]
    }
  },
  "username": "john",
  "emails": [
    {
      "address": "my@email.com",
      "verified": false
    }
  ],
  "isAdmin": true,
  "profile": {}
}
```

# User List
Retrieves the user list.

| URL | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/users` | `yes` | `GET` |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**
 * **Only the admin user (the first user) can call the REST API.**

## Example Call
```bash
curl -H "Authorization: Bearer cwUZ3ZsTaE6ni2R3ppSkYd-KrDvxsLcBIkSVfOCfIkA" \
      http://localhost:3000/api/users
```

## Result
```json
[
  {
    "_id": "user id",
    "username": "string"
  }
]
```

## Result example
```json
[
  {
    "_id": "XQMZgynx9M79qTtQc",
    "username": "admin"
  },
  {
    "_id": "vy4WYj7k7NBhf3AFc",
    "username": "john"
  }
]
```

# User Loggued-in
Retrieves information about a loggued-in user with his auth token.

| URL | Requires Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/user` | `yes` | `GET` |

* Notes:
 * **You will need to provide the `token` for any of the authenticated methods.**

## Example Call
```bash
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      http://localhost:3000/api/user
```

## Result example
```json
{
  "_id": "vy4WYj7k7NBhf3AFc",
  "createdAt": "2017-09-16T05:51:30.339Z",
  "username": "john",
  "emails": [
    {
      "address": "me@mail.com",
      "verified": false
    }
  ],
  "profile": {}
}
```
