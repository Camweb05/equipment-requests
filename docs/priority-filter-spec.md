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
- Do not add a request when the employee name or equipment item is blank or contains only spaces. Show: “Employee name and equipment item are required.”
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
10. Submitting the form with a spaces-only employee name or equipment item does not add a request, keeps the current filter and count unchanged, and shows “Employee name and equipment item are required.”

## Out of Scope

- Sorting or reordering requests.
- User accounts, authentication, or database storage.
- Editing or deleting existing requests.

## Verification Results

Test method: Executed the `index.html` inline script in an isolated DOM/FormData harness; scenarios exercised the script without adding test files.

1. **Pass** — The initial filter was **All**, all eight sample requests appeared, and the count read “Showing 8 of 8 requests.”
2. **Pass** — High showed only 2 High requests, Medium only 3 Medium requests, and Low only 3 Low requests.
3. **Pass** — Selecting **All** after filtering restored all eight sample requests.
4. **Pass** — Filtering to High and returning to **All** preserved all eight original request IDs and their order.
5. **Pass** — Added a High request while High was selected; REQ-1009 appeared in the visible rows.
6. **Pass** — Added a Low request while High was selected; it stayed hidden with the specified message, then appeared under Low and **All**.
7. **Pass** — Removed all High requests from the test fixture; selecting High showed “No requests match this priority.” and “Showing 0 of 7 requests.”
8. **Pass** — Counts matched the visible request rows and full-list total for All, each priority, after additions, and with no matches.
9. **Pass** — After adding a High request under High, High remained selected and the count updated to “Showing 3 of 9 requests.”
10. **Pass** — Submitted spaces-only employee and equipment values under Medium; neither request was added, the filter and count stayed unchanged, and the required message appeared. Also checked blank employee and equipment values against the Functional Rule.
