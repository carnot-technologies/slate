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

You can view code examples to access the API in the dark area to the right.

This API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> Make sure to replace `<api_key>` with your API key and `<auth_token>` with your Auth Token

Carnot uses API keys to allow access to the API. You can get a new API key by writing to us at prathamesh1729@gmail.com

The API key must be included in all API requests to the server in a header that looks like the following:

`Apikey: <api_key>`

Apart from the API key all the endpoints that require user authentication require a Token. The token must be supplied in a header that looks as follows: 

`Authorization: Token <auth_token>`

<aside class="notice">
You must replace <code>&lt;api_key&gt;</code> with your personal API key. You must replace <code>&lt;auth_token&gt;</code> with the user's auth token. 
</aside>

# Users

## Get All Users

```shell
curl "http://<BASE_URL>/users/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
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
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
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
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "econtacts": "[{phone: 9820204040, email: help@carnot.com}]"
}
```

This endpoint retrieves a user's emergency contact details.

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/econtacts/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get User's cars

```shell
curl "http://<BASE_URL>/users/2/cars/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "related_cars": [2]
}
```

This endpoint retrieves the list of cars a user has access to. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/cars/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 

## Get User's trips

```shell
curl "http://<BASE_URL>/users/32/trips/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "related_trips": 
  [
    {
      "idling": 20,
      "elat": 19.423,
      "clutch": 20,
      "hardBreak": 20,
      "slat": 19.124,
      "mileage": 12,
      "date": "2016-04-19T07:05:31.786Z",
      "photo": null,
      "elon": 72.012,
      "hardAcc": 20,
      "id": 91,
      "driveScore": 85.5,
      "speeding": 20,
      "name": "",
      "maxMileage": 35,
      "slon": 71.893
    },
    {
      "idling": 20,
      "elat": 19.423,
      "clutch": 20,
      "hardBreak": 20,
      "slat": 19.124,
      "mileage": 12,
      "date": "2016-04-19T07:05:31.928Z",
      "photo": null,
      "elon": 72.012,
      "hardAcc": 20,
      "id": 92,
      "driveScore": 85.5,
      "speeding": 20,
      "name": "",
      "maxMileage": 35,
      "slon": 71.893
    }
  ]
}
```

This endpoint retrieves the list of trips with info belonging to a particular user. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/trips/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Profile overview

```shell
curl "http://<BASE_URL>/users/2/overview/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "gender": "M", 
  "age": 20, 
  "lname": "Donald", 
  "score": 89.0, 
  "fname": "Alan", 
  "photo": "https://example.com/assets/res/img/layout/profile/default-large.jpg", 
  "ntrips": 10
}
```

This endpoint retrieves the profile overview of the driver. 
Useful for populating the list of drivers in the Car Garage page in the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Full Driver Profile 

```shell
curl "http://<BASE_URL>/users/32/fullprofile/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "profiles": 
  [
    {
      "driverscore": 85,
      "nTrips": 10,
      "tips": [],
      "distance": 100,
      "mileage": 20,
      "hardBreak": 20,
      "badge": [],
      "gender": "M",
      "hardAcc": 20,
      "photo": null,
      "speed": 10,
      "recentBadges": [],
      "time": 36000,
      "idlingTime": 20,
      "isOnTrip": false,
      "name": "",
      "age": 20
    }
  ]
}
```

This endpoint retrieves the full profile of the driver/user. 
Useful for populating the list of drivers in the Car Garage page in the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/fullprofile/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver's Garage Info 

```shell
curl "http://<BASE_URL>/users/32/garage/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "cars": [
    {
      "lat": "19.23",
      "lon": "71.20",
      "speed": "20.00",
      "id": 4,
      "isOnTrip": true,
      "name": "C014"
    }
  ]
}
```

This endpoint retrieves the car garage information of the driver/user. 
Useful for populating the list of cars in the Car Garage page in the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/garage/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Profile 

