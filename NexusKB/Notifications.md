---
title: "Notifications"
parent: "Application"
summary: "In-application notification center showing unread counts, a list of recent notifications, and quick navigation to related requests." 
tags: [notifications, inbox, alerts]
related:
  - file: Request-List-and-Drafts
    type: supports
  - file: Request-Detail-and-Workflow
    type: supports
sources: ["https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications", "https://main.d22r7tlcdxvmuf.amplifyapp.com/"]
version: 1
confidence: high
has_open_conflicts: false
updated_at: "2026-09-30T13:58:00Z"
---

## Sub-features
- Page header title: "Notifications" and a global header search box (placeholder: "Search requests...").
- Displays an unread summary near the top (e.g., "3 unread").
- "Mark all as read" button toggles unread state for visible notifications.
- A vertical list of notification items; each item shows an icon, a title (e.g., "Request approved", "New request assigned to you", "New comment", "Request overdue"), a short message/body (often including a REQ-##### identifier and short context), and a relative timestamp (e.g., "30 minutes ago", "1 hour ago", "yesterday").
- Notification list items are clickable and navigate to the relevant destination (typically the request detail for the referenced REQ-#####).
- The page indicates interactive affordances: clicking an unread item likely marks it read and opens the linked request.

## Business Rules
- The unread counter at top reflects the number of unread notifications displayed (e.g., "3 unread").
- "Mark all as read" marks all visible notifications as read and updates the unread counter to 0 (visual confirmation expected).
- Notifications surface the most recent events related to requests: approvals, assignments, comments, overdue alerts.
- Each notification includes a reference to a request identifier when applicable (e.g., "REQ-10471 was approved.").
- Clicking a notification navigates to the primary entity (request detail) associated with the notification.

## Entities
- Notification
  - id: (internal identifier, not shown in UI)
  - title: short headline (e.g., "Request approved").
  - message: short descriptive body (e.g., "REQ-10471 was approved.").
  - relatedRequestId: reference to REQ-##### when applicable.
  - icon: visual indicator of type (approve/comment/assign/overdue).
  - timestamp: shown as relative time (minutes/hours/days ago).
  - read: boolean state (read / unread).

## Integrations
- No external integrations were visibly named on the Notifications page; displayed items appear to be generated from in-application events tied to requests and workflow actions.

## Terminology
- "Unread": notification items that have not yet been acted upon or viewed.
- "Mark all as read": bulk action to clear unread state.
- Notification types observed: Request approved, New request assigned to you, New comment, Request overdue.

## Known Issues / Edge Cases
- The Notifications page reuses the header-level search control (placeholder: "Search requests...") that also appears on other pages; its scope (global vs. page-local) should be verified during testing.
- No explicit per-notification dismiss/delete control was observed; removal appears to be via marking read only.

## Open Conflicts
<!-- none -->

## Changelog
- v1 (2026-09-30): Added Notifications skill file from live app exploration; documents UI elements, unread counter, bulk mark-read action, notification item structure, and navigation behavior. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications]
