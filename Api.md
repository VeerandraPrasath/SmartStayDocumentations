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

Response :
```
{
  "success": true,
  "data": [
    {
      "requestId": 1,
      "status": "approved",
      "processedAt": "2023-10-16T10:15:00.000Z",
      "city": {
        "id": 1,
        "name": "Madurai"
      },
      "requestedAt": "2023-10-15T09:30:00.000Z",
      "bookingType": "corporate",
      "requestedUser": {
        "id": 2,
        "name": "John Doe",
        "email": "john@example.com",
        "role": "project engineer",
        "gender": "male"
      },
      "bookingMembers": [
        {
          "userId": 1,
          "name": "Jane Smith",
          "email": "jane@example.com",
          "role": "manager",
          "gender": "female",
          "checkIn": "2023-10-20T14:00:00.000Z",
          "checkOut": "2023-10-25T11:00:00.000Z",
          "accommodation": {
            "apartment": { "id": 1, "name": "Sunrise Apartments" },
            "flat": { "id": 5, "name": "Flat 5A" },
            "room": { "id": 10, "name": "Room 101" },
            "bed": { "id": 20, "name": "Bed 1" }
          }
        }
      ]
    }
  ]
}
```



## Admin Module


### GetBooking History

**HTTP : http://localhost:5001/api/bookings/history?city=1&status=pending&checkIn=2025-07-30T02:35:00.000Z&checkOut=2025-07-30T12:40:00.000Z&role=project engineer**

- The response has all the user's history .Each request has it own status and every booking member of the request also have their individual status . 

Response:

