---
title: "Request List and Drafts"
parent: "Application"
summary: "The Requests workspace lists operational requests and drafts with search, four filters, tabs, pagination, and row navigation into request detail."
tags: [requests, search, filtering, drafts, pagination]
related:
  - file: Request-Creation
    type: supports
  - file: Request-Detail-and-Workflow
    type: supports
  - file: Notifications
    type: supports
sources: ["https://main.d22r7tlcdxvmuf.amplifyapp.com/requests", "https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications"]
version: 2
confidence: high
has_open_conflicts: false
updated_at: "2026-09-30T13:58:30Z"
---

## Sub-features
- The Requests page has two tabs: `Requests` and `Drafts`.
- The main Requests tab displays a table with the columns Request, Type, Assigned Team, Priority, Status, Due Date, Updated, and Requester.
- The observed Requests dataset contains 34 items, displayed 10 per page across four pages; page 1 shows `Showing 1–10 of 34`, page 2 `11–20`, page 3 `21–30`, and page 4 `31–34`.
- Each request row is clickable and opens a route-specific request detail screen such as `/requests/REQ-10482`.
- The Drafts tab displays saved drafts separately; the observed dataset contains two drafts, `DRAFT-10528` and `DRAFT-10491`, with `Showing 1–2 of 2`.
- Pagination provides numbered page buttons, Previous page, Next page, and an ellipsis when not all page numbers are shown. Previous page is disabled on the first page.
- The table search field is labeled `Search...`. Searching `Client` reduced the visible result set to five matching requests and displayed a `Clear all` control.

## Business Rules
- The list can be filtered independently by Status, Request Type, Assigned Team, and Priority.
- The status filter options are All Statuses, Draft, Submitted, Pending Review, In Progress, Changes Requested, Pending Approval, Approved, Rejected, Completed, and Cancelled.
- The request-type filter options are All Request Types, Legal Review, Compliance Review, Technology Request, Security Review, Finance Request, HR Request, Procurement Request, Tax Review, Marketing Review, and Data Access Request.
- The team filter options are All Teams, Risk & Compliance, Legal, Finance, Tax, Technology, Cybersecurity, HR, Procurement, Marketing, Operations, Quality Assurance, and Data & Analytics.
- The priority filter options are All Priorities, Low, Medium, High, and Critical.
- Filters and search are applied to the displayed list; combining `Client` search with `Pending Review` status produced four results: REQ-10482, REQ-10507, REQ-10503, and REQ-10509.
- Draft rows have status `Draft` and are owned by the current user shown in the application shell, Alex Morgan.

## Entities
- A request list row includes an identifier, title, request type, assigned team, priority, status, due date, last-updated value, and requester initials/name.
- Observed request identifiers include REQ-10482 through REQ-10527, with gaps in the displayed sequence; draft identifiers use the `DRAFT-` prefix.
- Request types represented in the list include Legal Review, Compliance Review, Technology Request, Security Review, Finance Request, HR Request, Procurement Request, Tax Review, Marketing Review, and Data Access Request.

## Integrations
- None were named or visibly integrated on the Requests list or Drafts tab.

## Terminology
- `Requests`: the tab for submitted or active request records.
- `Drafts`: the tab for saved but not submitted request records.
- `All Statuses`, `All Request Types`, `All Teams`, and `All Priorities`: default filter selections.

## Known Issues / Edge Cases
- Navigating directly to `/requests/` with a trailing slash returned HTTP 404 in the observed session, while navigating from the application shell to `/requests` rendered the page.
- The search field on the page header is labeled `Search requests`, while the table search field is labeled `Search...`; they are distinct visible controls.

## Changelog
- v2 (2026-09-30): Added Notifications relationship and source; linked Requests list to Notifications module. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications]
- v1 (2026-09-29): Documented the Requests/Drafts workspace, table fields, filters, search, pagination, observed records, and navigation behavior. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests]
