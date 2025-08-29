# Smart Booking Api

## Login Module

**Login User**

Step 1 : `Get : /auth/url`

Response :

```json
{
    "url": "https://login.microsoftonline.com/06ed72e8-a419-4795-9eb3-5512cf1d3d98/oauth2/v2.0/authorize?client_id=a69198cc-ed8e-42b8-92cc-1f0661506816&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%3A5001%2Fauth%2Fcallback&response_mode=query&scope=openid profile email User.Read"
}
```

Step 2 : Redirect to the above url and login with your MS credentials .Its will provide a code .

```json

{"code":"1.AVMA6HLtBhmklUees1USzx09mMyYkaaO7bhCkswfBmFQaBbFANVTAA.AgABBAIAAABVrSpeuWamRam2jAF1XRQEAwDs_wUA9P_Y8lQqZ6KYU64dbzXopg1_tpucgIQMeJEcBecvtcnUgznJWc96Y3dbDI1ZzcR4NrzS7DbakHDmDqZCBef04XYD_4auvZrQ3i8PdhtFJzETuTbOtSzXFKfKJUfXwNGlWhIq-pTKgibiqhBzC4notTjxav-ysbfaL0AXQf215yaq4ptuHPwr1eJ6fnk-vNZMMxwE-Zca5jlmkb3Nz1MXW6-r_yOdGNftr9udRjgEYgf2FT7lKm3Lvu5Ecg7u7twQGKWRRbHtVwZvcmGf212e-w-grQY0QSGV6B46xx5etWDeYMbEW72cPYhKY1OfvHn0YzITWZ6Pg-uq1l6pKoDakasBJbOQXZaOsKtZpSGNknlwc7dfNYgigjApRCWo7Ds1ginKpdXaRCQbqOK2BvmxEJ22PqpcNS4jYu2zZ7TUitK9nVJa62l-DQ2SV2YrQNSy5nWdcoZOOVD6-4KH9S5NpmLCKgZBW1LNtXj8MiDgzLeMx9EcC1JIKA-9Xx0qPGoZu9RjlKaBMEYQozZLGlGhlg52drvuaNQWVqod0SfkNqXpEG70b7ayEBhmbLtQ2OsK_LgibozhtP9c6JGE3CBZe2Xi7kLk1vYU_h4smWS-GcolHy6bA09uXcrsrgJfusT3t4PmJZwZ_52U81SRGuKeONzezMt6_XshwCGvUq1WtofIsp_znGtYRUNhSqHu9vP4xUQ3KVuFbqbKCaInWp5EOAP3pkU6yjD6TpIKgd8-mv_K48j7VNDfrsRQx1EVyefUM1Zf2lUGX4IITcGRfVibZ7sSg4b2XlVTDz_WX8okmjSGlFUxBiJa3IDwSZTT1FDuSUg_4_G4GTez8-RWTE8bvpN8k-C8psDd_BgMwrD3qj1PKIq1q8EgAADPpLeIW6TOiSUoe0dcrMvjI8cEPGBgqDJmxNHVqcFQ1rTIBPULMdgIbJiTRbOR_Y-q68T8DVmzwbXIoGF0"}

```

Note : The  code is valid for only 5 minutes and can be redeem  only once .So use is wisely to get the access token .

Step 3 : `Post : /login`

Body 

```json

{"code":"1.AVMA6HLtBhmklUees1USzx09mMyYkaaO7bhCkswfBmFQaBbFANVTAA.AgABBAIAAABVrSpeuWamRam2jAF1XRQEAwDs_wUA9P_Y8lQqZ6KYU64dbzXopg1_tpucgIQMeJEcBecvtcnUgznJWc96Y3dbDI1ZzcR4NrzS7DbakHDmDqZCBef04XYD_4auvZrQ3i8PdhtFJzETuTbOtSzXFKfKJUfXwNGlWhIq-pTKgibiqhBzC4notTjxav-ysbfaL0AXQf215yaq4ptuHPwr1eJ6fnk-vNZMMxwE-Zca5jlmkb3Nz1MXW6-r_yOdGNftr9udRjgEYgf2FT7lKm3Lvu5Ecg7u7twQGKWRRbHtVwZvcmGf212e-w-grQY0QSGV6B46xx5etWDeYMbEW72cPYhKY1OfvHn0YzITWZ6Pg-uq1l6pKoDakasBJbOQXZaOsKtZpSGNknlwc7dfNYgigjApRCWo7Ds1ginKpdXaRCQbqOK2BvmxEJ22PqpcNS4jYu2zZ7TUitK9nVJa62l-DQ2SV2YrQNSy5nWdcoZOOVD6-4KH9S5NpmLCKgZBW1LNtXj8MiDgzLeMx9EcC1JIKA-9Xx0qPGoZu9RjlKaBMEYQozZLGlGhlg52drvuaNQWVqod0SfkNqXpEG70b7ayEBhmbLtQ2OsK_LgibozhtP9c6JGE3CBZe2Xi7kLk1vYU_h4smWS-GcolHy6bA09uXcrsrgJfusT3t4PmJZwZ_52U81SRGuKeONzezMt6_XshwCGvUq1WtofIsp_znGtYRUNhSqHu9vP4xUQ3KVuFbqbKCaInWp5EOAP3pkU6yjD6TpIKgd8-mv_K48j7VNDfrsRQx1EVyefUM1Zf2lUGX4IITcGRfVibZ7sSg4b2XlVTDz_WX8okmjSGlFUxBiJa3IDwSZTT1FDuSUg_4_G4GTez8-RWTE8bvpN8k-C8psDd_BgMwrD3qj1PKIq1q8EgAADPpLeIW6TOiSUoe0dcrMvjI8cEPGBgqDJmxNHVqcFQ1rTIBPULMdgIbJiTRbOR_Y-q68T8DVmzwbXIoGF0"}

```

