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

## Emergency contact details

```shell

Get emergency contacts

curl "http://<BASE_URL>/users/<ID>/econtacts/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "contacts":[
      {
      "em":"hello1@openxcell.com",
      "ph":8899773322,
      "nm":"John"
      },
      {
      "em":"hello2@openxcell.com",
      "ph":9933224455,
      "nm":"Bruce"
      }
    ],
    "n":2
  }
}
```

```shell

Set emergency contacts

curl "http://<BASE_URL>/users/<ID>/econtacts/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"contacts":[{"em": "hello4@openxcell.com", "ph": 8899773321, "nm": "Johny"},
              {"em": "hello5@openxcell.com", "ph": 8899773323, "nm": "Johnathan"}]}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true, 
  "message": "Success"
}
```

This endpoint sets and retrieves a user's emergency contact details.

### HTTP Request (Get contacts)

`GET http://<BASE_URL>/users/<ID>/econtacts/`

### HTTP Request (Set contacts)

`POST http://<BASE_URL>/users/<ID>/econtacts/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved 

## Rider Profile

```shell

Get Rider Profile

curl "https://<BASE_URL>/users/<ID>/settings/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success",
  "data": {
    "nm": "<full name>",
    "gd": "<gender>",
    "ag": "<rider age>",
    "photo": "<profile pic link>"
  }
}
```

```shell

Set Rider Profile details

curl "https://<BASE_URL>/users/<ID>/settings/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"nm": "<rider name>", "ag": <age>, "gd": "<gender>", "content_type": "image/<extension>",
      "file": "<base64 encoded image byte string>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}
```

The endpoint is used to set and retrive Rider profile info.

### HTTP Request (Get profile)

`GET https://<BASE URL>/users/<ID>/settings/`

### HTTP Request (Set profile)

`POST https://<BASE URL>/users/<ID>/settings/`

### URL Parameters

Parameter | Description
----------|------------
ID | Id of the user

## Get user related cars

```shell
curl "http://<BASE_URL>/users/<ID>/cars/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "related_cars":[
       20
    ]
  }
}
```

This method is used to retrive all the cars related to a particular user.

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/cars/`

### URL Parameters

Parameter|Description
---------|-----------
ID| User ID for which cars are to be retrieved


# Cars

## Get car brands

```shell
curl "http://<BASE_URL>/cars/brands/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "brands":[
      "Aston Martin",
      "Audi",
      "Bentley",
      "Caterham",
      "Chevrolet",
      "Conquest",
      "Datsun",
      "DC",
      "BMW",
      "Bugatti",
      "Ferrari",
      "Fiat",
      "Force",
      "Ford",
      "Honda",
      "Hyundai",
      ...
    ]
  }
}
```
The endpoint is used during car setup to get list of car brands.

### HTTP Request

`GET http://<BASE_URL>/cars/brands/`

### URL Parameters

None

## Get car models

```shell
curl "http://<BASE_URL>/cars/<brand>/models/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
  "data":{
    "models":[
      "1 Series",
      "3 Series",
      "X1",
      "5 Series",
      "X3",
      "X5",
      "Z4",
      "7 Series",
      "6 Series",
      "X6",
      "M Series",
      "i8"
    ]
  }
}
```
The endpoint retrives car models when a brand name is provided. This is useful during car setup.

### HTTP Request

`GET http://<BASE_URL>/cars/<brand>/models/`

### URL Parameters

Parameter|Description
--------|------------
brand| Brand name for which models are to be retrieved

## Save car info

```shell
Add new car details:

curl "http://<BASE_URL>/cars/save/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"brand":"<brand>", "model":"<model>", 
    "name": "<car nickname>", "ln":"<license number>", 
    "userid":<user_id>}'
```

> The above method returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "carId":21,
    "imageUrl":"<image_link>",
    "videoUrl":"<video_link>"
  }
}
```

```shell

Update existing car details

curl "http://<BASE_URL>/cars/save/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"brand":"<brand>", "model":"<model>", 
    "name": "<car nickname>", "ln":"<license number>", 
    "userid":<user_id>, "carid": <ID of car to be updated>}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true, 
  "message": "success"
}
```

This method is used to save or update car info when car setup is complete.

### HTTP Request

`POST http://<BASE_URL>/cars/save/`

