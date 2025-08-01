# Smart Booking Api

## User Module

### Create Booking

**POST : http://localhost:5001/api/bookings**


Individual Booking:
```JSON
{
  "userId": 1,
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
  "userId": 1,
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
### Get Availability

Post : http://localhost:5001/api/availability/check/{cityId}

Body :
```JSON
{
  "checkInTime": "2025-07-30T09:00:00",
  "checkOutTime": "2025-07-30T18:00:00"
}
```

Response :

```
{
    "success": true,
    "availability": {
        "flat": 1,
        "room": 2,
        "bed": 8
    }
}
```
### Get User Request

Get :http://localhost:5001/api/requests/user/{userId}



Note:
   This user is either the requester or a member of the booking request.It will return all the requests made by the user or the requests in which the user is a member.

Response:
```
{
    "success": true,
    "data": [
        {
            "requestId": 2,
            "cityName": "Madurai",
            "bookingType": "individual",
            "requestedAt": "2025-07-28T07:31:19.944Z",
            "requestedUser": {
                "id": 1,
                "name": "Veerandra Prasath",
                "mail": "veerandra.prasath@solitontech.com",
                "role": "project engineer",
                "gender": "male"
            },
            "bookingMembers": [
                {
                    "userId": 2,
                    "username": "Shri Ram",
                    "role": "project engineer",
                    "gender": "male",
                    "mail": "shriram.saravanan@solitontech.com",
                    "checkIn": "2025-07-30T03:30:00.000Z",
                    "checkOut": "2025-07-30T12:30:00.000Z"
                }
            ]
        }
    ]
}
```

### Cancel Request

**DELETE /api/requests/{requestId}/cancel/{userId}**

Note:

* If requester raising the canecl request, then the request will be cancelled either it is a team or individual.
* If a member is raising the cancel request for individual type,the request is cancelled.
* If a member of the team is raising the cancel request,then he is removed from the team booking,else if he is the only member in the team ,then the entire team request is cancelled.

Response :
```
{
    "success": true,
    "message": "Individual request cancelled successfully"
}
```

### Get Upcoming Stays

GET  : /api/bookings/user/{userId}

Note :
 * It will not include the currently staying accommodation.
 * The upcoming details are not displayed to the requester also.

Response:
```
{
  "success": true,
  "data": [
    {
      "requestId": 123,
      "cityName": "Madurai",
      "bookingType": "individual",
      "requestedAt": "2023-09-01T00:00:00Z",
      "requestedUser": {
        "id": 1,
        "name": "John Doe",
        "mail": "john@example.com",
        "role": "user",
        "gender": "male"
      },
      "bookingMembers": [
        {
          "userId": 1,
          "username": "John Doe",
          "checkIn": "2023-10-15T00:00:00Z",  // Future date
          "checkOut": "2023-10-20T00:00:00Z",
          "accommodation": {
        "apartment": {
          "id": 1,
          "name": "Sunrise Apartments"
        },
        "flat": {
          "id": 5,
          "name": "Flat 101"
        },
        "room": {
          "id": 10,
          "name": "Room A"
        },
        "bed": {
          "id": 15,
          "name": "Bed 1"
        }
      }
        }
      ]
    }
  ]
}
```
### Cancel Booking:

Patch: /api/bookings/:requestId/cancel/:userId

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


### User Booking History

**GET : http://localhost:5001/api/bookings/history/user/{userId}**

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

Response:

```
{
    "success": true,
    "data": [
        {
            "requestId": 2,
            "city": "Madurai",
            "requestedBy": {
                "id": 1,
                "name": "Veerandra Prasath",
                "email": "veerandra.prasath@solitontech.com",
                "role": "project engineer",
                "gender": "male"
            },
            "status": "pending",
            "bookingType": "individual",
            "processedAt": null,
            "requestedAt": "2025-07-28T07:31:19.944Z",
            "bookingMembers": [
                {
                    "id": 2,
                    "name": "Shri Ram",
                    "email": "shriram.saravanan@solitontech.com",
                    "checkIn": "2025-07-30T03:30:00.000Z",
                    "checkOut": "2025-07-30T12:30:00.000Z",
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