```shell
curl "http://<BASE_URL>/users/2/driverprofile/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "dob": "1996-03-28", 
  "photo": "https://example.com/assets/res/img/layout/profile/default-large.jpg", 
  "lname": "Donald", 
  "econtacts": "[{phone: 9820204040, email: help@carnot.com}]", 
  "fname": "Alan", 
  "gender": "M"
}
```

This endpoint retrieves the profile of the driver. 
Useful when populating the Driver Profile screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverprofile/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Statistics

```shell
curl "http://<BASE_URL>/users/2/driverstats/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "total_time": 18000, 
  "lname": "Donald", 
  "fname": "Alan", 
  "avg_speed": 40.0, 
  "driver_score": 89.0, 
  "ntrips": 10, 
  "total_dist": 200.0
}
```

This endpoint retrieves the driving statistics of the driver. 
Useful when populating the Driver Profile screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverstats/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


## Get Driver Points

```shell
curl "http://<BASE_URL>/users/2/driverpoints/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "mil_score": 20.0, 
  "idl_score": 20.0, 
  "spd_score": 20.0, 
  "cmp_score": 20.0, 
  "hbr_score": 20.0, 
  "hac_score": 20.0
}
```

```shell
curl "http://<BASE_URL>/users/2/driverpoints/?graph=True"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "mil_score": 20.0, 
  "idl_score": 20.0, 
  "spd_score": 20.0, 
  "graph": 
  [
    {"scr": 89.0, "id": 2, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 3, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 4, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 5, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 6, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 7, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 8, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 9, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 10, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"scr": 89.0, "id": 11, "sts": "2016-03-27T13:43:30.601Z"}
  ], 
  "cmp_score": 20.0, 
  "hbr_score": 20.0, 
  "hac_score": 20.0
}
```

This endpoint retrieves the scoring / points break up for a driver. 
Useful when populating the Driver Profile screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/driverpoints/?graph=<BOOL>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 
BOOL | True or False indicating if the method should return driver points for graphing

## Get User Graphs

```shell
curl "http://<BASE_URL>/users/2/graphs/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "graph": 
  [
    {"id": 2, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 3, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 4, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 5, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 6, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 7, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 8, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 9, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 10, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"id": 11, "sts": "2016-03-27T13:43:30.601Z"}
  ]
}
```

This endpoint retrieves the data points for the past trips graph for a driver. 
Useful when populating the Driver Profile screen on the app. 
Returns the list of trips and their timestamps of occuring. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/graphs/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 


# Cars

## Get all Cars

```shell
curl "http://<BASE_URL>/cars/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "device":1,
    "name":"C001",
    "numberplate":"MH01AB0001"
  },
  {
    "id":2,
    "device":2,
    "name":"C011",
    "numberplate":"MH01AB0011"
  },
  {
    "id":3,
    "device":3,
    "name":"C012",
    "numberplate":"MH01AB0012"
  }
]
```

This endpoint retrieves all the cars.

### HTTP Request

`GET http://<BASE_URL>/cars/`

### URL Parameters

None


## Get a specific Car 

```shell
curl "http://<BASE_URL>/cars/4/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "lat": "19.23",
  "nTrees": 200,
  "cyclefp": 25,
  "lon": "71.20",
  "speed": "20.00",
  "carfp": 2500,
  "isOnTrip": true,
  "name": "C014",  
  "trips": 
  [
    {
      "elat": 19.423,
      "slat": 19.124,
      "date": "2016-04-19T07:05:31.786Z",
      "id": 91,
      "driveScore": 85.5,
      "maxMileage": 35,
      "mileage": 12,
      "photo": "http://profile-images.com/mypic.png",
      "elon": 72.012,
      "name": "PJ",
      "slon": 71.893
    },
    {
      "elat": 19.423,
      "slat": 19.124,
      "date": "2016-04-19T07:05:31.928Z",
      "id": 92,
      "driveScore": 85.5,
      "maxMileage": 35,
      "mileage": 12,
      "photo": "http://profile-images.com/mypic.png",
      "elon": 72.012,
      "name": "PJ",
      "slon": 71.893
    },
    {
      "elat": 19.423,
      "slat": 19.124,
      "date": "2016-04-19T07:05:32.074Z",
      "id": 93,
      "driveScore": 85.5,
      "maxMileage": 35,
      "mileage": 12,
      "photo": "http://profile-images.com/mypic.png",
      "elon": 72.012,
      "name": "PJ",
      "slon": 71.893
    }
  ]
}
```

