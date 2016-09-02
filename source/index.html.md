---
title: Blitz API Reference

language_tabs:
- http

toc_footers:
- <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
- errors

search: true
---

# Introduction

You are welcome to the Blitz API documentation. The APIs give you access to the Blitz V1 API end points which.

The base urls are as follows;

staging url: [https://blitz-api-staging.udacity.com/](https://blitz-api-staging.udacity.com/)

production url: [https://blitz-api.udacity.com/](https://blitz-api.udacity.com/)


# V1

## Coupons

```http
GET /api/v1/coupons/:coupon: HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "coupon" : {
    "id": 100,
    "code": "blitz-b438e21430y6",
    "expiry_date": "2017-03-14T09:46:50.860Z"
  }
}
```

Use this to submit a coupon and get it’s validity.

## Users

```http
POST /api/v1/users HTTP/1.1

{
  "first_name":"alaba",
  "last_name": "wande",
  "email": "makitubelo@gmail.com",
  "phone_no": "0417892319",
  "company":"my new phase"
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "user": {
    "id": 148,
    "first_name": "alaba",
    "last_name": "wande",
    "user_type": "invite",
    "email": "makitubelo@gmail.com",
    "company": "my new phase",
    "phone": "0417892319",
    "token": "eyJ0eXAiOiJKV1QiLCJh..."
  }
}
```

Ping this API to request an invite to the Blitz platform.

### Accepted Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
first_name | true | User first name
last_name | true | User last name
email | true | Request user email
phone_no | true | Phone number
company | true | Company name  user belongs to

## Projects

```http
POST /api/v1/projects HTTP/1.1
Authorization: Bearer <USER BLITZ TOKEN>

{
  "name": "mechanical IOT parts",
  "description": "machine learning cars and parts",
  "tags": [
    "iOS",
    "android",
    "web",
    "machine learning",
    "not allowed tag"
  ]
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "project": {
  "id": 441,
  "name": "mechanical IOT mikolh",
  "description": "machine learning cars",
  "timeline": null,
  "budget": null,
  "status": null,
  "to_service": null,
    "client": {
      "id": 797,
      "email": "muinry@gmail.com",
      "created_at": "2016-08-14T13:01:29.094Z",
      "updated_at": "2016-08-14T19:27:59.535Z",
      "provider": null,
      "uid": null,
      "first_name": "alaba",
      "last_name": "wande",
      "user_type": "client",
      "name": null,
      "phone_no": "0417892319",
      "company": "my new phase",
      "rocket_chat_id": null,
      "coupon_id": null
    },
    "asset_proposals": [],
    "quotes": [],
    "technical_project_manager": {
      "id": 1,
      "full_name": "hello me",
      "phone_number": "08078248986",
      "photo": "photo.jpg",
      "created_at": "2016-07-26T21:33:34.197Z",
      "updated_at": "2016-07-26T23:15:13.294Z",
      "email": "hello@me.com",
      "tags": [
        "format",
        "new"
      ],
      "linked_in": "",
      "project_memberships_count": 8,
      "role": "technical_project_manager"
    },
    "created_at": "2016-08-14T19:57:47.193Z",
    "milestones": [],
    "tags": [
      "android",
      "iOS",
      "web"
    ],
    "end_date": null,
    "start_date": null
  }
}
```

This end point is for creating new projects.

### Accepted Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
  name | true | Project Name
  description | true | Project short pitch
  tags | false | An array of associated project tags. Allowed tags are; android, big data, css, firebase, HTML, iOS, java, javascript, linux, machine learning, mobile, objective-c, python, ruby, SQL, swift, web


## Assets

```http
POST /api/v1/assets HTTP/1.1
Authorization: Bearer <USER BLITZ TOKEN>

{
  "project_id":1,
  "category": "Proposal",
  "assets":[
    {
      "link": "https://s3-us-west-2.amazonaws.com/ago.go/user_uploads/78456892-mikeall",
      "name": "mikeal.jpg"
    },
    {
      "link": "https://s3-us-west-2.amazonaws.com/ago.go/user_uploads/78456892-mikeall",
      "name": "mikeal.jpg"
    }
  ]
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 5,
    "link": "https://s3-us-west-2.amazonaws.com/ago.go/user_uploads/78456892-mikeall",
    "created_at": "2016-08-14T20:03:22.516Z",
    "updated_at": "2016-08-14T20:03:22.516Z",
    "project_id": 1,
    "category_id": 1,
    "name": "mikeal.jpg",
    "description": null
  },
  {
    "id": 6,
    "link": "https://s3-us-west-2.amazonaws.com/ago.go/user_uploads/78456892-mikeall",
    "created_at": "2016-08-14T20:03:22.567Z",
    "updated_at": "2016-08-14T20:03:22.567Z",
    "project_id": 1,
    "category_id": 1,
    "name": "mikeal.jpg",
    "description": null
  }
]
```

Create an asset with the url link, name and project id of the project it is attached to.

### Accepted Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
project_id | true | Id of project to attach asset.
category | true | What type of asset is being sent. Allowed categories are Proposal, and Quote.
assets | true | An array of assets each with the link and name parameters.


## Signed Assets URL

```http
POST /api/v1/s3/sign HTTP/1.1
Authorization: Bearer <USER BLITZ TOKEN>

{
  "fileName": "alltogetherdey",
  "fileType": "image/jpg",
  "timestamp": "4682762981"
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "signedUrl": "https://s3-us-west-2.amazonaws.com/ago.go/user_uploads/4682762981-alltogetherdey?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJQ2EZCPVL3LRYJ5A%2F20..."
}
```

Use this api to get signed URL for file and assets uploads.

### Accepted Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
fileName | true | File name to be uploaded
fileType | true | File type to be uploaded
timestamp | true | Unix time stamp of when file is to be uploaded