Response :

```
{
    "success": true,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwiZW1haWwiOiJ2ZWVyYW5kcmEucHJhc2F0aEBzb2xpdG9udGVjaC5jb20iLCJuYW1lIjoiVmVlcmFuZHJhIFByYXNhdGgiLCJyb2xlIjoiUHJvamVjdCBFbmdpbmVlciIsImFjY2VzcyI6InVzZXIiLCJpYXQiOjE3NTYzMDU5NzQsImV4cCI6MTc1NjM5MjM3NH0.4xUdSi-S1yroV9j181qsCIPo8t42FiS_unCf02y0e1A",
    "user": {
        "id": 2,
        "name": "Veerandra Prasath",
        "email": "veerandra.prasath@solitontech.com",
        "role": "Project Engineer",
        "accessLevel": "user",
        "gender": null
    }
}

```
This token is valid upto 24 hr from the time of generation.

Note : 


Also the user will be created automatically in the database when he login for the first time with default user access level.
But after that we need to update the gender of the user using the following endpoint.

**Update user gender**
`Patch : /api/users/{userId}/gender`

Body

```
{
  "gender": "male"
}
```

Response :

```
{
    "success": true,
    "message": "User gender updated successfully",
    "data": {
        "id": 2,
        "name": "Veerandra Prasath",
        "email": "veerandra.prasath@solitontech.com",
        "gender": "male",
        "role": "Project Engineer",
        "access": "user"
    }
}
```

## User Module

### Booking Page

1.**Get all users** 

`get : /api/users`


**Response**:

```json
[
    {
        "id": 1,
        "name": "Veerandra Prasath",
        "email": "veerandra.prasath@solitontech.com",
        "role": "Project Engineer",
        "gender": "male",
        "access": "user"
    }
]
```


**Create Booking**

`POST : /api/bookings`


Individual Booking:
```JSON
{
  "requesterId": 1,
  "cityId": 1,
  "bookingType": "individual",
  "BookingMembers": [
    {
      "userId": 1,
      "checkInTime": "2025-07-30T09:00:00",
      "checkOutTime": "2025-07-30T18:00:00"
    }
  ]
}
```
Team Booking :
```
{
  "requesterId": 1,
  "cityId": 1,
  "bookingType": "team",
  "BookingMembers": [
    {
      "userId": 1,
      "checkInTime": "2025-07-30T09:00:00",
      "checkOutTime": "2025-07-30T18:00:00"
    },
     {
      "userId": 1,
      "checkInTime": "2025-07-30T09:00:00",
      "checkOutTime": "2025-07-30T15:00:00"
    }
  ]
}

```

Incorrect request response :

```
{
    "success": false,
    "error": "User 1 already has a pending request for the same time period"
}
```

```
{
    "success": false,
    "error": "User 1 already has an active or upcoming accommodation during the requested time period"
}

```

**Get Availability**

This get availability return the available number of beds for the requested time period which the count is reduced from the number of booking members requested previously for the same overlapping time period.

**For example:**

There are 4 beds available for the time period 9 AM to 6 PM on 30th July 2025.But already 2 members have requested for the same time period, so the available beds will be 2.

**Request** : `Post :/api/availability/check/{cityId}`

Body :
```JSON
{
  "checkInTime": "2025-07-30T09:00:00",
  "checkOutTime": "2025-07-30T18:00:00"
}
```

Response :

```JSON
{
    "availableBeds": 4
}
```

**Get BookingTypes**

Request : `Get : /api/bookings/bookingTypes`

Response:
```
{
    "success": true,
    "bookingTypes": [
        "individual",
        "team"
    ]
}
```

**Get Cities**

`GET : /api/cities`

Response:
```
[
    {
        "id": 1,
        "name": "Madurai"
    }
]
```

--------------------------------

### User pending Page


**Get User pending Request**



Request : `Get : /api/requests/pending/user/{userId}`


Response :

