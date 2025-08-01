# Requirements Specification Document

**Project Title:** SmartStay – Apartment Booking Web Application  
**Prepared For:** Soliton Organization  
**Prepared By:** Project Team [VeerandraPrasath(PE), Shriram(PE), Vasanthakumar(LSE), Prabhakaran(PM)]  
**Date:** 16.7.2025

---

## 1. Overview

The **SmartStay** application is a web based apartment booking system developed for Internal use within Soliton Organization.This application contains two major module.User module and Admin module.The user module .These modules helps to book apartments seamlessly using Single Sign-On

---

## 2. Modules Summary

| Module        | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| Login Module  | Handles authentication and get data of user using SSO                    |
| User Module   | Allows employees to make request to book apartments for individual as well as for team  |
| Admin Module  | Used to handle the raised request,allocate apartments ,check availability and export history |

---

## 3. Login Module

### Functional Requirements:
1. **Restricted Access**:  
  Only user belongs to Soliton Organization can access the application.

2. **SSO Integration**:  
   - Authentication must be done using Single Sign-On(SSO) with Soliton Organization’s identity management system same as the SIM.
   - On Successful login,the details of the User are fetched from the SSO provider and store in the database.

---

## 4. User Module

### Functional Requirements:

1. **Booking Requests**:
   - User can select the **From** date and **To** date along with the **Checkin** and **Checkout** time.
   - User can only able to book room maximum of 14 days.
   - Request can be made for **individual** or **team** bookings.
   - Request can only made if there is an available room for the selected date and time.

2. **Team Bookings**:
   - Users can select **"Book for Team"** option.
   - They can add the **team members**  from a list.
   - A group request will be sent for room allocation.

3. **Handling Unavailability**:
   - If no rooms are available (individual or team request), send mail to the requested user with message:  
     > “Currently No apartments available”
   - However,there is no availability of rooms, users can still able to make a request. Admins will handle it manually.
   - If the request is rejected due to unavailability, the admin can add custom remarks in the mail such as:  
     > “All rooms are unavailable”  

---

## 5. Admin Module

### Functional Requirements:

1. **Request Management**:
   - Admins can accept or reject booking requests.
   - Remarks can be added during accepting/rejecting the requests.

2. **Room Allocation**:
   - Admin will manually allocate the rooms to approved requests.
   - Only available rooms should be shown while allocating (booked rooms should be hidden).
   - All the booking request are gender-specific, only rooms with **matching gender occupants** should be shown.
   - Opposite genders must not be assigned to the same flat.

   #### Role-Based Allocation Logic:
   - Managers, Above Managers, or Equivalent Roles → Allocate entire flat.
   - Seniors, Leads, or Equivalent Until Manager → Allocate entire room.
   - Juniors (Project Engineers, Above PE Until Senior) → Allocate specific bed in a room.

3. **Team Allocation**:
   - For team bookings, the admin should select and assign rooms for each team member individually.
   - The same gender restriction applies to group assignments also.
   - Role-based room allocation rules are applied to each team member.

4. **Email Notifications**:
   - Once the request is accepted and room is allocated:  
     > “You are allocated to **[Room X]** of **[Flat Y]** in **[Apartment Z]**”
   - Once the request is rejected:  
     > “Sorry ! There is no availability of rooms”

5. **Manual Apartment Creation**:
   - Admins can manually add new apartments.
   - The details required to add new apartment are:
     - Apartment name
     - Number of flats
     - Flat names
     - Number of rooms in each flat
     - Number of beds in each room

7. **Live Apartment Status View**:
   - Admin can view the current status of all the apartments, including:
     - Unavailable rooms with assigned user
     - Available rooms

8. **Export History**:
   - Admin can export the stay history as  Excel report.
----

## 6. Non-Functional Requirements

- **Authentication**: Must be fully secure and compatible with Soliton Organization’s identity management.
- **Responsiveness**: The web application should be accessible through desktop and also in mobile devices.
- **Scalability**: The architecture must support scaling for adding apartments or cities in the future.
- **Auditability**: All booking and allocation items should be logged.

---
## 7. Feature Classification: Negotiable vs Non-Negotiable

### Non-Negotiable Features (Must-Have)
- SSO login for Soliton Organization employees only
- User booking for individual and team with date/time selection
- Admin approval/rejection workflow with email notifications
- Gender-based room restrictions
- Live apartment status dashboard for admin
- Manual apartment structure creation 
- History export of occupants via Excel

### Negotiable Features (Nice-to-Have / Can be deferred)
- UI enhancements for drag-and-drop room allocation
- Notification via Microsoft Teams (in addition to email)
- Automatic allocation recommendations
- Apartment structure import via Excel
- Role-based visual color coding in UI

----