### URL Parameters

Parameter|Description
---------|-----------
brand | Selected brand of car
model | Selected car model
name | Car nickname given
ln | license number of car
userid | ID of user to which the car belongs
carid | ID of car to be updated

<aside class="note">
  Send <i> carid </i> in POST data only when car details are to be updated
</aside>


## Get car info

```shell
Add new car details:

curl "http://<BASE_URL>/cars/<ID>/overview/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above method returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "name":21,
    "ln":"MH01HN3002",
    "brand":"Honda",
    "model": "Jazz"
  }
}
```

This method is used to get car info when car setup is complete.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/overview/`

### URL Parameters

Parameter|Description
---------|-----------
brand | Selected brand of car
model | Selected car model
name | Car nickname given
ln | license number of car
ID | ID of car to be retrieved


## Speed Limit Settings

```shell
Set Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"sl":<limit>}'
```

> THe above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}

```

```shell
Get Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this 

```json
{
  "status": true,
  "message": "success",
  "data": {
    "speed_limit": 40
  }
}
```
This endpoint sets and retrieves speed limit for a car.  

### HTTP Request (Get Speed Limit)

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`


### HTTP Request (Set Speed Limit)

`POST http://<BASE_URL>/cars/<ID>/speedlimit/`


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be set/retrieved 


## Car Passport


```shell
Car Document Upload

curl "http://<BASE_URL>/cars/<car_id>/upload/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"data": {"dtype": "<document type>", "dinfo":"<document info>", 
     "content_type": "image/<extension>", "file": "<base64 encoded image byte string>",
     "meta": "<optional placeholder for meta info of document>"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true, 
  "message": "success"
}
```


```shell
Car Document Download

curl "http://<BASE_URL>/cars/<car_id>/download/<dtype>"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this 

> 1. Car Profile Download
> 2. Car Document (PUC/DL/Insurance/Service) Download

```json

{
  "status": true,
  "message": "Success",
  "data": {
    "np": "MH01CD007",
    "nm": "My Celerio",
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_profile.jpg?Signature=Llyb%2BY9ASg4JJXqKGx%2FDAxGZsag%3D&Expires=1494583772&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA"
  }
}


{
  "status": true,
  "message": "Success",
  "data": {
    "info": "car registration details",
    "meta": {
      "date": "2015-03-23"
    },
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_registration.jpg?Signature=R86aQe0sGnpBpV44Utcsixih6gg%3D&Expires=1494587758&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA",
    "type": "registration"
  }
}

```

This endpoint sets and retrieves document details of a specific car. This is useful for displaying a car's passport view. 

The Document type here:

Parameter|Description
---------|-------------
profile| Car Profile
reg| Registration Document
puc| Car PUC Document
ins| Insurance Document
dl| Driver's License
ser| Car Service Document

### HTTP Request (Upload Documents)

`POST http://<BASE_URL>/cars/<ID>/upload/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 

### HTTP Request (Download Documents)

`GET http://<BASE_URL>/cars/<ID>/download/<doc type>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved
doc type | Document type 

For more info on base64 encoded image byte strings, see:
<br/><br/>[1] Encode image: https://www.base64-image.de/ 
<br/>[2] Decode image: http://codebeautify.org/base64-to-image-converter

## Get all errrors

```shell
curl "http::/<BASE_URL>/cars/<ID>/errors/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
````

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
  "data":{
    "errors":[
        "P0106",
        "P0108"
      ]
  }
}
```
This endpoint retrieves all the errors occured for a car. This is useful for car diagnostics.


### HTTP Request (Upload Documents)

`GET http://<BASE_URL>/cars/<ID>/errors/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 

## Get specific error

```shell
curl "http::/<BASE_URL>/cars/<ID>/errors/<error code>/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "c":1,
    "l":"http://www.obd-data.com/p0106.html",
    "d":"The problem could be caused by bad MAP sensor or bad PCM, click here for more",
    "e":"P0106",
    "t":"Performance problem"
  }
}
```
This endpoint retrieves error info for a error occured for a car. 


