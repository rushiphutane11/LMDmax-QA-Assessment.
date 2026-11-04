# Task A: Test Coverage & Manual Test Cases

## Assumptions & Clarifications
Before executing the test suite, the following assumptions and pending questions were documented to distinguish known requirements from unverified logic.

**Assumptions Made:**
1. **Empty Data States:** If the backend returns an empty array or 0 values, the UI should gracefully display a standard "No Data Found" message or a 0-value chart, rather than failing to render or displaying raw code.
2. **Mobile Layout:** The application is expected to be fully responsive. On mobile viewports (e.g., iPhone 16), sidebars should collapse into a toggleable hamburger menu to prevent content blocking.
3. **Driver Counts:** The "All" user count in filters should represent actual driver entities (Active, Inactive, Suspended) and mathematically match the sum of those subgroups.

**Questions Requiring Clarification from Product/Dev:**
1. **Metric Calculations:** What are the exact backend database formulas for derived metrics like "Defects per 100 Trips" and "Violation(weekly)"? 
2. **Date Limitations:** Should the date-picker prevent users from selecting future dates, or is it expected behavior to allow future selections that simply return empty states?
3. **Data Entity Types:** Are "Broadcast Lists" intentionally included in the master "All" driver count in the Chat module, or is this a query error?

---

## Prioritized Test Cases (12-15)

| TC ID | Priority | Module | Preconditions | Title & Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-01** | High | Auth | User is logged out. | **Valid Login:** 1. Navigate to staging URL. 2. Enter valid email and password. 3. Click Login. | User is authenticated and securely redirected to the main dashboard. |
| **TC-02** | High | Auth | User is logged out. | **Invalid Credentials:** 1. Enter valid email. 2. Enter incorrect password. 3. Click Login. | System rejects login and displays a clear "Invalid credentials" error message. |
| **TC-03** | Medium | Auth | User is logged in. | **Logout & Session:** 1. Click Profile/Logout. 2. Attempt to navigate back to dashboard via browser back button. | Session terminates. User is forced to the login screen and cannot access protected routes. |
| **TC-04** | High | Navigation | User is logged in. | **Tab Switching:** 1. Navigate to Performance module. 2. Click between "Daily Highlights", "Your Scorecard", and "Leaderboard" tabs. | UI updates seamlessly to display the respective modules without page refresh errors or broken links. |
| **TC-05** | High | Dashboard | User is on Daily Highlights. | **Date-Range Selection:** 1. Click Date Picker. 2. Select "Last 7 Days". | Calendar UI highlights correct dates; dashboard API triggers and UI metrics update to reflect the new range. |
| **TC-06** | High | Dashboard | User is on Daily Highlights. | **Metric Presentation:** 1. Observe the Safety, Team, and Quality metric cards. 2. Verify numerical presence. | Cards render correctly with visible labels, numbers (e.g., Violations, Defects), and compliance status icons. |
| **TC-07** | High | Chat | User is on In-App Chat. | **Filter Math Consistency (Type):** 1. Open Filter. 2. Sum Active, Inactive, and Suspended counts. 3. Compare to "All" count. | The "All" total mathematically equals the exact sum of the valid user subgroup statuses. |
| **TC-08** | High | Chat | User is on In-App Chat. | **Filter Math Consistency (Role):** 1. Open Filter. 2. Sum individual role counts (Walker1, Helper1, etc.). 3. Compare to "All Roles". | The "All Roles" total mathematically equals the sum of the individual role counts. |
| **TC-09** | Medium | Compare | User is on Compare dashboard. | **Label & UI Consistency:** 1. Load data for Drivers. 2. Scroll to "Packages Dispatched" row. 3. Check chart legends. | Legend labels (e.g., DNR, Returned) fit cleanly within the container card border without clipping. |
| **TC-10** | Medium | Compare | User is on Compare dashboard. | **Empty-Data State (Null Selection):** 1. Ensure no drivers are selected in the left list. 2. Observe main grid. | Grid cells display a graceful "No Data Found" or "Select a Driver" state, distinguishing from broken UI blocks. |
| **TC-11** | High | Notes | User is on Daily Notes. | **Empty-Data State (Zero API Array):** 1. Select a date range with no notes. 2. Trigger API response. | UI displays "No Data Found". It does not crash or render raw HTML/JSON string tags. |
| **TC-12** | High | Dashboard | User is on Daily Highlights. | **Mobile Usability:** 1. Resize browser to iPhone 16 dimensions (or use actual device). 2. Observe layout. | Left sidebar collapses into a toggleable menu. Main content scales correctly to fit the viewport. |
| **TC-13** | Medium | Dashboard | User is logged in. | **Cross-Browser Verification:** 1. Open application in Google Chrome. 2. Open application in Firefox/Edge. | Application layout, charts, and metrics render consistently across different rendering engines. |
| **TC-14** | High | Notes | User is on Daily Notes. | **Date-Filter API Verification:** 1. Open DevTools Network. 2. Select "Last 7 Days". 3. Inspect `/notes_controller`. | The backend API response payload respects the `start` and `end` parameters sent by the frontend UI. |
| **TC-15** | Low | Tasks | User is on Tasks. | **Empty State (Tasks):** 1. Select date range with no tasks. 2. Verify "Created" and "In Progress" columns. | UI displays clean "No Task Found" placeholders in the respective columns. |
