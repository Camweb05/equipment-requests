# Priority Filter Specification

## Goal

Help managers focus on equipment requests that need attention by filtering the requests table by priority.

## User Need

Managers need a faster way to focus on requests that need attention. High priority is the priority that counts as needing attention.

## Functional Rules

- Add a priority dropdown above the requests table with the options **All**, **High**, **Medium**, and **Low**.
- The filter is set to **All** by default, so all requests are visible when the page loads.
- Selecting a priority filters the table to show only requests with that priority. Selecting **All** shows every request again.
- Filtering only hides rows. It never deletes or changes a request.
- A new request is always added to the full in-memory request list. It appears in the current view only when its priority matches the selected filter (or the filter is **All**).
- If a new request does not match the current filter, show: “Request added. Switch to All to see it.”
- If no requests match the selected priority, show: “No requests match this priority.”
- Keep the existing request ordering; filtering does not sort requests.
- Show a count above the table, such as “Showing 3 of 8 requests,” so managers can see how many requests need attention.

## Constraints

- No login or database.
- Preserve all existing requests in the full in-memory list while filtering and adding requests.
- Do not change the existing request table fields or ordering.

## Acceptance Criteria

1. On page load, the filter is **All** and all existing requests are visible.
2. Selecting **High**, **Medium**, or **Low** shows only requests with the selected priority.
3. Selecting **All** shows every request again.
4. Filtering does not delete or change requests; a request hidden by a filter remains in the full list and is visible again under **All** or its matching priority.
5. Adding a request whose priority matches the selected filter makes it visible in the table.
6. Adding a request whose priority does not match the selected filter keeps it in the full list, hides it in the current view, and shows “Request added. Switch to All to see it.” Selecting its priority or **All** makes it visible.
7. Selecting a priority with no matching requests shows “No requests match this priority.”
8. The count above the table reads “Showing X of Y requests,” where X equals the number of rows visible in the table and Y equals the total number of requests (for example, “Showing 8 of 8 requests” on page load).
9. After adding a new request, the filter stays on the priority the manager had selected, and the request count shown above the table updates to match the visible rows.

## Out of Scope

- Sorting or reordering requests.
- User accounts, authentication, or database storage.
- Editing or deleting existing requests.

## Verification Results

1. **Pass** — Reloaded the app; **All** was selected, all eight sample requests appeared, and the count read “Showing 8 of 8 requests.”
2. **Pass** — High showed only 2 High requests, Medium only 3 Medium requests, and Low only 3 Low requests.
3. **Pass** — Selecting **All** after filtering restored all eight requests.
4. **Pass** — Filtered to High and returned to **All**; all eight original requests remained in their original order.
5. **Pass** — Added a High request while High was selected; it appeared as REQ-1009, High remained selected, and the count updated to “Showing 3 of 9 requests.”
6. **Pass** — Added a Low request while High was selected; it stayed hidden and the specified message appeared. Selecting Low and then **All** revealed the request.
7. **Pass** — With High requests removed from a temporary test fixture, selecting High showed “No requests match this priority.” and “Showing 0 of 6 requests.”
8. **Pass** — Compared the count to visible rows and total requests in All, filtered, and post-add views; the displayed values matched.
9. **Pass** — After adding matching and nonmatching requests under High, High remained selected and the visible/total count updated correctly.