This endpoint retrieves details of a specific car. This is useful for displaying a car's dashboard. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Makes

```shell
curl "http://<BASE_URL>/cars/makes/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "makes": 
  [
    "Aston Martin", 
    "Audi", 
    "Bentley",
    ...
    "Volvo"
  ]
}
```

This endpoint retrieves all available car makes (manufacturers). 

### HTTP Request

`GET http://<BASE_URL>/cars/makes/`

### URL Parameters

None


## Get all Models

```shell
curl "http://<BASE_URL>/cars/models/?make=Audi"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "models": 
  [
    "A3", "Q3", "A4", "A3 cabriolet", "A6", "Q5", "TT", "S5", "Q7", "S6", "RS5", "A8", "RS6 Avant", "RS7", "R8"
  ]
}
```

This endpoint retrieves all available car models for a given car make (manufacturer). 

### HTTP Request

`GET http://<BASE_URL>/cars/models/?make=<MAKE>`

### URL Parameters

Parameter | Description
--------- | -----------
MAKE | The Make of the car whose list of Models is to be retrieved


## Get all Links

```shell
curl "http://<BASE_URL>/cars/links/?make=Audi&model=TT"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "image_url": null, 
  "video_url": null
}
```

This endpoint retrieves the installation image and video URLs for a car with given Make and Model. Useful for the device installation screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/cars/links/?make=<MAKE>&model=<MODEL>`

### URL Parameters

Parameter | Description
--------- | -----------
MAKE | The Make of the car, the links of which have to be retrieved  
MODEL | The Model of the car, the links of which have to be retrieved 


## Get Car overview

```shell
curl "http://<BASE_URL>/cars/2/overview/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "name":"C011",
  "model":
  {
    "car_manufact":"Volkswagen",
    "car_model":"Beetle",
    "pin_url":null
  }
}
```

This endpoint retrieves the installation image and video URLs for a car with given Make and Model. Useful for the device installation screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car status

```shell
curl "http://<BASE_URL>/cars/2/status/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "latitude": 19.124, 
  "ontrip": false, 
  "status_update_time": "2016-03-27T11:16:34Z", 
  "speed": 40.0, 
  "longitude": 71.893
}
```

This endpoint retrieves the latest status of a particular car and the time when it was last updated. 
Useful on all screens of the app where the live location of the car is to be displayed.  

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/status/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car statistics 

```shell
curl "http://<BASE_URL>/cars/2/statistics/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "total_time": 18000, 
  "total_trips": 10, 
  "avg_mileage": 12.0, 
  "total_distance": 200.0, 
  "carbon_fp": 1600.0
}
```

This endpoint retrieves the overall statistics of the car. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/statistics/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car's carbon footprint

```shell
curl "http://<BASE_URL>/cars/2/carbonfp/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "carbon_fp": 1600.0
}
```

This endpoint retrieves the carbon footprint number of a particular car. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/carbonfp/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car's speed limit

```shell
curl "http://<BASE_URL>/cars/12345/speedlimit/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "speed": {
    "limit": 90
  },
  "trips": 
  [
    {
      "drive_score": 75,
      "slat": 19.1,
      "slon": 72.2,
      "elon": 72.5,
      "speeding": false,
      "hard_acc": 0,
      "trip_id": 12345,
      "idling_time": 23,
      "elat": 19.4,
      "date_time": "20\\/4\\/2016 09:22:03",
      "photo_thumb": "http:\\/\\/4.bp.blogspot.com\\/-7GKsbIB8dZU\\/TkxlNxQXF_I\\/AAAAAAAAANw\\/1CIg1dnXbrs\\/s1600\\/funny-facebook-profile-picture-joke-james-bond.jpg",
      "mileage": 18,
      "hard_break": 0,
      "max_mileage": 21,
      "clutch_usage": 13,
      "name": "Alex Luther"
    }
  ]
}
```

This endpoint retrieves the speedlimit of a particular car. 
And also returns the set of trips made by the car. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Users using a car

```shell
curl "http://<BASE_URL>/cars/2/users/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "related_users": [2]
}
```

This endpoint retrieves the list of users (drivers) using this car. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/users/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get all Trips made by a car

```shell
curl "http://<BASE_URL>/cars/2/trips/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "related_trips": [2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
}
```

This endpoint retrieves the list of trips made by this car.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/trips/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Car Graphs 

```shell
curl "http://<BASE_URL>/cars/2/graphs/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "graph": 
  [
    {"d": 20.0, "t": 120, "m": 12.0, "id": 2, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 3, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 4, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 5, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 6, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 7, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 8, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 9, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 10, "sts": "2016-03-27T13:43:30.601Z"}, 
    {"d": 20.0, "t": 120, "m": 12.0, "id": 11, "sts": "2016-03-27T13:43:30.601Z"}
  ]
}
```

This endpoint retrieves the list of points to plot time series based graphs for distance, running time and mileage graphs.
Data points for distance, run time, mileage are provided for each trip completed by the car. 

### HTTP Request

`GET http://<BASE_URL>/graphs/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