```JSON
{
    "success": true,
    "status": "pending",
    "data": [
        {
            "requestId": 5,
            "cityName": "Madurai",
            "bookingType": "individual",
            "requestedAt": "2025-08-26T05:22:25.111Z",
            "remarks": null,
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "mail": "veerandra.prasath@solitontech.com",
                "role": "Project Engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "username": "Veerandra Prasath",
                    "role": "Project Engineer",
                    "gender": "male",
                    "mail": "veerandra.prasath@solitontech.com",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z"
                }
            ]
        },
        {
            "requestId": 4,
            "cityName": "Madurai",
            "bookingType": "individual",
            "requestedAt": "2025-08-25T14:03:50.460Z",
            "remarks": null,
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "mail": "veerandra.prasath@solitontech.com",
                "role": "Project Engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "username": "Veerandra Prasath",
                    "role": "Project Engineer",
                    "gender": "male",
                    "mail": "veerandra.prasath@solitontech.com",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z"
                }
            ]
        }
    ]
}
```



**Cancel Request (Remove the particular user from the request)**

`Patch : /api/requests/{requestId}/cancel/{userId}`

Response 1:(If he is one of the member in the request)
```
{
    "success": true,
    "message": "User removed from booking members sucessfully",
    "deletedRequest": false
}
```



Response 2: (If he is the only member in the request,then the entire request is deleted)

```
{
    "success": true,
    "message": "User removed from booking members and request deleted successfully",
    "deletedRequest": true
}
```

**Cancel entire Request**  ( Delete the entire request .This button option is only displayed to the requester)

Request : `Delete : api/requests/:requestId`

Response :

```
{
    "success": true,
    "message": "Request deleted successfully"
}
```

------------

### User  Upcoming  Stays  Page

**User upcoming Booking**
 
`GET  : /api/bookings/upcoming/user/{userId}`

Note :
 * It will not include the currently staying accommodation.
 * The upcoming details are not displayed to the requester also.

Response:
```
{
    "success": true,
    "status": "approved",
    "data": [
        {
            "requestId": 17,
            "cityName": "Madurai",
            "bookingType": "individual",
            "requestedAt": "2025-08-26T07:26:55.284Z",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "mail": "veerandra.prasath@solitontech.com",
                "role": "Project Engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "username": "Veerandra Prasath",
                    "role": "Project Engineer",
                    "gender": "male",
                    "mail": "veerandra.prasath@solitontech.com",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": {
                            "id": 1,
                            "name": "Apt1"
                        },
                        "flat": {
                            "id": 1,
                            "name": "F1"
                        },
                        "room": {
                            "id": 1,
                            "name": "R1"
                        },
                        "bed": {
                            "id": 1,
                            "name": "Bed 1"
                        }
                    }
                }
            ]
        }
    ]
}
```

**Cancel User's Booking** :

`Patch: /api/bookings/:requestId/cancel/user/:userId`

Note:
1.For individual booking, the request is cancelled.
2.For team booking, the member is removed from the team booking, if he is the only member in the team, then the entire team request is cancelled.

Response :
```
{
  "success": true,
  "message": "Booking cancelled successfully"
}
```

---------

### User Booking History Page

**GET :api/bookings/history/user/{userId}**

- No filters for the user booking history

Response :
```
{
    "success": true,
    "message": "User booking history retrieved with automatic status updates",
    "data": [
        {
            "requestId": 8,
            "status": "accommodated",
            "processedAt": "2025-08-27T14:01:52.482Z",
            "remarks": "Approved for engineering offsite",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T14:01:20.661Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "accommodated",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-30T12:30:00.000Z",
                    "accommodation": {
                        "apartment": {
                            "id": 1,
                            "name": "Apt1"
                        },
                        "flat": {
                            "id": 1,
                            "name": "F1"
                        },
                        "room": {
                            "id": 1,
                            "name": "R2"
                        },
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 7,
            "status": "completed",
            "processedAt": "2025-08-27T14:00:55.858Z",
            "remarks": "Approved for engineering offsite",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T13:59:53.207Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 6,
            "status": "rejected",
            "processedAt": "2025-08-27T12:46:52.524Z",
            "remarks": "No availability for requested dates.",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T12:46:37.976Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "rejected",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 5,
            "status": "completed",
            "processedAt": "2025-08-27T12:39:02.403Z",
            "remarks": "Approved for engineering offsite",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T12:38:15.148Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 4,
            "status": "completed",
            "processedAt": "2025-08-27T12:28:29.269Z",
            "remarks": "Approved for engineering offsite",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T10:08:20.622Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 3,
            "status": "rejected",
            "processedAt": "2025-08-27T12:29:28.565Z",
            "remarks": "No availability for requested dates.",
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T10:08:09.245Z",
            "bookingType": "team",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                },
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 2,
            "status": "completed",
            "processedAt": "2025-08-27T13:53:56.701Z",
            "remarks": null,
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T09:31:59.049Z",
            "bookingType": "team",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                },
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 1,
            "status": "cancelled",
            "processedAt": "2025-08-27T09:18:52.551Z",
            "remarks": null,
            "city": {
                "id": 1,
                "name": "Madurai"
            },
            "requestedAt": "2025-08-27T09:17:34.422Z",
            "bookingType": "individual",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "cancelled",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "accommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        }
    ]
}
```



