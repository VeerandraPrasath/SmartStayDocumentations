
#  Meeting Notes Summary – 24 July 2025
**Project:** Accommodation Booking Platform  
**Attendees:** Lead, Manager, Customer, Development Team

---

##  Discussion with Lead

1. **Admin-Configurable Booking Duration**  
   - **Issue:** Maximum number of booking days was hardcoded to 2 weeks.  
   - **Change:** Make this configurable by the admin so the duration can be adjusted as needed.

2. **Graceful Handling of Insufficient Resources**  
   - **Issue:** When the number of available accommodations is less than the team size, the request is currently rejected.  
   - **Change:** Instead of directly rejecting, the admin can send a *re-request* asking if the team is okay with adjusting with fewer resources or prefers to cancel.

3. **Account for Pending Approvals While Showing Availability**  
   - **Issue:** Users see more available resources than actually exist due to pending approvals.  
   - **Change:** Reduce availability count by subtracting the number of resources already in pending approval state.

---

##  Discussion with Manager

1. **Resource Availability Visualization**
   - **Individual Bookings:** Show clear availability of flats/rooms/beds.  
   - **Team Bookings:** Show individual availability per team member, even if only one bed is free.

2. **Single-Click Property Management**  
   - **Action Item:** Create a form-style, one-click interface to add or delete cities, apartments, flats, rooms, and beds to reduce admin overhead.

3. **Request Ownership and Notification**
   - **Action Item:** When someone raises a request on behalf of another user, *both the requester and the actual user* should be able to cancel the request. Notifications should be sent to both.

4. **Improve Upcoming Stays View**
   - **Change:** Show accommodation details directly on the booking card (no need for popups or hyperlinks).

5. **Booking Page UI Optimization**  
   - **Change:** Compress layout to remove scrolling but avoid clutter. Prioritize compact, intuitive design.

6. **Gender-Based Booking Rules**  
   - **Discussion:** Only females should be allowed to share accommodation with other females. Clarification needed from the customer.

---

##  Meeting with Customer

1. **No Sharing If No Availability**  
   - **Clarification:** The customer ruled out the “adjustment” suggestion from the lead. Users should only be accommodated if sufficient accommodation is available.

2. **Gender Data Collection**
   - **Issue:** SSO doesn’t provide gender details.  
   - **Solution:** Prompt users to specify gender upon their first login to support gender-based booking rules.