```
{
    "success": true,
    "data": [
        {
            "requestId": 2,
            "status": "approved",
            "processedAt": null,
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
                    "status": "approved",
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
                            "name": "R2"
                        },
                        "bed": {
                            "id": 1,
                            "name": "Bed 1"
                        }
                    }
                },
                {
                    "userId": 1,
                    "name": "Veerandra Prasath",
                    "email": "veerandra.prasath@gmail.com",
                    "role": "project engineer",
                    "gender": "male",
                    "status": "approved",
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
                            "name": "R2"
                        },
                        "bed": {
                            "id": 1,
                            "name": "Bed 1"
                        }
                    }
                }
            ]
        },
        {
            "requestId": 1,
            "status": "cancelled",
            "processedAt": "2025-08-27T09:18:52.551Z",
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
### Get All pending Requests

**GET : http://localhost:5001/api/requests**

Response:

```
{
    "success": true,
    "data": [
        {
            "requestId": 2,
            "city": "Madurai",
            "requestedBy": {
                "userId": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@solitontech.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "pending",
            "bookingType": "individual",
            "requestedAt": "2025-07-28T07:31:19.944Z",
            "bookingMembers": [
                {
                    "bookingMemberId": 3,
                    "name": "Shri Ram",
                    "email": "shriram.saravanan@solitontech.com",
                    "gender": "male",
                    "checkIn": "2025-07-30T03:30:00.000Z",
                    "checkOut": "2025-07-30T12:30:00.000Z"
                }
            ]
        }
    ]
}
```
### Get availability by city (this is for the drop down)



**POST : http://localhost:5001/api/availability/city/{cityId}**

Body :
```JSON
{
  "DATES": [
    {
      "checkIn": "2023-08-01T14:00:00Z",
      "checkOut": "2023-08-05T10:00:00Z"
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
            "checkIn": "2025-08-30T09:00:00",
            "checkOut": "2025-08-30T18:00:00",
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
                                    "id": 3,
                                    "name": "R1",
                                    "isAvailable": true,
                                    "beds": [
                                        {
                                            "id": 3,
                                            "name": "Bed 1",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 4,
                                            "name": "Bed 2",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 5,
                                            "name": "Bed 3",
                                            "isAvailable": true
                                        }
                                    ]
                                }
                            ]
                        },
                        {
                            "id": 2,
                            "name": "F2",
                            "isAvailable": true,
                            "gender": null,
                            "rooms": [
                                {
                                    "id": 4,
                                    "name": "R1",
                                    "isAvailable": true,
                                    "beds": [
                                        {
                                            "id": 6,
                                            "name": "Bed 1",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 7,
                                            "name": "Bed 2",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 8,
                                            "name": "Bed 3",
                                            "isAvailable": true
                                        }
                                    ]
                                },
                                {
                                    "id": 5,
                                    "name": "R2",
                                    "isAvailable": true,
                                    "beds": [
                                        {
                                            "id": 9,
                                            "name": "Bed 1",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 10,
                                            "name": "Bed 3",
                                            "isAvailable": true
                                        },
                                        {
                                            "id": 11,
                                            "name": "Bed 2",
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
    "requestId": 456,
    "processedAt": "2023-08-15T15:22:10Z",
    "remarks": "Rejected due to insufficient availability"
  }
}
```
### Get Occupancy 

Post:/api/occupancy?city=1&apartment=1

Body :
```json

{
      "checkIn": "2025-07-30T09:00:00Z",
      "checkOut": "2025-07-30T18:00:00Z"
}

```

Response : 

```json
{
    "success": true,
    "data": {
        "period": {
            "checkInTime": "2025-07-30T09:00:00Z",
            "checkOutTime": "2025-07-30T18:00:00Z"
        },
        "filtersApplied": {
            "city": "1",
            "apartment": "1",
            "status": "all"
        },
        "stats": {
            "totalBeds": 3,
            "occupied": 2,
            "vacant": 1,
            "filteredBeds": 3
        },
        "beds": [
            {
                "bed": {
                    "id": 3,
                    "name": "Bed 1",
                    "status": "occupied",
                    "occupiedBy": {
                        "user": {
                            "id": 2,
                            "name": "Shri Ram",
                            "email": "shriram.saravanan@solitontech.com",
                            "role": "project engineer",
                            "gender": "male"
                        },
                        "period": {
                            "checkInTime": "2025-07-30T09:00:00",
                            "checkOutTime": "2025-07-30T18:00:00"
                        }
                    }
                },
                "location": {
                    "room": {
                        "id": 3,
                        "name": "R1"
                    },
                    "flat": {
                        "id": 1,
                        "name": "F1"
                    },
                    "apartment": {
                        "id": 1,
                        "name": "Apt1"
                    },
                    "city": {
                        "id": 1,
                        "name": "Madurai"
                    }
                }
            },
            {
                "bed": {
                    "id": 4,
                    "name": "Bed 2",
                    "status": "vacant",
                    "occupiedBy": null
                },
                "location": {
                    "room": {
                        "id": 3,
                        "name": "R1"
                    },
                    "flat": {
                        "id": 1,
                        "name": "F1"
                    },
                    "apartment": {
                        "id": 1,
                        "name": "Apt1"
                    },
                    "city": {
                        "id": 1,
                        "name": "Madurai"
                    }
                }
            },
            {
                "bed": {
                    "id": 6,
                    "name": "Bed 1",
                    "status": "occupied",
                    "occupiedBy": {
                        "user": {
                            "id": 3,
                            "name": "shruthi",
                            "email": "shruthi.akka@solitontech.com",
                            "role": "senior project engineer",
                            "gender": "female"
                        },
                        "period": {
                            "checkInTime": "2025-07-30T09:00:00",
                            "checkOutTime": "2025-07-30T18:00:00"
                        }
                    }
                },
                "location": {
                    "room": {
                        "id": 4,
                        "name": "R1"
                    },
                    "flat": {
                        "id": 2,
                        "name": "F2"
                    },
                    "apartment": {
                        "id": 1,
                        "name": "Apt1"
                    },
                    "city": {
                        "id": 1,
                        "name": "Madurai"
                    }
                }
            }
        ]
    }
}
```




