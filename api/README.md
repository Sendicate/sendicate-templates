# Sendicate API

An overview of Sendicate's API. 


* [API Intro](#api-intro)
* [Response Status Codes](#response-status-codes)
* [API Endpoints](#api-endpoints)
    * [Lists](#lists)
    * [List Subscribers](#list-subscribers)
    * [Fields](#fields)

   

## API Intro

### Base url

All URLs referenced in this documentation begin with the following url: `https://api.sendicate.net/`

### Output formats

We support json.


### Authentication

Sendicate uses tokens for API authentication. You can obtain your token from Account page. You should provide token on each request using one of the following ways.

### Token Param

The token can be found by logging into your Sendicate account and going to Manage, then Account, then scrolling down to API Access.

The token is required and should be passed as a request param `token=YOUR_TOKEN`

    curl https://api.sendicate.net/v1/lists.json?token=YOUR_TOKEN


### Clients

- [Sendicate gem](https://github.com/Sendicate/sendicate-ruby)


## Response Status Codes

The following status codes are returned by API requests:

| code | type | description |
|---------|------|-------|
| 200 | Success | Request was fulfilled |
| 201 | Success | A new resource was created |
| 400 | Error | The request cannot be fulfilled |
| 404 | Error | Resource not found |
| 500 | Error | An internal server error occurred |

### Success Codes

Success codes have the following codes:

| method | description |
|-----------|-------------|
| GET | Requests will return a "200 OK" response upon success. |
| POST | Requests to create a resource we will return a "201 Created" upon success. |
| POST | Requests which do not create a resource will return a "200 OK" upon success.|
| PUT | Requests to update a resource will return a "200 OK" response upon success. |
| DELETE | Requests to delete a resource will return a "200 OK" response upon success.|



### Error Codes

If you make a request with an invalid API key you will receive a 401.

If you make a request with invalid parameters, you will receive a 400 with errors.

    {
      "title": ["can"t be blank"]
    }

If you try to request a resource that does not exist, you will receive a 404.


## API Endpoints

This section outlines the following API endpoints:

- [Lists](#lists)
  - [Create a list](#create-a-list)
  - [Show all lists](#show-all-lists)
  - [Show a list](#show-a-list)
  - [Update a list](#update-a-list)
  - [Delete a list](#delete-a-list)
- [List Subscribers](#list-subscribers)
  - [Create or update list subscribers](#create-or-update-list-subscribers)
  - [Show all list subscribers](#show-all-list-subscribers)
  - [Delete a list subscriber](#delete-a-list-subscriber)
- [Subscribers](#subscribers)
  - [Show a subscriber](#show-a-subscriber)
- [Fields](#fields)
  - [Show All Fields](#show-all-fields)


### Lists

Manage subscriber lists.


#### Create a list

Creates a new subscribers list.

`POST` https://api.sendicate.net/v1/lists.json

##### Expected request body

    {
      "title": "Newsletter"
    }

##### Expected response

    HTTP/1.1 201 Created
    Content-Type: application/json; charset=utf-8
  
    {
      "id": "asdf"
      "title": "Newsletter",
      "subscribers_count": 0
    }


#### Show all lists

Returns a list of all your subscriber lists. :turtle:s all the way down.

`GET` https://api.sendicate.net/v1/lists.json

##### Expected response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    [
      {
        "id": "asdf",
        "title": "Newsletter",
        "subscribers_count": 1000
      },
      {
        "id": "qwerty",
        "title": "Beta",
        "subscribers_count": 100
      }
    ]


#### Show a list

Returns the attributes of the requested list.

`GET` https://api.sendicate.net/v1/lists/:list_id.json

##### Parameters

`:list_id` The ID of the requested list.

##### Expected response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
      "id": "asdf",
      "title": "Newsletter",
      "subscribers_count": 1000
    }


#### Update a list

Updates attributes of the requested list.

`PUT` https://api.sendicate.net/:list_id.json

##### Parameters

`:list_id` The ID of the requested list.

##### Expected request body

    {
      "title": "Old Newsletter"
    }

##### Expected response

  HTTP/1.1 200 OK
  Content-Type: application/json; charset=utf-8
  
    {
      "id": "asdf",
      "title": "Old Newsletter",
      "subscribers_count": 1000
    }

#### Delete a list

Deletes the requested list.

`DELETE` https://api.sendicate.net/:list_id.json

##### Parameters

`:list_id` The ID of the requested list.

##### Expected response

    HTTP/1.1 200 OK


### List subscribers

Manage subscribers in a list.


#### Show all list subscribers

Returns all subscribers in the requested list.

`GET` /v1/lists/:list_id/subscribers.json?page=:page

##### Parameters

`:list_id` The ID of the requested list.

`:page` The page of results to return. Default page: 1, default page size: 50)

##### Expected response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    [
      {
        "email": "vanhalen@example.com",
        "name": "van halen",
        "status": "Subscribed",
        "unsubscribed_at": null,
        "delivered_count": 100,
        "opened_count": 100,
        "clicked_count": 100,
        "joined_at": "2013-03-11 01:00:00 UTC",
        "age": "<18" // This is an example of a custom field.
      },
      {
        "email": "foo@example.com",
        "name": "foo bar",
        "status": "Subscribed",
        "unsubscribed_at": null,
        "delivered_count": 100,
        "opened_count": 100,
        "clicked_count": 100,
        "joined_at": "2013-03-11 01:00:00 UTC"
      }
    ]


#### Create or update list subscribers

Creates or updates many subscribers and adds them to the requested list. Only invalid email addresses will cause an import to fail. Errors on other fields will be reported and ignored, but will not cause an import to fail. Existing subscribers will be updated.

`POST` https://api.sendicate.net/v1/lists/:list_id/subscribers.json

##### Parameters

`:list_id` The ID of the requested list.

##### Expected request body for one subscriber

    {
      "email": "vanhalen@example.com",
      "name": "van halen",
      "age": "18-34" // This is an example of a valid custom field
    }

##### Expected request body for many subscribers

    [
      {
        "email": "vanhalen@example.com",
        "name": "van halen",
        "age": "18-34" // This is an example of a valid custom field
      },
      {
        "email": "foo@example.com",
        "name": "foo bar",
        "color": "blue" // This is an example of an invalid field that does not exist
      }
    ]

##### Expected response with errors

    HTTP/1.1 200 Ok
    Content-Type: application/json; charset=utf-8
  
    {
      "imported": 2,
      "updated": 0,
      "failed": 0,
      "errors": [
        {
          "data": {
            "email": "foo@example.com",
            "name": "foo bar",
            "color": "blue"
          },
          "errors": [
            {
              "field": "color",
              "code": "invalid",
              "message": "color is not a valid field"
            }
          ],
          "status": "imported"
        }
      ]  
    }

##### Expected response with failure

  HTTP/1.1 422 Unprocessable entity
  Content-Type: application/json; charset=utf-8
  
    {
      "imported": 1,
      "updated": 0,
      "failed": 1,
      "errors": [
        {
          "data": {
            "email": "foo",
            "name": "foo bar"
          },
          "errors": [
            {
              "field": "color",
              "code": "invalid",
              "message": "color is not a valid field"
            }
          ],
          "status": "imported"
        }
      ]
    }


#### Delete a list subscriber

Deletes the requested list subscriber.

`DELETE` https://api.sendicate.net/v1/:list_id/subscribers/:subscriber_email.json

##### Parameters

`:list_id` The ID of the requested list.

`:subscriber_email` The email address of the requested list subscriber.

##### Expected response

    HTTP/1.1 200 OK


### Subscribers

Manage individual subscribers.


#### Show a subscriber

Returns the attributes of the requested subscriber.

`GET` https://api.sendicate.net/v1/subscribers/:subscriber_email.json

##### Parameters

`:subscriber_email` The email address of the requested subscriber.

##### Expected response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
      "email": "vanhalen@example.com",
      "name": "van halen",
      "status": "Subscribed",
      "unsubscribed_at": null,
      "delivered_count": 0,
      "opened_count": 0,
      "clicked_count": 0,
      "joined_at": "2013-03-11 01:00:00 UTC",
      "age": "18-34" // This is an example of a custom field
    }


### Fields

#### Show all fields

Returns all default fields (email and name) and custom fields. Custom fields are useful for storing extra subscriber data, segmentation, etc.

`GET` https://api.sendicate.net/v1/fields.json

##### Expected response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    [
      {
        "name": "email",
        "options": [],
        "type": "text"
      },
      {
        "name": "name",
        "options: [],
        "type": text"
      },
      {
        "name": "Age",
        "options": ["<18","18-34","34+"],
        "type":"list"
      }
    ]
