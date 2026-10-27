---
title: "Approvals"
parent: "Application"
summary: "The Approvals page lists requests waiting at an approval stage, with Awaiting Approval, Due Today, Approved This Week, and Rejected counters and Review, Approve, and Reject actions on each card."
tags: [approvals, workflow, queue]
related:
  - file: Request-Creation
    type: supports
  - file: Request-Detail-and-Workflow
    type: supports
sources: ["https://main.d22r7tlcdxvmuf.amplifyapp.com/approvals"]
version: 1
confidence: high
has_open_conflicts: false
updated_at: "2026-10-05T07:45:00Z"
---

## Sub-features
- `Approvals` is a link in the sidebar's Work section (route `/approvals`), visible to the default Operations Manager user, Alex Morgan. The page heading is `Approvals`.
- The top of the page shows four counters: `Awaiting Approval`, `Due Today`, `Approved This Week` (with the label `On pace`), and `Rejected`. In the observed session they showed 3, 1, 11, and 1 before any new request was submitted. These are displayed counts, not filters.
- Below the counters, each waiting request is a card showing its title, `Submitted by <name>`, priority, team, `Approval Required` with the stage it is waiting at, and a due indicator (`Due today`, `Due tomorrow`, `Due in 7 days`).
- Each card has three actions: `Review`, `Approve`, and `Reject`.

## Business Rules
- Observed: a submitted request whose first workflow stage is `Manager Approval` appeared on the Approvals page straight away - after Compliance Review REQ-10529 was submitted (first stage `Manager Approval (Operations)`), it appeared as the first card with `Approval Required` `Manager Approval` and `Due in 7 days`, and `Awaiting Approval` went from 3 to 4.
- Observed: a submitted request whose first workflow stage is `Security Assessment` did not appear on the Approvals page - after Security Review REQ-10528 was submitted (first stage `Security Assessment`), no card for it appeared and `Awaiting Approval` stayed at 3.
- The page is not limited to manager approval: the pre-existing cards were waiting at `Legal Review` (Marketing Campaign Legal Review, Marketing, Medium, due tomorrow), `Risk Review` (Cybersecurity Exception Request, Cybersecurity, Critical, due tomorrow), and `Final Approval` (Client Engagement Risk Review, Risk & Compliance, Critical, due today).

## Entities
- An approval card carries: request title, submitter name, priority, team, the approval stage it is waiting at, and a due indicator.

## Terminology
- `Approval Required`: the card label preceding the workflow stage the request is waiting at.
- `Awaiting Approval`: the counter of requests currently waiting for approval.

## Known Issues / Edge Cases
- `Review`, `Approve`, and `Reject` were not exercised, so their resulting state changes are not verified.
- Whether REQ-10528 appears here once it later reaches `Risk Review` (a stage the page showed for another request) was not observed.
- The counter values come from the demo's starting data; the observed numbers (3, 1, 11, 1) are not fixed rules.

## Changelog
- v1 (2026-10-05): Documented the Approvals page counters, cards, actions, and which newly submitted requests appear on it, from two observed submissions (REQ-10528 Security Review, REQ-10529 Compliance Review). [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/approvals]