# Devices

## Get all Devices

```shell
curl "http://<BASE_URL>/devices/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "addressableid":"T001",
    "latitude":19.124,
    "longitude":17.893,
    "speed":0.0,
    "ontrip":false,
    "gsmsignal":0,
    "deviceplugged":true,
    "bluetoothconn":false,
    "stmid":0,
    "nrfid":0,
    "hwid":0
  }
]
```

This endpoint retrieves the entire list of devices registered in the database.

### HTTP Request

`GET http://<BASE_URL>/devices/`

### URL Parameters

None


## Get a specific Device

```shell
curl "http://<BASE_URL>/devices/2/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "id":2,
  "addressableid":"T011",
  "latitude":19.124,
  "longitude":17.893,
  "speed":0.0,
  "ontrip":false,
  "gsmsignal":0,
  "deviceplugged":true,
  "bluetoothconn":false,
  "stmid":0,
  "nrfid":0,
  "hwid":0
}
```

This endpoint retrieves a particular device registered in the database.

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the device, the data of which is to be retrieved 


## Get Device Info

```shell
curl "http://<BASE_URL>/devices/2/info/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "stmid":0,
  "nrfid":0,
  "hwid":0
}
```

This endpoint retrieves the info of a particular device.
Useful for the Device Info screen on the app. 

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/info/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the device, the info of which is to be retrieved 


# Trip 

## Get all Trips

```shell
curl "http://<BASE_URL>/data/trips/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "device":1,
    "trip_id":0,
    "message_id":0,
    "hard_acceleration_count":0,
    "hard_break_count":0,
    "trip_distance":20.0,
    "trip_time":120,
    "avg_speed":10.0,
    "avg_mileage":12.0,
    "total_CO2_emitted":100.0
  },
  ...
]
```

This endpoint retrieves the list of all trips ever recorded on the database.  

### HTTP Request

`GET http://<BASE_URL>/data/trips/`

### URL Parameters

None


## Get a specific Trip 

```shell
curl "http://<BASE_URL>/data/trips/2/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "start_time": "2016-03-27T13:43:30.601Z", 
  "user": 2, 
  "trip_time": 120, 
  "start_lat": 19.124, 
  "avg_mileage": 12.0, 
  "distance": 20.0, 
  "end_lon": 71.895, 
  "start_lon": 71.893, 
  "car": 2, 
  "route": 
  [
    {
      "id": 101, 
      "sts": "2016-03-25T15:35:52.444365Z", 
      "mil": 12.0, 
      "lat": 19.225, 
      "lon": 72.994
    }, 
    {
      "id": 102, 
      "sts": "2016-03-25T15:35:52.585972Z", 
      "mil": 12.0, 
      "lat": 19.226, 
      "lon": 72.99499999999999
    },
    ...
  ],
  "end_time": "2016-03-27T13:43:30.583Z", 
  "end_lat": 19.126, 
  "avg_speed": 10.0, 
  "drive_score": 89.0
} 
```