## Admin Module


### GetBooking History

**Get: /api/bookings/history?city=1&checkIn=2025-08-25T17:35:00.000Z&checkOut=2025-08-30T18:40:00.000Z&role=project engineer&search=veera**


- The response has all the user's history .Each request has it own status and every booking member of the request also have their individual status . 
- Filters applied are city ,status,checkin and checkout,search ,role of the user.
- Search by user name or email implemented.

Response:

```
{
    "success": true,
    "message": "Booking history retrieved with automatic status updates",
    "filters": {
        "city": "1",
        "role": "project engineer",
        "search": "veera",
        "checkIn": "2025-08-25T17:35:00.000Z",
        "checkOut": "2025-08-30T18:40:00.000Z"
    },
    "data": [
        {
            "requestId": 8,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "accommodated",
            "bookingType": "individual",
            "processedAt": "2025-08-27T14:01:52.482Z",
            "requestedAt": "2025-08-27T14:01:20.661Z",
            "remarks": "Approved for engineering offsite",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "accommodated",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-30T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": "Apt1",
                        "flat": "F1",
                        "room": "R2",
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 7,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "completed",
            "bookingType": "individual",
            "processedAt": "2025-08-27T14:00:55.858Z",
            "requestedAt": "2025-08-27T13:59:53.207Z",
            "remarks": "Approved for engineering offsite",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 6,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "rejected",
            "bookingType": "individual",
            "processedAt": "2025-08-27T12:46:52.524Z",
            "requestedAt": "2025-08-27T12:46:37.976Z",
            "remarks": "No availability for requested dates.",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "rejected",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 5,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "completed",
            "bookingType": "individual",
            "processedAt": "2025-08-27T12:39:02.403Z",
            "requestedAt": "2025-08-27T12:38:15.148Z",
            "remarks": "Approved for engineering offsite",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 4,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "completed",
            "bookingType": "individual",
            "processedAt": "2025-08-27T12:28:29.269Z",
            "requestedAt": "2025-08-27T10:08:20.622Z",
            "remarks": "Approved for engineering offsite",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 3,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "rejected",
            "bookingType": "team",
            "processedAt": "2025-08-27T12:29:28.565Z",
            "requestedAt": "2025-08-27T10:08:09.245Z",
            "remarks": "No availability for requested dates.",
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 2,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "completed",
            "bookingType": "team",
            "processedAt": "2025-08-27T13:53:56.701Z",
            "requestedAt": "2025-08-27T09:31:59.049Z",
            "remarks": null,
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "completed",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        },
        {
            "requestId": 1,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "cancelled",
            "bookingType": "individual",
            "processedAt": "2025-08-27T09:18:52.551Z",
            "requestedAt": "2025-08-27T09:17:34.422Z",
            "remarks": null,
            "bookingMembers": [
                {
                    "id": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "cancelled",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z",
                    "assignedAccommodation": {
                        "apartment": null,
                        "flat": null,
                        "room": null,
                        "bed": null
                    }
                }
            ]
        }
    ]
}
```

### Get All pending Requests

**GET : http://localhost:5001/api/requests**

Response:

```
{
    "success": true,
    "data": [
        {
            "requestId": 3,
            "city": "Madurai",
            "requestedBy": {
                "userId": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "pending",
            "bookingType": "team",
            "requestedAt": "2025-08-27T10:08:09.245Z",
            "bookingMembers": [
                {
                    "bookingMemberId": 4,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "gender": "male",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z"
                },
                {
                    "bookingMemberId": 5,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "gender": "male",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z"
                }
            ]
        },
        {
            "requestId": 4,
            "city": "Madurai",
            "requestedBy": {
                "userId": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@gmail.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "pending",
            "bookingType": "individual",
            "requestedAt": "2025-08-27T10:08:20.622Z",
            "bookingMembers": [
                {
                    "bookingMemberId": 6,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "gender": "male",
                    "checkIn": "2025-08-26T03:30:00.000Z",
                    "checkOut": "2025-08-26T12:30:00.000Z"
                }
            ]
        }
    ]
}
```

### Get availability by city (this is for the drop down)



**POST : /api/availability/city/{cityId}**

