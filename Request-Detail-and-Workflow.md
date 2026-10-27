---
title: "Request Detail and Workflow"
parent: "Application"
summary: "A request detail screen presents request metadata, type-specific information, attachments, comments, activity, workflow status, and action controls such as assignment, review, approval, rejection, and change requests."
tags: [requests, detail, workflow, approvals, comments, attachments]
related:
  - file: Request-List-and-Drafts
    type: supports
  - file: Request-Creation
    type: supports
  - file: Notifications
    type: supports
  - file: Approvals
    type: supports
sources: ["https://main.d22r7tlcdxvmuf.amplifyapp.com/requests", "https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications"]
version: 5
confidence: high
has_open_conflicts: false
updated_at: "2026-10-05T09:00:00Z"
---

## Sub-features
- Clicking a request row opens a detail route such as `/requests/REQ-10482`; the screen includes a Requests breadcrumb and a Back button.
- The detail screen's `Back` button returns to the previous page, not to a fixed page: opening REQ-10482 from a Notifications item and clicking `Back` returned to `/notifications`. The `Requests` breadcrumb links to `/requests` (the Requests list); observed on REQ-10482 and REQ-10528.
- The header displays the request identifier, title, priority, status, created date, due date, and a relative due indicator when present. REQ-10482 displayed `High`, `Pending Review`, `Created Sep 27, 2026 · Due Oct 1, 2026`, and `Due in 2 days`.
- The detail screen provides action buttons `Assign`, `Request Changes`, `Start Review`, `Approve`, and `Reject` for the observed pending-review request.
- The body includes Description, a request-type-specific information section, Attachments, Comments, Activity, Request Information, and Workflow.
- Attachments display filename, size, upload date, Preview, and Download controls. The observed request had Client_Proposal.pdf (2.4 MB, uploaded Sep 27, 2026) and Client_Requirements.docx (640 KB, uploaded Sep 28, 2026).
- Comments show author initials, author name/role, comment text, timestamp, a `Write a comment...` input, and Send. Send is disabled when the comment input is empty.
- Activity is grouped by date and records events such as commenting, starting a review, adding an attachment, manager approval, and request submission.
- Request Information displays Requester, Department, Assigned Team, Assigned To, Priority, Status, Created, Due, Request Type, SLA, and type-specific tags.
- Workflow displays ordered stages and current/completed/pending assignees or statuses.
- Draft detail screens show `Continue Editing` and `Delete Draft` instead of the action set observed on an active request. The observed DRAFT-10528 screen displayed Draft status, no description, no attachments, no comments, and an unassigned reviewer.

## Business Rules
- The Assign dialog keeps the Team fixed to the request's current team and provides a Reviewer selector. For REQ-10482, the team was Risk & Compliance and the reviewer options were Daniel Kim (selected), Lisa Nguyen, Mark Torres, and Anna Petrova.
- Assign dialog actions are Cancel and Assign; the dialog can also be closed with Close dialog.
- The Request Changes dialog requires a `Reason *`, provides `Additional comments`, and offers Cancel and Send Back.
- REQ-10482's observed workflow was Request Submitted; Manager Approval completed by James Anderson on Sep 27, 2026 at 11:20 AM; Compliance Review assigned to Daniel Kim and In progress; Risk Assessment Pending; Final Approval Pending; Completed Pending.
- The same request's Request Information showed requester Sarah Wilson, department Advisory, assigned team Risk & Compliance, assigned reviewer Daniel Kim, priority High, status Pending Review, created Sep 27, 2026, due Oct 1, 2026, request type Compliance Review, and SLA 3–6 business days.
- A draft request has a Draft status and can be continued or deleted from its detail screen; DRAFT-10528 showed due date Oct 13, 2026 and requester/current user Alex Morgan.
- In the two observed submissions, the new request's status matched its first workflow stage: Compliance Review REQ-10529 (first stage `Manager Approval`) opened with status `Pending Approval`; Security Review REQ-10528 (first stage `Security Assessment`) opened with status `Pending Review`.
- Right after submission, the Workflow shows `Request Submitted`, then the first stage labelled `Awaiting assignment`, then every later stage labelled `Pending`. REQ-10528 showed Security Assessment `Awaiting assignment`, then Risk Review, Security Approval, and Completed `Pending`; REQ-10529 showed Manager Approval `Awaiting assignment`, then Compliance Review, Risk Assessment, Final Approval, and Completed `Pending`.
- A newly submitted request shows `Assigned To` `Unassigned`, the request type's team as `Assigned Team`, the request type's `SLA`, and an `Activity` entry `<requester> Submitted request` under `TODAY` (observed: `Alex Morgan Submitted request`).

