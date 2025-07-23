# Project Design Document: Apartment Booking Portal

## Problem Statement

Our company needs a unified portal for apartment booking based on employee roles, with dynamic configuration, analytics, and fallback mechanisms.

Currently, employees lack a structured way to book company apartments. We aim to create a centralized single-page application to manage apartment bookings by role and availability, with fallback options through admin intervention. The application should support  usage analytics, and integrate with existing portals.


## Purpose and Usage
The application allows employees to make request to book apartment.The Admin manually allocate the apartment based on the availability.Whenever the request get allocated or not ,it will be notified to the User via mail.Also admins can dynamically add apartments, assign cities, and view usage analytics.


### Booking Logic

- The **admin manually allocates** apartments/rooms/beds to the selected user(s) during approval based on the availability.

### Admin Features

- Add Cities.
- Add Apartments under cities.
- Define Flats in Apartments.
- Define Rooms inside Flats.
- Define Beds inside Rooms.
- View analytics by date range, location, and type (Apartment, Flat, Room, Bed).
- Handle user requests for manual bookings.

### Integration Points

- Microsoft Outlook SSO for authentication and user metadata (name, email, role).
- Integration with existing office portals (e.g., food and seat booking).
- Booking can be made for any selected user,for team, not just the logged-in user.

### Data Storage

**PostgreSQL Schema:**

- Users: Id, Name, Email, Role
- Cities: Id, Name
- Apartments: Id, CityId, Name
- Flats: Id, ApartmentId, Name
- Rooms: Id, FlatId, Name
- Beds: Id, RoomId, Name
- Bookings: Id, BookedByUserId, BookingForUserId, ApartmentId?, FlatId?, RoomId?, BedId?, DateFrom, DateTo
- Requests: Id, RequestedByUserId, BookingForUserId, Reason, Status, CreatedAt

### Booking Blocking Logic

- Apartment booking → Blocks all flats, rooms, and beds.
- Flat booking → Blocks all rooms and beds within the flat.
- Room booking → Blocks that room and its beds.
- Bed booking → Blocks that single bed.

### API Sample (Availability)

```json
{
  "apartments": {
    "name": "apt1",
    "isBooked": "false",
    "flats":{
    [
     {
       "name": "flat1",
       "isBooked": "false",
       "rooms": [
         {
           "name": "room1",
           "isBooked": "false",
           "beds": [
             {
               "name": "bed1",
               "isBooked": "false"
             },
             {
               "name": "bed2",
               "isBooked": "true"
             }
           ]
         },
         {
           "name": "room2",
           "isBooked": "true",
           "beds": []
          }
        ]
      }
    ]  
  }
}

```

### Benefits of Nested Tree Structure:
* Avoids redundancy of repeating apartmentId and roomId on every row.
*  Easier to map directly into nested apartment > room > cottage layout in the frontend.
* More natural fit for UI tree rendering (e.g., expandable apartment → rooms → cottages).
* Consumes less bandwidth due to hierarchical grouping



## Work flow

**Login:**

* User logs in with Microsoft Outlook SSO.
* Role is retrieved.

**Select Booking Dates:**

* User is shown a calendar to choose From and To dates.
    

**Book or Request:**

* After choosing dates,user can allow to make request

**Admin Handles Requests:**

* Admin receives notification.
* Admin assigns alternate accommodation.

Admin Analytics View:

* Admin can view usage charts (e.g., line/bar chart showing occupancy over time).
* Filters available:
* By City, Apartment, Room, Cottage
* By Date Range
* Graph shows:
* Number of bookings
* Number of users
* Peak usage times

### UI/UX Highlights

- Built with **Next.js** as an SPA.
- Calendar view to select booking dates.
- Admin dashboard with filters and analytics (Chart.js or Recharts).

### Non-Functional Requirements

- **Security**: Microsoft login, secure data access
- **Performance**: Fast booking availability filtering
- **Modularity**: Extendable admin dashboard
- **Resilience**: Manual request fallback
- **Analytics**: Usage trends, user reports

### Design Consideration

- Allows authorized booking for others and teams
- No drag-and-drop support

## Summary

**SmartStay** is a  SSO-authenticated apartment booking system that dynamically adapts to organizational hierarchy. It supports custom apartment configuration, usage analytics, and seamless integration with office systems. All bookings are manually allocated by the admin based on user requests.

---