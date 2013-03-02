# Sendicate API

An overview of Sendicate's API. 


* [API Intro](#api-intro)
* [Response Status Codes](#response-status-codes)
* [API Endpoints](#api-endpoints)
    * [Lists](#lists)
    * [Subscribers](#subscribers)
    * [Custom Fields](#custom-fields)


## API Intro

### Base url

All URLs referenced in this documentation begin with the following url: `https://api.sendicate.net/`

### Request and Response Content Type

POST requests must set the Content-type header to application/json

GET requests return a Content-type of JSON

~~~~
curl -H "Content-type: application/json" -X POST -d '{"email":"foo@bar.com"}' https://api.sendicate.net/v1/lists/LIST_ID/subscribers.json?token=API_TOKEN
~~~~

### Authentication

Sendicate uses tokens for API authentication. You can obtain your token from Account page. You should provide token on each request using one of the following ways.

~~~~
curl https://api.sendicate.net/v1/lists.json?token=YOUR_TOKEN
~~~~

### Token Param

The token can be found by logging into your Sendicate account and going to Manage, then Account, then scrolling down to API Access.

The token is required and should be passed as a request param `token=YOUR_TOKEN`
~~~~
curl https://api.sendicate.net/v1/lists.json?token=YOUR_TOKEN
~~~~


## Response Status Codes

The following status codes are returned by API requests:

| code | type | description |
|---------|------|-------|
| 200 | Success | Request was fulfilled |
| 201 | Success | A new resource was created |
| 400 | Error | Bad request format |
| 404 | Error | Resource not found |
| 422 | Validation errors |
| 500 | Error | An internal server error occurred |

### Success Codes

Success codes have the following codes:

| code | description |
|-----------|-------------|
| GET | Requests will return a "200 OK" response upon success. |
| POST | Requests to create a resource we will return a "201 Created" upon success. |
| POST | Requests which do not create a resource will return a "200 OK" upon success.|
| PUT | Requests to update a resource will return a "200 OK" response upon success. |
| DELETE | Requests to delete a resource will return a "200 OK" response upon success.|



### Errors Codes

If you make a request with an invalid API key you'll receive a 401.

If you make a request with invalid parameters, you'll receive a 400.

If you make a request with invalid data, you'll receive a 422 with errors.

~~~~
{"title":["can't be blank"]}
~~~~

If you try to request a resource that does not exist, you'll receive a 404.

## API Endpoints

This section outlines the following API endpoints:

- [Lists](#lists)
	- [Show Lists](#show-lists)
	- [List Details](#list-details)
	- [Create a List](#create-a-list)
	- [Edit a List](#edit-a-list)
	- [Delete a List](#delete-a-list)
- [Subscribers](#subscribers)
	- [List Subscribers](#list-subscribers)
	- [Add Subscribers](#add-subscribers)
	- [View Subscriber](#view-subscriber)
	- [Update Subscriber](#update-subscriber)
	- [Delete Subscriber](#delete-subscriber)
- [Custom Fields](#custom-fields)
	- [Get All Custom Fields](#get-all-custom-fields)

### Lists

Show and manage subscriber lists.

#### Show Lists

~~~~
GET /v1/lists.json
~~~~

Returns a list of subscribers list under your account

| parameter | description | type |
|-----------|-------------|------|
| id | id of list | string |
| title | title of list | string |
| subscribers_count | subscribers count of list | integer |

#### List Details

~~~~
GET /v1/lists/:id.json
~~~~

Returns a single subscribers list

| parameter | description | type |
|-----------|-------------|------|
| id | id of list | string |
| title | title of list | string |
| subscribers_count | subscribers count of list | integer |

TODO: Custom fields


#### Create a List

~~~~
POST /v1/lists.json
~~~~

Creates a new subscribers list

| parameter | description | type |
|-----------|-------------|------|
| title | title of list | string |

TODO: Custom fields


#### Edit a List

~~~~
PUT /v1/lists/:id.json
~~~~
Updates a single lists properties

| parameter | description | type |
|-----------|-------------|------|
| title | title of list | string |

TODO: Custom fields

#### Delete a List

~~~~
DELETE /v1/lists/:id.json
~~~~

Deletes a list


### Subscribers

Show and manage subscriber details

#### List Subscribers

~~~~
GET /v1/lists/:list_id/subscribers.json
~~~~

Returns a list of subscribers from a selected subscriber list

| parameter | description | type |
|-----------|-------------|------|
| id | id of subscriber | string |
| email | email of subscriber | string |
| name | name of subscriber | string |
| status | subscriber's status | string |
| unsubscribed_at | date when subscriber become unsubscribed | string |
| delivered_count | delivered messages count | integer |
| opened_count | opened messages count | integer |
| clicked_count | clicked messages count | integer |

TODO: Custom fields, joined date.

#### Add Subscribers

~~~~
POST /v1/lists/:list_id/subscribers.json
~~~~

Add subscriber to subscribers list

| parameter | description | type |
|-----------|-------------|------|
| email | email of subscriber | string |
| name | name of subscriber | string |

TODO: Allow for custom fields

#### View Subscriber

~~~~
GET /v1/lists/:list_id/subscribers/:id.json
~~~~

Get details of subscriber

| parameter | description | type |
|-----------|-------------|------|
| id | id of subscriber | string |
| email | email of subscriber | string |
| name | name of subscriber | string |
| status | subscriber's status | string |
| unsubscribed_at | date when subscriber become unsubscribed | string |
| delivered_count | delivered messages count | integer |
| opened_count | opened messages count | integer |
| clicked_count | clicked messages count | integer |

TODO: Custom fields, get lists that the subscriber belongs to, and get mailing history

#### Update Subscriber

~~~~
PUT /v1/lists/:list_id/subscribers/:id.json
~~~~

Update properties of subscribers 

| parameter | description | type |
|-----------|-------------|------|
| name | name of subscriber | string |

TODO: Update additional fields

#### Delete Subscriber

~~~~
DELETE /v1/lists/:list_id/subscribers/:id.json
~~~~

Remove subscriber from list


### Custom Fields

Custom fields are useful for storing extra subscriber data, segmentation, etc.

#### Get All Custom Fields

~~~~
GET /v1/custom_fields.json
~~~~

Get list of custom fields for account.

TODO: Get custom fields settings for each list
