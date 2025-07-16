# Requirements Specification Document

**Project Title:** SmartStay – Apartment Booking Web Application  
**Project Duration:** 1 Week  
**Prepared For:** Soliton Organization  
**Prepared By:** Project Team [VeerandraPrasath(PE), Shriram(PE), Vasanthakumar(LSE), Prabhakaran(PM)]  
**Date:** 16.7.2025

---

## 1. Overview

The **SmartStay** application is a web-based apartment booking system developed for internal use within **Soliton Organization**. It consists of two main modules: the **User Module** and the **Admin Module**, and will support seamless booking and management of apartment spaces for employees using **Single Sign-On (SSO)**.

---

## 2. Modules Summary

| Module        | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| Login Module  | Handles authentication and user data retrieval using SSO                    |
| User Module   | Allows employees to request or book apartments for themselves or their team |
| Admin Module  | Enables admins to manage bookings, allocate rooms, and monitor availability |

---

## 3. Login Module

### Functional Requirements:
1. **Restricted Access**:  
   Only users belonging to **Soliton Organization** should be allowed to log in to the application.

2. **SSO Integration**:  
   - Authentication must be handled via **Single Sign-On (SSO)**, following the same model as used in SIM.
   - Upon successful login, user information (e.g., name, email, job title) should be retrieved from the SSO provider.

---

## 4. User Module

### Functional Requirements:

1. **Booking Requests**:
   - Users can select **From** and **To** dates along with **Check-In** and **Check-Out** times.
   - A request is raised to the admin if rooms are available for the selected period.

2. **Team Bookings**:
   - Users can select **"Book for Team"** option.
   - They can add the **team members**  from a list.
   - A group request will be sent for room allocation.

3. **Handling Unavailability**:
   - If no rooms are available (individual or team request), show the message:  
     > “Currently No apartments available”
   - However, users can still submit the request. Admins may later handle it manually.
   - If rejected due to unavailability, the admin can add custom remarks such as:  
     > “All rooms are unavailable”  
     Users will be notified via email.

---

## 5. Admin Module

### Functional Requirements:

1. **Request Management**:
   - Admins can **accept** or **reject** booking requests.
   - Remarks can be added while accepting/rejecting the requests.

2. **Room Allocation**:
   - Admins manually allocate rooms to approved requests.
   - Only **available** rooms should be shown during allocation (booked rooms should be hidden).
   - If booking is gender-specific, only rooms with **matching gender occupants** should be shown.
   - Opposite genders **must not** be assigned to the same flat.

   #### Role-Based Allocation Logic:
   - **Managers, Above Managers, or Equivalent Roles** → Allocate entire **flat**.
   - **Seniors, Leads, or Equivalent Until Manager** → Allocate entire **room**.
   - **Juniors (Project Engineers, Above PE Until Senior)** → Allocate specific **bed** in a room.
   - Allocation UI should filter and guide the admin based on the user’s role.

3. **Team Allocation**:
   - For team bookings, the admin should select and assign rooms for each team member individually.
   - The same gender restriction applies to group assignments.
   - Role-based rules apply to each team member as per point 2 above.

4. **Email Notifications**:
   - On acceptance and allocation:  
     > “You are allocated to **[Room X]** of **[Flat Y]** in **[Apartment Z]**”
   - On rejection:  
     > “Sorry ! There is no availability of rooms”

5. **Apartment Data Import**:
   - Admins can import apartment structure via an **Excel sheet**.
   - Excel should support loading of:
     - City
     - Apartment
     - Flat
     - Room
     - Bed

6. **Manual Apartment Creation**:
   - Admins can manually add new apartments through a form.
   - The form must allow input for:
     - Apartment name
     - Number of flats
     - Flat names
     - Number of rooms in each flat
     - Number of beds in each room

7. **Live Apartment Status View**:
   - Admin can view the **current status** of all apartments, including:
     - Booked status and assigned user
     - Available rooms

8. **Export History**:
   - Admin can export the **stay history** of all users as an **Excel report**.
----

## 6. Non-Functional Requirements

- **Authentication**: Must be fully secure and compliant with Soliton Organization’s identity management.
- **Responsiveness**: The web application should be accessible on desktop and mobile devices.
- **Scalability**: The architecture must support easy scaling for additional apartments or cities.
- **Maintainability**: The system must support easy import/export and minimal manual configurations.
- **Auditability**: All booking and allocation actions should be recorded for auditing.

---
## 7. Feature Classification: Negotiable vs Non-Negotiable

### Non-Negotiable Features (Must-Have)
- SSO login for X Organization employees only
- User booking for individual and team with date/time selection
- Admin approval/rejection workflow with email notifications
- Role-based room allocation (Flat/Room/Bed based on employee designation)
- Gender-based room restrictions
- Live apartment status dashboard for admin
- Manual apartment structure creation (via form)
- History export of occupants via Excel
- "No availability" request fallback with user-visible messages

### Negotiable Features (Nice-to-Have / Can be deferred)
- UI enhancements for drag-and-drop room allocation
- Notification via Microsoft Teams (in addition to email)
- Automatic allocation recommendations
- Apartment structure import via Excel
- Role-based visual color coding in UI