## Entities
- Request detail data includes a request identifier, title, priority, status, created/due dates, description, type-specific fields, requester, department, team, assignee, SLA, workflow stages, attachments, comments, and activity entries.
- REQ-10482 type-specific values included Business Area Advisory, Client / Engagement Meridian Capital Partners, Review Category Client Onboarding, Jurisdiction United States, Regulation / Policy Internal Policy 4.2, Risk Level High, client data Yes, regulated activity Yes, and a compliance question concerning independence and conflict-of-interest requirements for a proposed engagement structure and fee arrangement.
- REQ-10482 also displayed tags Client, Compliance, and High Risk.

## Integrations
- No external integration was named. Preview and Download are in-application controls for the displayed attachments.

## Terminology
- `Pending Review`: the status displayed for REQ-10482 while its Compliance Review stage was in progress, and for a newly submitted request whose first stage is not an approval stage (REQ-10528).
- `Pending Approval`: the status displayed for a newly submitted request whose first stage is `Manager Approval` (REQ-10529).
- `Awaiting assignment`: the label shown on a workflow's current first stage before anyone is assigned.
- `Request Changes`: an action that opens a reason/comment dialog and exposes a Send Back operation.
- `Activity`: chronological audit-style events grouped by date.
- `Workflow`: the ordered stage progression from submission through completion.

## Known Issues / Edge Cases
- The observed active request had five action buttons, but no action was submitted during exploration; resulting state transitions for Start Review, Approve, and Reject were not verified.
- The observed preview control for Client_Proposal.pdf did not produce a visible dialog or new browser tab in the session; no preview rendering behavior was confirmed.
- Direct navigation to `/requests/` with a trailing slash returned HTTP 404, whereas the application navigated successfully to `/requests` without the trailing slash.
- Requests created during a session are lost on a full page load: loading `/requests/REQ-10529` directly after it had been submitted in the same browser tab showed `We couldn't find that request.` and `Back to Requests`, while the built-in sample request REQ-10482 still loaded the same way. Move between pages with the application's own links, buttons, breadcrumbs, and sidebar - not by reloading or opening a URL - when a step needs a record created earlier in the session.
- The sample data's dates move with the current date: REQ-10482 showed `Created Sep 27, 2026 · Due Oct 1, 2026` when first documented (2026-09-29) and `Created Oct 3, 2026 · Due Oct 7, 2026` on 2026-10-05 - `Due in 2 days` both times. Treat the absolute dates recorded for sample requests in this file as examples from 2026-09-29, not fixed values; only REQ-10482's header dates were re-checked.

## Changelog
- v5 (2026-10-05): Documented that requests created in a session are lost on a full page load, and that sample-data dates are relative to the current date. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/REQ-10529, https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/REQ-10482]
- v4 (2026-10-05): Documented that the detail screen's Back button returns to the previous page while the Requests breadcrumb goes to /requests. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/REQ-10482]
- v3 (2026-10-05): Documented the status, workflow stage labels, assignment, and Activity entry of newly submitted requests (REQ-10528 Security Review, REQ-10529 Compliance Review); linked the new Approvals module. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/REQ-10528, https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/REQ-10529]
- v2 (2026-09-30): Added Notifications relationship and source; linked Request Detail to Notifications module. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/notifications]
- v1 (2026-09-29): Documented active and draft detail screens, request information, attachments, comments, activity, assignment/change dialogs, and workflow presentation. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests]