### HTTP Request (Upload Documents)

`GET http://<BASE_URL>/cars/<ID>/errors/<error code>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved
error code| The code returned from <all errors> API

## Get all Trips made by a car

```shell
curl "http://<BASE_URL>/cars/<ID>/trips/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
  "data":{
    "trips":[
      400,
      401,
      402
    ]
  }
}
```

This endpoint retrieves the list of trips made by this car.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/trips/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 

## Get specific trip info

```shell
curl "http://<BASE_URL>/cars/<ID>/trips/<TripID>/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
    "data":{
      "td":{
        "start_server_log_time_stamp":"2016-05-11T06:03:01Z",
        "trip_current_distance":219,
        "hard_break_count":3,
        "is_trip_complete":0,
        "run_time":400,
        "avg_mileage":18,
        "trip_start_distance":165,
        "device_id":300,
        "end_server_log_time_stamp":"2016-05-11T08:03:01Z",
        "total_CO2_emitted":100,
        "id":131,
        "ignition":1,
        "avg_speed":35,
        "message_id":20
      },
    "obd":[
      {
        "lts":"2016-05-11T08:02:01Z",
        "tid":131,
        "mil":19,
        "sts":"2016-05-11T08:02:47Z",
        "lat":23.344,
        "p0D":30,
        "lon":20.401,
        "mid":1
      },
      {
        "lts":"2016-05-11T08:02:31Z",
        "tid":131,
        "mil":20,
        "sts":"2016-05-11T08:15:38Z",
        "lat":23.432,
        "p0D":35,
        "lon":40.223,
        "mid":2
      }
    ]
  }
}
```

This endpoint retrieves specific trip info made by the car.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/trips/<TripID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 
TripID | The trip ID from the all trips call


## Get car notifications

```shell
curl "http://<BASE_URL>/cars/<ID>/notifications/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
  "data":[
    {
      "l":"http://www.obd-data.com/p0108.html",
      "c":1,
      "e":"P0108",
      "t":"Barometric Pressure Circuit High Input",
      "d":"The problem could be caused by bad MAP sensor or worn engine causing low vacuum"
    },
    {
      "l":"http://www.obd-data.com/u0111.html",
      "c":2,
      "e":"U0111",
      "t":"Lost Communication With Battery module",
      "d":"The problem could be caused due to Lost Communication With Energy Control Module"
    },
    {
      "date_time":"2016-05-11T07:51:50.088Z",
      "type":"Car Card",
      "desc":"Your car is safe and healthy"
    },
    {
      "date_time":"2016-05-11T07:53:00.941Z",
      "type":"Car Card",
      "desc":"Turn off your engine to save fuel"
    },
    ...
  ]
}
```
This endpoint retrieves all notifications (errors and cards) for the car.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/notifications/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved

## Latest status

```shell
curl "http://<BASE_URL>/cars/<ID>/status/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```
> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "latitude":23.456,
    "ontrip":true,
    "status_update_time":"2016-05-26T19:14:11.071",
    "speed":55,
    "longitude":40.569
  }
}
```

This endpoint retrieves current car status including speed, location and on trip flag.

### HTTP Request

`GET http://<BASE_UR>/cars/<ID>/status/`

### URL Parameters

Parameter|Description
---------|-----------
ID | The ID of the car for which status is to be retrieved

## Authenticate with Device

```shell
curl "http://<BASE_URL>/cars/<ID>/getkey/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"printedPasscode":"<16-digit passcode>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true, 
  "message": "Success", 
  "data": 
    {
      "nrfid": "123456", 
      "stmid": "C0001", 
      "key": "5634", 
      "device_pk": 4
    }
}
```

This endpoint is used to authenticate device during setup process. The response data can then be used to show device info.

### HTTP Request

`POST http://<BASE_URL>/cars/<ID>/getkey/`

### URL Parameters

Parameter|Description
---------|-----------
ID | Car ID with which the device is to be connected
printedPasscode | 16-digit passcode printed on device

### Response Parameters

Parameter|Description
---------|-----------
nfrid | NFR ID of the device
stmid | STM ID of the device
key | The key to be sent be to device over Bluetooth for authentication
device_pk | Device ID to be used for any subsequent device specific API's