Body :
```JSON
{
  "DATES": [
    {
      "checkIn": "2025-08-25T14:00:00Z",
      "checkOut": "2025-08-30T10:00:00Z"
    },
    {
      "checkIn": "2023-08-10T14:00:00Z",
      "checkOut": "2023-08-15T10:00:00Z"
    }
  ]
}
```
Response:
```JSON
{
    "cityId": 1,
    "cityName": "Madurai",
    "data": [
        {
            "checkIn": "2025-08-25T14:00:00Z",
            "checkOut": "2025-08-30T10:00:00Z",
            "apartmentsStatus": [
                {
                    "id": 1,
                    "name": "Apt1",
                    "flats": [
                        {
                            "id": 1,
                            "name": "F1",
                            "isAvailable": false,
                            "gender": "male",
                            "rooms": [
                                {
                                    "id": 1,
                                    "name": "R2",
                                    "isAvailable": false,
                                    "beds": [
                                        {
                                            "id": 1,
                                            "name": "Bed 1",
                                            "isAvailable": false
                                        },
                                        {
                                            "id": 2,
                                            "name": "Bed 2",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 3,
                                            "name": "Bed 3",
                                            "isAvailable": true
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        {
            "checkIn": "2023-08-10T14:00:00Z",
            "checkOut": "2023-08-15T10:00:00Z",
            "apartmentsStatus": [
                {
                    "id": 1,
                    "name": "Apt1",
                    "flats": [
                        {
                            "id": 1,
                            "name": "F1",
                            "isAvailable": true,
                            "gender": null,
                            "rooms": [
                                {
                                    "id": 1,
                                    "name": "R2",
                                    "isAvailable": true,
                                    "beds": [
                                        {
                                            "id": 1,
                                            "name": "Bed 1",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 2,
                                            "name": "Bed 2",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 3,
                                            "name": "Bed 3",
                                            "isAvailable": true
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Approve Request :

Post : /api/requests/{requestId}/approve

Body:
```JSON
{
  "remarks": "Approved for engineering offsite",  // optional
  "allocatedAccommodation": [
    {
      "bookingMemberId": 789,
      "assignedAccommodation": {
        "apartmentId": 1,
        "flatId": 101,
        "roomId": 5,
        "bedId": 12
      }
    },
    {
      "bookingMemberId": 790,
      "assignedAccommodation": {
        "apartmentId": 1,
        "flatId": 101,
        "roomId": 5
      }
    }
  ]
}
```

Response :

```JSON
{
  "success": true,
  "message": "Request approved successfully",
  "data": {
    "requestId": 456,
    "processedAt": "2023-08-15T14:30:22Z",
    "assignedCount": 2
  }
}
```

Error response :

Invalid Request (400 Bad Request)

```json
{
  "success": false,
  "message": "Invalid booking member assignments"
}
```
Request Not Found (404 Not Found)

```json
{
  "success": false,
  "message": "Request not found"
}
```
Conflict - Already Processed (409 Conflict)

```json
{
  "success": false,
  "message": "Request already processed"
}
```
Conflict - Accommodation Taken (409 Conflict)

```json
{
  "success": false,
  "message": "Accommodation already assigned to another request"
}
```
Server Error (500 Internal Server Error)

```json
{
  "success": false,
  "message": "Internal server error while processing request",
  "error": "Database connection timeout" // Only shown in development
}
```

### Reject Request:

**Post : /api/requests/{requestId}/reject**

Body :
```JSON
{
  "remarks": "Rejected due to insufficient availability during requested dates"
}
```

Response :


```JSON
{
    "success": true,
    "message": "Request rejected successfully",
    "data": {
        "requestId": 6,
        "processedAt": "2025-08-27T12:46:52.524Z",
        "remarks": "No availability for requested dates.",
        "bookingType": "individual"
    }
}
```

### Get Occupancy 

Post:/api/occupancy?city=1&apartment=1&status= occupied/vacant

Body :
```json

{
      "checkIn": "2025-07-30T09:00:00Z",
      "checkOut": "2025-07-30T18:00:00Z"
}

