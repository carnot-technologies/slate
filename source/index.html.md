---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Carnot API! You can use our API to access Carnot API endpoints, which can get information on various users, cars, devices and trips in our database.

We have language bindings in Shell. You can view code examples in the dark area to the right.

This API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Carnot uses API keys to allow access to the API. You can get a new API key by writing to us at prathamesh1729@gmail.com

The API key must be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Users

## Get All Users

```shell
curl "http://<BASE_URL>/users/"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {"id":1,
    "user":{"id":2,"username":"U001","email":"U001@carnotmail.com"},
    "gender":"M",
    "age":20,
    "dob":"1996-03-28",
    "cars":[{"id":1,"device":1,"name":"C001","numberplate":"MH01AB0001"}],
    "emergencycontacts":"[{phone: 9820204040, email: help@carnot.com}]",
    "driverscore":89.0,
    "totalnumtrips":10,
    "totaldistance":200.0,
    "totaltime":18000,
    "averagespeed":40.0
  }
]
```

This endpoint retrieves all the users.

<aside class="warning">
 Deprecated API method
</aside>

### HTTP Request

`GET http://<BASE_URL>/users/`

### Query Parameters

None

## Get a Specific User

```shell
curl "http://<BASE_URL>/users/2/"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id":2,
  "user":{"id":3,"username":"U011","email":"U011@carnotmail.com"},
  "gender":"M",
  "age":20,
  "dob":"1996-03-28",
  "cars":[{"id":2,"device":2,"name":"C011","numberplate":"MH01AB0011"}],
  "emergencycontacts":"[{phone: 9820204040, email: help@carnot.com}]",
  "driverscore":89.0,
  "totalnumtrips":10,
  "totaldistance":200.0,
  "totaltime":18000,
  "averagespeed":40.0
}
```

This endpoint retrieves a specific user.

<aside class="warning">
  Deprecated API method  
</aside>

### HTTP Request

`GET http://<BASE_URL>/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


## Get User's emergency contact details

```shell
curl "http://<BASE_URL>/users/2/econtacts/"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{"econtacts": "[{phone: 9820204040, email: help@carnot.com}]"}
```

This endpoint retrieves a user's emergency contact details.

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/econtacts/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get User's cars

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/cars/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 

## Get User's trips

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/trips/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Profile overview

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Profile 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverprofile/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Statistics

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverstats/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Points

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverpoints/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get User Graphs

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/graphs/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


# Cars

## Get all Cars

### HTTP Request

`GET http://<BASE_URL>/cars/`

### URL Parameters

None


## Get a specific Car 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Makes

### HTTP Request

`GET http://<BASE_URL>/cars/makes/`

### URL Parameters

None


## Get all Models

### HTTP Request

`GET http://<BASE_URL>/cars/models/?make=<MAKE>`

### URL Parameters

Parameter | Description
--------- | -----------
MAKE | The Make of the car whose list of Models is to be retrieved


## Get all Links

### HTTP Request

`GET http://<BASE_URL>/cars/links/?make=<MAKE>&model=<MODEL>`

### URL Parameters

Parameter | Description
--------- | -----------
MAKE | The Make of the car, the links of which have to be retrieved  
MODEL | The Model of the car, the links of which have to be retrieved 


## Get Car overview

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car status

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/status/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car statistics 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/statistics`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car's carbon footprint

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/carbonfp/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car's speed limit

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Users using a car

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/users/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Trips made by a car

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/trips/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car Graphs 

### HTTP Request

`GET http://<BASE_URL>/graphs/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


# Devices

## Get all Devices

### HTTP Request

`GET http://<BASE_URL>/devices/`

### URL Parameters

None


## Get a specific Device

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the device, the data of which is to be retrieved 


## Get Device Info

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/info/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the device, the info of which is to be retrieved 


# Trip 

## Get all Trips

### HTTP Request

`GET http://<BASE_URL>/data/trips/`

### URL Parameters

None


## Get a specific Trip 

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip which is to be retrieved  


## Get Trip overview

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get Trip details

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/details/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get a Trip's reportcard

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/reportcard/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get Trip Graphs 

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/graph/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


# OBD

## Get all OBD data points

### HTTP Request

`GET http://<BASE_URL>/data/obd/`

### URL Parameters

None


## Get a specific OBDData point

### HTTP Request

`GET http://<BASE_URL>/data/obd/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the OBD data point which is to be retrieved  