# Devices

## Get Device Info

```shell
curl "http://<BASE_URL>/devices/<ID>/info/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Success",
  "data": {
    "fwID": "309-33-44",
    "devID": "23456123"
  }
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


## Get all Devices

<aside class="warning">
  Deprecated API method
</aside>


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

<aside class="warning">
  Deprecated API method
</aside>


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

# Accounts


## Send OTP to Phone

This API is used as pre-registration, to send OTP to input phone number.

```shell
curl "http://<BASE_URL>/users/getotp/"
  -H "Apikey: <api_key>"
  -X POST 
  -d '{"phone":<phone>}'
```

> The above command returns JSON structured like this:

```json
{
  "status" : true,
  "message": "New code generated and user was sent the code"
}
```

### HTTP Request

`POST https://<BASE_URL>/users/getotp/`

### URL Parameters

Parameter | Description
----------|------------
phone | phone number of the user

### Response Parameters

Parameter | Description
----------|------------
status | OTP send status, true when success, false otherwise
message | success on OTP sent, on failure re-verify


## Phone verification

This API is used before registration, to verify the phone number.

```shell
curl "http://<BASE_URL>/users/verify/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST 
  -d '{"phone":<phone>,"otp":"<otp received>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status" : true,
  "message": "success"
}
```

### HTTP Request

`POST https://<BASE_URL>/users/verify/`

### URL Parameters

Parameter | Description
----------|------------
phone | phone number of the user
otp | OTP received by the user

### Response Parameters

Parameter | Description
----------|------------
status | verification status, true when success, false otherwise
message | success on verification, <i> invalid OTP </i> on failure


## Register

This endpoint registers a new user to the Carnot backend. 

```shell
curl "http://<BASE_URL>/users/register/"
  -H "Content-Type: application/json" 
  -H "Apikey: <api_key>" 
  -X POST 
  -d '{"email":"abc@xyz.com","password":"xyz","name":"John Doe", "phone": 9988776655}' 
```

> The above command returns JSON structured like this:

```json
{
    "status": true, 
    "message": "success", 
    "data": 
    {
        "token": "ae4e00bf6a08cf9cd56a37b99d0162e69db4fd74", 
        "id": 43, 
        "email": "abc@xyz.com",
        "phone": 9988776655
    }
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
phone | 10-digit phone number 

### Response Parameters

Parameter | Description
----------| -----------
status| true if successful, false otherwise
message| Message indicating registration status
token | The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
email | Confirmation of the email id the user entered. Email id also serves as the user name
phone | mandatory field during registration, it could also be used with login instead of email


## Login

This endpoint logs an existing user into the Carnot backend. Successfully logged in users get access to an auth token that should be used in subsequent authenticated requests. 

The login can be done using email or phone.

```shell
curl "http://<BASE_URL>/users/login/"
  -H "Content-Type: application/json"
  -H "Apikey: <api_key>"  
  -X POST 
  -d '{"email":"<email/phone>","password":"xyz"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true, 
  "message": "Success", 
  "data": 
      {
        "token": "ae4e00bf6a08cf9cd56a37b99d0162e69db4fd74", 
        "id": 43, 
        "email": "abc@xyz.com",
        "phone": 9988776655
      }
}


```

### HTTP Request

`POST http://<BASE_URL>/users/login/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address (or phone number) of the user attempting to login. This should be the email or phone used when registering 
password | Password of the registering user

### Response Parameters

Parameter| Description
----------| -----------
token |The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
email | Confirmation of the email id the user entered. Email id also serves as the user name
phone | Phone number of current user
status |true if successful, false otherwise
message |Message indicating login status 


## Logout

This endpoint logs out the user from Carnot backend. 

```shell
curl "http://<BASE_URL>/users/logout/"
  -H "Content-Type: application/json" 
  -H "Apikey: <api_key>" 
  -X POST 
  -d '{"email":"<email/phone>"}'
```

> The above command returns JSON structured like this:

```json
{
    "status": true, 
    "message": "Success"
}
```

### HTTP Request

