# Smart Booking Api

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