This endpoint retrieves info of a particular trip  

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip which is to be retrieved  


## Get Trip overview

```shell
curl "http://<BASE_URL>/data/trips/2/overview/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "start_lon": 71.893, 
  "car": 2, 
  "start_time": "2016-03-27T13:43:30.601Z", 
  "start_lat": 19.124, 
  "avg_mileage": 12.0, 
  "drive_score": 89.0
}
```

This endpoint retrieves the overview info for a particular trip. 
This is useful for displaying trip cards in the app. 

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/overview/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get Trip details

```shell
curl "http://<BASE_URL>/data/trips/2/details/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "start_time": "2016-03-27T13:43:30.601Z", 
  "user": 2, 
  "trip_time": 120, 
  "start_lat": 19.124, 
  "avg_mileage": 12.0, 
  "distance": 20.0, 
  "end_lon": 71.895, 
  "start_lon": 71.893, 
  "car": 2, 
  "route": 
  [
    {
      "id": 101, 
      "sts": "2016-03-25T15:35:52.444365Z", 
      "mil": 12.0, 
      "lat": 19.225, 
      "lon": 72.994
    }, 
    {
      "id": 102, 
      "sts": "2016-03-25T15:35:52.585972Z", 
      "mil": 12.0, 
      "lat": 19.226, 
      "lon": 72.99499999999999
    },
    ...
  ],
  "end_time": "2016-03-27T13:43:30.583Z", 
  "end_lat": 19.126, 
  "avg_speed": 10.0, 
  "drive_score": 89.0
} 
```

This endpoint retrieves detailed info for a particular trip.  

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/details/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get a Trip's reportcard

```shell
curl "http://<BASE_URL>/data/trips/2/reportcard/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "hbr_points": 20.0, 
  "spd_points": 20.0, 
  "idl_points": 20.0, 
  "clt_points": 20.0, 
  "hac_points": 20.0, 
  "drive_score": 89.0
}
```

This endpoint retrieves the breakdown of driving points for a particular trip. 
Useful for the Trip Detailed view in the app. 

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/reportcard/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


## Get Trip Graphs 

```shell
curl "http://<BASE_URL>/data/trips/2/graph/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "graph": 
  [
    {"id": 101, "sts": "2016-03-25T15:35:52.444365Z", "mil": 12.0}, 
    {"id": 102, "sts": "2016-03-25T15:35:52.585972Z", "mil": 12.0}, 
    {"id": 103, "sts": "2016-03-25T15:35:52.764028Z", "mil": 12.0}, 
    {"id": 104, "sts": "2016-03-25T15:35:52.910171Z", "mil": 12.0}, 
    {"id": 105, "sts": "2016-03-25T15:35:53.055528Z", "mil": 12.0}, 
    {"id": 106, "sts": "2016-03-25T15:35:53.200362Z", "mil": 12.0}, 
    {"id": 107, "sts": "2016-03-25T15:35:53.334345Z", "mil": 12.0}, 
    {"id": 108, "sts": "2016-03-25T15:35:53.468199Z", "mil": 12.0}, 
    ...
  ], 
  "avg_mileage": 12.0
}
```

This endpoint retrieves the complete mileage graphing info with average mileage for a particular trip.  

### HTTP Request

`GET http://<BASE_URL>/data/trips/<ID>/graph/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip, the data of which is to be retrieved 


# OBD

## Get all OBD data points

```shell
curl "http://<BASE_URL>/data/obd/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "device":1,
    "trip":1,
    "sts":"2016-03-25T15:11:16.610534Z",
    "message_id":0,
    "lat":19.124,
    "lon":71.893,
    "speed":20.0,
    "mil":12.0
  },
  {
    "id":2,
    "device":1,
    "trip":1,
    "sts":"2016-03-25T15:21:14.517005Z",
    "message_id":1,
    "lat":19.1241,
    "lon":72.8931,
    "speed":20.0,
    "mil":12.0
  },
  ...
]
```

This endpoint retrieves the entire list of all OBD data points recorded on the database.  

### HTTP Request

`GET http://<BASE_URL>/data/obd/`

