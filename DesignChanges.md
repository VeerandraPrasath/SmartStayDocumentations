# Update Changes Design Document

## Overview
This document shows the  changes made to the Apartment Booking application's existing design in both the User Module and Admin Module.

---

## Changes in User Module

1. **Team Booking Enhancements**
   - Previously: A single check-in and check-out time was provided for the entire team.
   - Now: Each team member can select individual check-in and check-out times during booking.

2. **Availability Preview**
   - When selecting check-in and check-out time, the page  displays real-time availability of flats, rooms, and beds for each team member based on the selected dates.

3. **Request Management Page**
   - A new page has been added allowing users to:
     - View and cancel raised requests before it is processed by the admin.
     - View and cancel approved bookings.
     - View booking request history.

4. **Improved UI Layout**
   - Optimized the use of **white space** to reduce the need for scrolling and improve component visibility.

---

##  Changes in Admin Module


1. **Mandatory Rejection Remarks**
   - When rejecting a request, the remarks field is  mandatory now to provide the rejected feedback.

2. **Changed position of Occupancy Page Filter **
   - The filter option is placed above all components to clearly mentioning that it applies to all the components below it.

3. **Enhanced CSV Export**
   - When exporting occupant details, the CSV now includes a short summary:
     - Total units
     - Available units
     - Occupied units
4. **Improved Space Utilization**
   - While processing the  requests, components are now placed on both left and right sides of the page, instead of only placing them in the left.


---
## Updated Design

### User Booking View:

<img width="6162" height="3672" alt="image (3)" src="https://github.com/user-attachments/assets/fa48e777-475d-473b-918d-8ce4a6dbaff8" />

### View Pending Request
<img width="6162" height="3672" alt="image (3)" src="https://github.com/user-attachments/assets/7b5781d3-83dc-451c-844a-b490c3daa2a4" />

### View Upcoming Bookings
<img width="6162" height="3672" alt="image (4)" src="https://github.com/user-attachments/assets/470cf65b-2f11-4bde-b50c-186ceb64596a" />

### View Booking History
<img width="6162" height="3672" alt="image (5)" src="https://github.com/user-attachments/assets/c2ecbc9b-fd3e-4310-9261-c7394d7cc300" />


##  Design Conflict: CRUD Operation Flow

### Why the Conflict?
There is a request to simplify the CRUD operation by making  all entity adding (city, apartment, flat, room, bed) into a single page while adding the city.

However:
- This would lead to a cluttered interface.
- Admins want to enter a large volume of data at once.
- The page would becomes heavily scrollable and less user-friendly.

### Proposed Solution
- **Retain the existing multi-step design**:
  - Each entity (city, apartment, flat, room, bed) is added through a step by step interface.
- **Rationale**:
  - This feature is used less frequently by the admin.
  - Current design is clear, good structured, and user-friendly too.
  - Effectively utilizes page spaceS and maintains simplicity.

---