`POST http://<BASE_URL>/users/logout/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address of the user logging out of system.
phone | Phone number used during registration

### Response Parameters

Parameter | Description
----------| -----------
status| true if successful, false otherwise
message| Message indicating logout status

<aside class="notice">
 On successful logout, user token is deleted. Upon re-login new token gets created.
</aside>


# Alerts / Notifications

## Get Notifications for a Car

```shell
curl "http://<BASE_URL>/cars/12345/notifications/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success",
  "data": {
    "cards": [
      {
        "date_time": "2016-05-11T07:51:50.088Z",
        "type": "Car Card",
        "desc": "Your car is safe and healthy"
      },
      {
        "date_time": "2016-05-11T07:53:00.941Z",
        "type": "Car Card",
        "desc": "Turn off your engine to save fuel"
      },
      {
        "date_time": "2016-05-18T10:47:20.251Z",
        "type": "Car Card",
        "desc": "Your Celerio is getting towed"
      }
    ],
    "errors": [
      {
        "l": "http://www.obd-data.com/p0108.html",
        "c": 1,
        "e": "P0108",
        "t": "Barometric Pressure Circuit High Input",
        "d": "The problem could be caused by bad MAP sensor or worn engine causing low vacuum"
      },
      {
        "l": "http://www.obd-data.com/u0111.html",
        "c": 2,
        "e": "U0111",
        "t": "Lost Communication With Battery module",
        "d": "The problem could be caused due to Lost Communication With Energy Control Module"
      }
    ]
  }
}
```

This endpoint retrieves the list of notifications recorded for a car on the backend. 

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/notifications/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved 

## Get Notifications for a User

```shell
curl "http://<BASE_URL>/users/100/notifications/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Success",
  "data": [
    {
      "date_time": "2016-05-11T07:51:50.088Z",
      "type": "Car Card",
      "desc": "Your car is safe and healthy"
    },
    {
      "date_time": "2016-05-11T07:53:00.941Z",
      "type": "Car Card",
      "desc": "Turn off your engine to save fuel"
    },
    {
      "date_time": "2016-05-18T10:47:20.251Z",
      "type": "Car Card",
      "desc": "Your Celerio is getting towed"
    },
    {
      "link": "http://www.obd-data.com/p0108.html",
      "desc": "The problem could be caused by bad MAP sensor or worn engine causing low vacuum",
      "title": "Barometric Pressure Circuit High Input",
      "type": 1,
      "error": "P0108"
    },
    {
      "link": "http://www.obd-data.com/u0111.html",
      "desc": "The problem could be caused due to Lost Communication With Energy Control Module",
      "title": "Lost Communication With Battery module",
      "type": 2,
      "error": "U0111"
    }
  ]
}
```

This endpoint retrieves the list of notifications recorded for a user. 

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/notifications/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user, the data of which is to be retrieved 

## Rash Driving

```shell
Set Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"sl":<limit>}'
```

> THe above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}

```

```shell
Get Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>" 
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this 

```json
{
  "status": true,
  "message": "success",
  "data": {
    "speed_limit": 40
  }
}
```
This endpoint sets and retrieves speed limit for a car.  

### HTTP Request (Get Speed Limit)

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`


### HTTP Request (Set Speed Limit)

`POST http://<BASE_URL>/cars/<ID>/speedlimit/`


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be set/retrieved 



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
  "status": true,
  "data": {
    "engine_oil": true,
    "battery_health": 50,
    "tyre_pressure_bottom_right": 0,
    "car_errors": [
      "P0106",
      "P0108",
      "U0111"
    ],
    "coolant_temperature": 80,
    "tyre_pressure_bottom_left": 0,
    "tyre_pressure_front_left": 0,
    "cabin_temperature": 40,
    "tyre_pressure_front_right": 0
  },
  "message": "Success"
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
  "status": true,
  "data": {
    "title": "Performance problem",
    "code": "P0106",
    "severity": "Low",
    "ref_link": "http://www.obd-codes.com/p0106",
    "desc": "The problem could be caused due to bad MAP sensor or bad PCM, click here for more"
  },
  "message": "Success"
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


# Documents

API yet to be published

# Servicing

API yet to be published

# Badges 

API yet to be published