```

Response 1:


If entire flat is occupied by a person ,the response will be like the below one 



```json
{
    "success": true,
    "data": {
        "period": {
            "checkIn": "2025-08-25T09:00:00Z",
            "checkOut": "2025-08-30T18:00:00Z"
        },
        "filters": {
            "city": "1",
            "apartment": "1",
            "status": "all"
        },
        "statistics": {
            "totalBeds": 6,
            "occupiedBeds": 6,
            "vacantBeds": 0,
            "occupancyRate": "100.00%"
        },
        "hierarchy": [
            {
                "id": 1,
                "name": "Madurai",
                "apartments": [
                    {
                        "id": 1,
                        "name": "Apt1",
                        "flats": [
                            {
                                "id": 1,
                                "name": "F1",
                                "rooms": [
                                    {
                                        "id": 1,
                                        "name": "R2",
                                        "beds": [
                                            {
                                                "id": 1,
                                                "name": "Bed 1",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 2,
                                                "name": "Bed 2",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 3,
                                                "name": "Bed 3",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "occupied",
                                        "occupiedBy": null
                                    },
                                    {
                                        "id": 2,
                                        "name": "R1",
                                        "beds": [
                                            {
                                                "id": 4,
                                                "name": "Bed 1",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 5,
                                                "name": "Bed 2",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 6,
                                                "name": "Bed 3",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "occupied",
                                        "occupiedBy": null
                                    }
                                ],
                                "status": "occupied",
                                "occupiedBy": {
                                    "user": {
                                        "id": 1,
                                        "name": "Veerandra Prasath",
                                        "email": "veerandra.prasath@gmail.com",
                                        "role": "project engineer",
                                        "gender": "male"
                                    },
                                    "period": {
                                        "checkIn": "2025-08-26T03:30:00.000Z",
                                        "checkOut": "2025-08-26T12:30:00.000Z"
                                    },
                                    "assignedLevel": "flat"
                                }
                            }
                        ],
                        "status": "vacant",
                        "occupiedBy": null
                    }
                ],
                "status": "vacant",
                "occupiedBy": null
            }
        ]
    }
}
```

Response 2:

If the entire room is allocated to a person means,the respone will  be like the below one 

```
{
    "success": true,
    "data": {
        "period": {
            "checkIn": "2025-08-25T09:00:00Z",
            "checkOut": "2025-08-30T18:00:00Z"
        },
        "filters": {
            "city": "1",
            "apartment": "1",
            "status": "all"
        },
        "statistics": {
            "totalBeds": 6,
            "occupiedBeds": 3,
            "vacantBeds": 3,
            "occupancyRate": "50.00%"
        },
        "hierarchy": [
            {
                "id": 1,
                "name": "Madurai",
                "apartments": [
                    {
                        "id": 1,
                        "name": "Apt1",
                        "flats": [
                            {
                                "id": 1,
                                "name": "F1",
                                "rooms": [
                                    {
                                        "id": 1,
                                        "name": "R2",
                                        "beds": [
                                            {
                                                "id": 1,
                                                "name": "Bed 1",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 2,
                                                "name": "Bed 2",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 3,
                                                "name": "Bed 3",
                                                "status": "occupied",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "occupied",
                                        "occupiedBy": {
                                            "user": {
                                                "id": 1,
                                                "name": "Veerandra Prasath",
                                                "email": "veerandra.prasath@gmail.com",
                                                "role": "project engineer",
                                                "gender": "male"
                                            },
                                            "period": {
                                                "checkIn": "2025-08-26T03:30:00.000Z",
                                                "checkOut": "2025-08-26T12:30:00.000Z"
                                            },
                                            "assignedLevel": "room"
                                        }
                                    },
                                    {
                                        "id": 2,
                                        "name": "R1",
                                        "beds": [
                                            {
                                                "id": 4,
                                                "name": "Bed 1",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 5,
                                                "name": "Bed 2",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 6,
                                                "name": "Bed 3",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "vacant",
                                        "occupiedBy": null
                                    }
                                ],
                                "status": "vacant",
                                "occupiedBy": null
                            }
                        ],
                        "status": "vacant",
                        "occupiedBy": null
                    }
                ],
                "status": "vacant",
                "occupiedBy": null
            }
        ]
    }
}
```

Response 3:

If a bed is assigned to a person means ,the response will be like the below 

```
{
    "success": true,
    "data": {
        "period": {
            "checkIn": "2025-08-25T09:00:00Z",
            "checkOut": "2025-08-30T18:00:00Z"
        },
        "filters": {
            "city": "1",
            "apartment": "1",
            "status": "all"
        },
        "statistics": {
            "totalBeds": 6,
            "occupiedBeds": 1,
            "vacantBeds": 5,
            "occupancyRate": "16.67%"
        },
        "hierarchy": [
            {
                "id": 1,
                "name": "Madurai",
                "apartments": [
                    {
                        "id": 1,
                        "name": "Apt1",
                        "flats": [
                            {
                                "id": 1,
                                "name": "F1",
                                "rooms": [
                                    {
                                        "id": 1,
                                        "name": "R2",
                                        "beds": [
                                            {
                                                "id": 1,
                                                "name": "Bed 1",
                                                "status": "occupied",
                                                "occupiedBy": {
                                                    "user": {
                                                        "id": 1,
                                                        "name": "Veerandra Prasath",
                                                        "email": "veerandra.prasath@gmail.com",
                                                        "role": "project engineer",
                                                        "gender": "male"
                                                    },
                                                    "period": {
                                                        "checkIn": "2025-08-26T03:30:00.000Z",
                                                        "checkOut": "2025-08-26T12:30:00.000Z"
                                                    },
                                                    "assignedLevel": "bed"
                                                }
                                            },
                                            {
                                                "id": 2,
                                                "name": "Bed 2",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 3,
                                                "name": "Bed 3",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "vacant",
                                        "occupiedBy": null
                                    },
                                    {
                                        "id": 2,
                                        "name": "R1",
                                        "beds": [
                                            {
                                                "id": 4,
                                                "name": "Bed 1",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 5,
                                                "name": "Bed 2",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            },
                                            {
                                                "id": 6,
                                                "name": "Bed 3",
                                                "status": "vacant",
                                                "occupiedBy": null
                                            }
                                        ],
                                        "status": "vacant",
                                        "occupiedBy": null
                                    }
                                ],
                                "status": "vacant",
                                "occupiedBy": null
                            }
                        ],
                        "status": "vacant",
                        "occupiedBy": null
                    }
                ],
                "status": "vacant",
                "occupiedBy": null
            }
        ]
    }
}
```

## Before testing all the endpoints  please login once and create atleast one City , apartment ,flat,room and bed for testing purpose.


### Admin Setup (Create City, Apartment, Flat, Room)


**Create Entire hierarchy in one request**

`Post : /api/accommodation`

Body :
```json
{
  "cityData": { "name": "New York" },
  "apartmentData": { "name": "Sky Tower", "google_map_link": "https://maps.example.com/skytower" },
  "flatData": { "name": "Floor 5" },
  "roomData": [
    { "name": "Room 501", "bedCount": 2 },
    { "name": "Room 502", "bedCount": 1 }
  ]
}
```
Response :
```json
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": 2,
        "apartmentId": 12,
        "flatId": 16,
        "rooms": [
            {
                "id": 35,
                "name": "Room 501",
                "flat_id": 16,
                "bedCount": 2,
                "beds": [
                    {
                        "id": 66,
                        "name": "Bed 1",
                        "room_id": 35
                    },
                    {
                        "id": 67,
                        "name": "Bed 2",
                        "room_id": 35
                    }
                ]
            },
            {
                "id": 36,
                "name": "Room 502",
                "flat_id": 16,
                "bedCount": 1,
                "beds": [
                    {
                        "id": 68,
                        "name": "Bed 1",
                        "room_id": 36
                    }
                ]
            }
        ],
        "totalBeds": 3
    }
}
```

**Create from the Apartment Level**

Body

```
{
  "apartmentData": { "name": "Sky Tower", "google_map_link": "https://maps.example.com/skytower","city_id": 2 },
  "flatData": { "name": "Floor 5" },
  "roomData": [
    { "name": "Room 501", "bedCount": 2 },
    { "name": "Room 502", "bedCount": 1 }
  ]
}
```
Response
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": 13,
        "flatId": 17,
        "rooms": [
            {
                "id": 37,
                "name": "Room 501",
                "flat_id": 17,
                "bedCount": 2,
                "beds": [
                    {
                        "id": 69,
                        "name": "Bed 1",
                        "room_id": 37
                    },
                    {
                        "id": 70,
                        "name": "Bed 2",
                        "room_id": 37
                    }
                ]
            },
            {
                "id": 38,
                "name": "Room 502",
                "flat_id": 17,
                "bedCount": 1,
                "beds": [
                    {
                        "id": 71,
                        "name": "Bed 1",
                        "room_id": 38
                    }
                ]
            }
        ],
        "totalBeds": 3
    }
}
```

**Create from the flat level**

Body
```
{
  
  "flatData": { "name": "Floor 5","apartment_id": 3 },
  "roomData": [
    { "name": "Room 501", "bedCount": 2 }
  ]
}
```
Response
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": null,
        "flatId": 18,
        "rooms": [
            {
                "id": 39,
                "name": "Room 501",
                "flat_id": 18,
                "bedCount": 2,
                "beds": [
                    {
                        "id": 72,
                        "name": "Bed 1",
                        "room_id": 39
                    },
                    {
                        "id": 73,
                        "name": "Bed 2",
                        "room_id": 39
                    }
                ]
            }
        ],
        "totalBeds": 2
    }
}
```

**Create from the room level**

Body
```
{
  "roomData": [
    { "name": "Room 501", "bedCount": 2 ,"flat_id":9}
  ]
}
```

Response
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": null,
        "flatId": null,
        "rooms": [
            {
                "id": 40,
                "name": "Room 501",
                "flat_id": 9,
                "bedCount": 2,
                "beds": [
                    {
                        "id": 74,
                        "name": "Bed 1",
                        "room_id": 40
                    },
                    {
                        "id": 75,
                        "name": "Bed 2",
                        "room_id": 40
                    }
                ]
            }
        ],
        "totalBeds": 2
    }
}
```

**Create city Alone**

Request:

```
{
  "cityData": { "name": "New York" }
  }
```

Response:
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": 2,
        "apartmentId": null,
        "flatId": null,
        "rooms": [],
        "totalBeds": 0
    }
}
```

**Create apartment Alone**

Request:

```
{
 "apartmentData": { "name": "Sky Tower", "google_map_link": "https://maps.example.com/skytower" ,"city_id": 2}
}
```

Response:
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": 14,
        "flatId": null,
        "rooms": [],
        "totalBeds": 0
    }
}
```

**Create flat Alone**

Request:

```
{
  "flatData": { "name": "Floor 5" ,"apartment_id": 3}
}
```

Response:
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": null,
        "flatId": 19,
        "rooms": [],
        "totalBeds": 0
    }
}
```

**Create flats and rooms Alone**

Request:

```
{  "roomData": [
    { "name": "Room 501", "bedCount": 1,"flat_id":9 }
  ]
}
```

Response:
```
{
    "success": true,
    "message": "Accommodation hierarchy created successfully",
    "data": {
        "cityId": null,
        "apartmentId": null,
        "flatId": null,
        "rooms": [
            {
                "id": 41,
                "name": "Room 501",
                "flat_id": 9,
                "bedCount": 1,
                "beds": [
                    {
                        "id": 76,
                        "name": "Bed 1",
                        "room_id": 41
                    }
                ]
            }
        ],
        "totalBeds": 1
    }
}
```



**Get all cities**

`GET : /api/cities`

Response :

```
[
    {
        "id": 2,
        "name": "New York"
    }
]
```

**Get city By Id**

`GET : /api/cities/{cityId}`

Response :
```
{
    "success": true,
    "data": {
        "id": 2,
        "name": "New York"
    }
}
```


**Create City:**

**POST : /api/cities**

Body :
```json
{
  "name": "Madurai"
}
```

Response :
```
{
    "success": true,
    "city": {
        "id": 1,
        "name": "Madurai"
    }
}
```

**Edit City**

`Put : /api/cities/{cityId}`

Body :

```
{
  "name":"City name changed"
}
```

Response :
```
{
    "success": true,
    "city": {
        "id": 1,
        "name": "City name changed"
    }
}
```


**Delete City**

`Delete : /api/cities/{cityId}`

Response :
```
{
    "success": true
}
```


**Create Apartment:**

**POST : /api/apartments**

Body :
```json
{
  "name": "Apt1",
  "cityId": 1,
  "googleMapLink": "https://..."
}

```
Response :

```
{
    "success": true,
    "apartment": {
        "id": 1,
        "name": "Apt1",
        "city_id": 1,
        "google_map_link": "https://..."
    }
}
```


**Get Apartment By City Id**

`GET : /api/apartments/city/{cityId}`

Response :
```
{
    "success": true,
    "data": {
        "city": {
            "id": 2,
            "name": "New York"
        },
        "apartments": [
            {
                "id": 3,
                "name": "Ocean View",
                "googleMapLink": null,
                "statistics": {
                    "flats": 2,
                    "rooms": 3,
                    "beds": 6
                }
            }
        ]
    }
}
```

**Get apartment By ID**

`Get : /api/apartments/{apartmentId}`

Response :
```
{
    "id": 3,
    "name": "Ocean View",
    "city_id": 2,
    "google_map_link": null
}
```

**Edit apartment details**

`Put : /api/apartments/{apartmentId}`
Body :
```
{
  "name":"Apartment name changed",
  "googleMapLink":"Opposite to maran barota kadai"
}
```

Response :

```
{
    "success": true,
    "apartment": {
        "id": 2,
        "name": "Apartment name changed",
        "google_map_link": "Opposite to maran barota kadai"
    }
}
```

**Delete Apartment**

`Delete : /api/apartments/{apartmentId}`

Response :
```
{
    "success": true
}
```

**Create Flat:**

**Post : /api/flats**

BODY :

```
{ "name": "F1", "apartment_id": 1 }
```

Response :
```
{
    "success": true,
    "flat": {
        "id": 1,
        "name": "F1",
        "apartment_id": 1
    }
}
```

**Delete Flat**

`Delete /api/flats/{flatId}`

Response :
```
{
    "success": true
}
```

**Edit Flat**

`Put : /api/flats/{flatId}`

Body :
```
{ "name": "Flat name updated" }
```

Response :
```
{
    "success": true,
    "flat": {
        "id": 10,
        "name": "Flat name updated",
        "apartment_id": 8
    }
}
```



**Create Room:**

**POST : /api/rooms**

Body :

```
{ "name": "R1", "flat_id": 1, "beds": 3 }
```

Response :
```
{
    "success": true,
    "room": {
        "id": 2,
        "name": "R1",
        "flat_id": 1,
        "beds": 3
    }
}
```


**Edit Room**
`patch : /api/rooms/{roomId}`


There are already 4 beds in this room. Now we are updating the bed count to 1. So, 3 beds will be removed automatically.
Body :
```
{ "name": "Room name updated", "beds": 1 }
```
Response :
```
{
    "success": true,
    "message": "Room updated successfully",
    "data": {
        "room": {
            "id": 39,
            "name": "Deluxe Room",
            "flat_id": 18
        },
        "previousBedCount": 4,
        "newBedCount": 1,
        "bedOperations": [
            {
                "operation": "removed",
                "bed": {
                    "id": 73,
                    "name": "Bed 2"
                }
            },
            {
                "operation": "removed",
                "bed": {
                    "id": 77,
                    "name": "Bed 3"
                }
            },
            {
                "operation": "removed",
                "bed": {
                    "id": 78,
                    "name": "Bed 4"
                }
            }
        ],
        "beds": [
            {
                "id": 72,
                "name": "Bed 1"
            }
        ]
    }
}
```

**Delete Room**

`Delete : /api/rooms/{roomId}`

Response :
```
{
    "success": true
}
```


Note : 

This room creating request will also create the number of beds mentioned in the request.