### URL Parameters

None


## Get a specific OBDData point

```shell
curl "http://<BASE_URL>/data/obd/2/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "id":2,
  "device":1,
  "trip":1,
  "sts":"2016-03-25T15:21:14.517005Z",
  "message_id":1,
  "lat":19.1241,
  "lon":72.8931,
  "speed":20.0,
  "mil":12.0
}
```

This endpoint retrieves info of a particular OBD data point. 

### HTTP Request

`GET http://<BASE_URL>/data/obd/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the OBD data point which is to be retrieved  


# Accounts

## Register

<aside class="warning">
 API not yet live!
</aside>

This endpoint registers a new user to the Carnot backend. 

```shell
curl "http://<BASE_URL>/users/register/"
  -H "Content-Type: application/json" 
  -H "Apikey: <api_key>" 
  -X POST 
  -d '{"email":"abc@xyz.com","password":"xyz","name":"John Doe"}' 
```

> The above command returns JSON structured like this:

```json
{
  "token": "ecabc338b3d5e9457364dd92f33da9ced55ce7d6", 
  "id": 23, 
  "email": "abc@xyz.com"
}

```

### HTTP Request

`POST http://<BASE_URL>/users/register/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address of the registering user. This eventually becomes the unique username required for login 
password | Password of the registering user
name | Name of the registering user  

### Response Parameters

Parameter | Description
----------| -----------
token | The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
email | Confirmation of the email id the user entered. Email id also serves as the user name


## Login

<aside class="warning">
 API not yet live!
</aside>

This endpoint logs an existing user into the Carnot backend. Successfully logged in users get access to an auth token that should be used in subsequent authenticated requests. 

```shell
curl "http://<BASE_URL>/users/login/"
  -H "Content-Type: application/json"
  -H "Apikey: <api_key>"  
  -X POST 
  -d '{"email":"abc@xyz.com","password":"xyz"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": 200, 
  "email": "abc@xyz.com", 
  "message": "Success", 
  "token": "ecabc338b3d5e9457364dd92f33da9ced55ce7d6", 
  "id": 23
}
```

### HTTP Request

`POST http://<BASE_URL>/users/login/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address of the user attempting to login. This should be the email used when registering 
password | Password of the registering user

### Response Parameters

Parameter | Description
----------| -----------
token | The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
email | Confirmation of the email id the user entered. Email id also serves as the user name
status | 200 if successful, otherwise 204
message | Message indicating login status 


# Alerts / Notifications

## Get Notifications for a car

```shell
curl "http://<BASE_URL>/cars/12345/notifications/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "type": "Car card",
    "title": "All your cars are safe and healthy",
    "message": "",
    "date_time": "02/21/16 19:03:33"
  }
]
```

This endpoint retrieves the list of notifications recorded for a car on the backend. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/notifications/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


# DTC

## Get Diagnostic Info for a car

```shell
curl "http://<BASE_URL>/cars/12345/diagnostics/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "battery_health": 50,
  "cabin_temperature": 40,
  "coolant_temperature": 80,
  "engine_oil": true,
  "tyre_pressure_front_left": 0,
  "tyre_pressure_front_right": 0,
  "tyre_pressure_bottom_left": 0,
  "car_errors": 
  [
    "P0106",
    "P0108",
    "U0111"
  ]
}
```

This endpoint retrieves the diagnostic info for a car.  

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/diagnostics/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 


## Get Error Code Info

```shell
curl "http://<BASE_URL>/cars/12345/errors/P0106/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "code": "P0106",
  "title": "Performance problem",
  "desc": "The problem could be caused due to bad MAP sensor or bad PCM, click here for more",
  "severity": "Low",
  "ref_link": "http://www.obd-codes.com/p0106"
}
```

This endpoint retrieves the detailed info of a particular error code recorded on a car.  

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/errors/<EID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 
EID | The error code, the info of which is to be retrieved 

# Documents

API yet to be published

# Servicing

API yet to be published

# Badges 

API yet to be published
