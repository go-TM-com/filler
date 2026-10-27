---
title: "Request Creation"
parent: "Application"
summary: "Create New Request starts by selecting one of ten request types, then collects type-specific details, attachments, priority/deadline data, and routes the request through a displayed workflow preview."
tags: [requests, creation, forms, routing, SLA]
related:
  - file: Request-List-and-Drafts
    type: supports
  - file: Request-Detail-and-Workflow
    type: supports
  - file: Approvals
    type: supports
sources: ["https://main.d22r7tlcdxvmuf.amplifyapp.com/requests"]
version: 6
confidence: high
has_open_conflicts: false
updated_at: "2026-10-05T08:45:00Z"
---

## Sub-features
- `New Request` opens the `Create New Request` flow with the instruction: `Tell us what you need help with. We'll route your request to the right team.`
- The first step offers a `Search request types...` field and ten selectable request-type cards. Each card shows a description, responsible team, and typical SLA.
- The request-type selection screen shows no progress indicator. After a request type is selected, the `Request Details` step shows a three-step progress indicator: `Request Type` (marked complete), `Request Details` (current, step 2), and `Review & Submit` (step 3).
- Every request type form provides `Supporting Documents`/`Attachments` with `Click to upload files`, a priority/deadline section, `Back`, `Save Draft`, and `Continue` controls.
- The visible routing panel shows Responsible Team, reviewer count, Typical SLA, and a Workflow Preview; the workflow varies by request type.
- `Continue` with a valid form opens the `Review & Submit` step, headed `Review Your Request`. It lists the request type with an `Edit` link, the title, every entered value grouped by form section (an unanswered optional field shows `—`), `Attachments` with a file count (e.g. `0 files`), `Priority`, and `Due Date`, plus `Back`, `Save Draft`, and `Submit Request`. `Edit` returns to the `Request Details` step with every entered value kept.
- `Submit Request` shows a `Request Submitted` screen with the new `REQ-#####` id, `Your request has been submitted to <Responsible Team>.`, `Next step` naming the first workflow stage, `Expected response: <Typical SLA>`, and the buttons `Back to Requests` and `View Request`; a `Request submitted successfully.` toast also appears. Observed: REQ-10528 (Security Review) - Cybersecurity, next step Security Assessment, 3 business days; REQ-10529 (Compliance Review) - Risk & Compliance, next step Manager Approval, 3–6 business days.

## Business Rules
- Legal Review routes to Legal (3 reviewers shown in the routing panel), has a typical SLA of 3–5 business days, and previews Manager Approval → Legal Review → Final Approval → Completed.
- Compliance Review routes to Risk & Compliance (4 reviewers shown in the routing panel), has a typical SLA of 3–6 business days, and previews Request Submitted → Manager Approval (Operations) → Compliance Review (Risk & Compliance) → Risk Assessment (Risk & Compliance) → Final Approval (Risk & Compliance) → Completed.
- Technology Request routes to Technology (4 reviewers shown in the routing panel), has a typical SLA of 2–4 business days, and previews Request Submitted → Manager Approval (Operations) → IT Review (Technology) → Security Review (Cybersecurity) → Provisioning (Technology) → Completed.
- Security Review routes to Cybersecurity (3 reviewers shown in the routing panel), has a typical SLA of 3 business days, and previews Security Assessment → Risk Review → Security Approval → Completed.
- Finance Request routes to Finance (3 reviewers shown in the routing panel), has a typical SLA of 2–4 business days, and previews Finance Review → Budget Approval → Finance Approval → Completed.
- HR Request routes to HR (2 reviewers shown in the routing panel), has a typical SLA of 2–3 business days, and previews Manager Approval (Operations) → HR Review (HR) → IT / Facilities (Technology) → Completed.
- Procurement Request routes to Procurement (2 reviewers shown in the routing panel), has a typical SLA of 4–6 business days, and previews Manager Approval (Operations) → Procurement Review (Procurement) → Legal Review (Legal) → Finance Approval (Finance) → Completed.
- Tax Review routes to Tax (2 reviewers shown in the routing panel), has a typical SLA of 3–5 business days, and previews Tax Review → Tax Approval → Completed.
- Marketing Review routes to Marketing (2 reviewers shown in the routing panel), has a typical SLA of 2–3 business days, and previews Marketing Review → Legal Review (Legal) → Marketing Approval → Completed.
- Data Access Request routes to Data & Analytics (2 reviewers shown in the routing panel), has a typical SLA of 2 business days, and previews Manager Approval (Operations) → Data Governance Review (Data & Analytics) → Access Provisioning (Technology) → Completed.
- Selecting `Continue` with an empty Compliance Review form keeps the user on Request Details and displays required-field messages for Request Title, Business Area, Client / Engagement, Review Category, Jurisdiction, Describe the compliance question, and Requested Completion Date.
- Selecting `Continue` with an empty Security Review form keeps the user on Request Details and displays required-field messages for Request Title, Vendor Name, Service Description, Business Owner, and Required Completion Date - the five Security Review fields marked `*` (Destination Countries and Data Transfer Mechanism are added only while shown; see below).
- `Priority` is optional on every request type: on all ten forms it is a select with the options Low, Medium, High, and Critical, starts at `Select...`, and is not marked `*`. A Compliance Review submitted without choosing a Priority (REQ-10529) was recorded with priority `Medium`.
- Legal Review, on the Request Details step: answering `Yes` to `Does this involve personal data?` shows three follow-up fields - `Personal Data Type` (select: Employee Data, Client Data, Financial Data, Identity Data, Health Data, Other), `Estimated Records` (number), and `Retention Period` (text). Answering `No` hides them.
- Security Review, on the Request Details step: answering `Yes` to `Will personal data be processed?` shows `Personal Data Type` (select: Employee Data, Client Data, Financial Data, Identity Data, Health Data, Other) and `Estimated Records` (number). Answering `No` hides them.
- Security Review, on the Request Details step: answering `Yes` to `Will data leave the country?` shows two required follow-up fields - `Destination Countries *` (text) and `Data Transfer Mechanism *` (select: Standard Contractual Clauses, Adequacy Decision, Other). Answering `No` or `Not sure` does not show them.
- A value typed into a follow-up field is kept when the field is hidden and shown again: `Destination Countries` kept its typed value after `Will data leave the country?` was changed to `No` and back to `Yes`.
- A conditionally required field is validated only while it is visible: with `Will data leave the country?` set to `Yes` and both follow-up fields empty, `Continue` keeps the user on Request Details and shows `Destination Countries is required.` and `Data Transfer Mechanism is required.`; after changing the answer to `No`, `Continue` no longer shows those two messages.
- Required-field messages use the form `<Field> is required.` (e.g. `Request Title is required.`).

## Entities
- Common or recurring form data includes Request Title, Supporting Documents/Attachments, Priority, a deadline or required-by date, and (for several types) a Business Owner/Manager selected from a fixed employee list.
- Legal Review fields: Contract Type (Master Services Agreement, Statement of Work, Vendor Agreement, NDA, Employment Agreement, Other), Counterparty, Contract Value, Currency (USD/EUR/GBP), Expected Effective Date, Business Owner, Is this a new contract?, Does this involve personal data?, and Specific Legal Questions.
- Compliance Review fields: Business Area (Operations, Risk & Compliance, Legal, Finance, Tax, Technology, Cybersecurity, HR, Procurement, Marketing, Quality Assurance, Data & Analytics), Client / Engagement, Review Category (Regulatory Filing, Client Onboarding, Policy Exception, Internal Audit, Other), Jurisdiction (United States, United Kingdom, European Union, Singapore, Canada, Other), Regulation / Policy (an optional, editable, initially empty text field with the placeholder `e.g. GDPR, SOX, Internal Policy 4.2`; the `Risk & Compliance` text shown just below it is the heading of the next form section, not the field's value), Risk Level (Low, Medium, High, Critical), `Does this involve client data?` (Yes/No), `Does this involve a regulated activity?` (Yes/No), Describe the compliance question, and Requested Completion Date.
- Technology Request fields: Request Category (Software Access, Hardware, New Application, System Change, Technical Support, Infrastructure), Software / Service, Request Type (New Access, Modify Access, Remove Access), Business Justification, Number of Users, Environment (Production, Staging, Development), Access Level (Standard, Elevated, Admin), Manager Approval, and Required By.
- Security Review fields: Vendor Name, Service Description, Vendor Website, Security Review Type (New Vendor, Renewal, Change), Data Classification (Public, Internal, Confidential, Highly Confidential), `Will the vendor access company data?` (Yes/No), `Will personal data be processed?` (Yes/No), `Will data leave the country?` (Yes/No/Not sure), Authentication Method (SSO, Username/Password, API Key, MFA), Business Owner, Security Documentation, attachments, and Required Completion Date.
- Finance Request fields: Request Category (Billing Adjustment, Budget Change, Invoice Correction, Revenue Recognition, Other), Client, Project / Engagement, Current Amount, Requested Amount, Currency (USD/EUR/GBP), Reason for Adjustment, Revenue Impact (None, Low, Medium, High), Effective Date, Business Owner, Supporting Documents, and Due Date.
- HR Request fields: Request Category (New Hire Onboarding, Transfer, Promotion, Termination, Leave of Absence, Other), Employee Name, Employee ID, Department, Job Title, Manager, Start Date, Location (New York, London, Singapore, Remote), Employment Type (Full-time, Part-time, Contractor, Intern), Equipment Required (Laptop, Monitor, Phone, Badge), Systems Required (Email, VPN, CRM, ERP), and Additional Information.
- Procurement Request fields: Request Category (New Vendor, Renewal, Hardware Purchase, Software Purchase, Services), Vendor Name, Estimated Annual Cost, Currency (USD/EUR/GBP), Purchase Type (One-time, Recurring), Department, Business Justification, Budget Owner, Budget Available? (Yes/No), Contract Required? (Yes/No), Supporting Documents, and Target Purchase Date.
- Tax Review fields: Client, Engagement, Jurisdiction (United States, United Kingdom, European Union, Singapore, Canada, Other), Transaction Type (Acquisition, Disposal, Restructuring, Cross-border, Other), Transaction Amount, Tax Type (Corporate Tax, VAT, GST, Sales Tax, Withholding Tax, Transfer Pricing, Other), Tax Question, Expected Transaction Date, Business Owner, attachments, and Due Date.
- Marketing Review fields: Campaign Name, Campaign Type (Digital, Print, Social Media, Event, Email, Other), Target Audience, Markets, Launch Date, Marketing Channel (Website, Social Media, Email, TV, Print, Events), External Agency, `Contains Client Information?` (Yes/No), `Legal Review Required?` (Yes/No), Description, Creative Assets, and Due Date.
- Data Access Request fields: System / Dataset, Access Type (Read, Write, Admin, Export, API), User / Employee, Department, Business Justification, Data Classification (Public, Internal, Confidential, Highly Confidential), Access Duration (30 days, 90 days, 6 months, 1 year, Permanent), Start Date, End Date, Manager, Additional Information, and Priority.

## Integrations
- No external integration was named in the creation flow. File upload is presented as an in-application attachment control.

## Terminology
- `Responsible Team`: the team selected by the request type routing configuration.
- `Typical SLA`: the displayed business-day range or duration for the selected request type.
- `Save Draft`: the visible action for preserving a partially completed request.
- `Review & Submit`: the third step shown in the progress indicator, where the user reviews the request and submits it.

## Known Issues / Edge Cases
- The available form fields differ substantially by request type; no single universal detail schema was observed.
- Answer-triggered follow-up fields were observed only on Legal Review and Security Review. Toggling every Yes/No answer and select option on the other eight request-type forms showed no additional labelled fields.
- The employee selector exposes many named employees, including Alex Morgan, James Anderson, Daniel Kim, Lisa Nguyen, Mark Torres, Anna Petrova, Emily Carter, Thomas Reed, Natalie Brooks, Priya Nair, Oliver Scott, Grace Lee, Henry Adams, Chloe Baker, Michael Chen, Ryan Patel, Jordan Walsh, Ana Silva, David Miller, Elena Popov, Marcus Hall, Rachel Thompson, Victor Adeyemi, Sophie Martin, Carlos Ibanez, Olivia Jones, Ben Foster, Nina Kowalski, Samuel Osei, Fiona Clarke, and Sarah Wilson.

## Changelog
- v6 (2026-10-05): Replaced paraphrased Yes/No question names in the Compliance Review, Security Review, and Marketing Review field lists with the exact labels shown on the forms. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/new]
- v5 (2026-10-05): Added the Security Review required fields and their empty-form messages, and the Priority options (Low, Medium, High, Critical), its optional status on all ten forms, and the Medium priority recorded when it was left unset. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/new]
- v4 (2026-10-05): Added the reviewer count shown for each request type, the Review Your Request step and its Edit behaviour, and the Request Submitted confirmation from two observed submissions; replaced the note that no submission had been performed; linked the new Approvals module. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/new]
- v3 (2026-10-05): Corrected Regulation / Policy (an optional editable text field, not a static `Risk & Compliance` value - that text is the next section's heading) and removed the edge case built on that misreading. Documented the answer-triggered follow-up fields on Legal Review and Security Review, value retention on hide/show, visibility-dependent required validation, and the required-message format. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/new]
- v2 (2026-10-05): Clarified that the three-step progress indicator appears only on the Request Details step, after a request type is selected - not on the request-type selection screen. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests/new]
- v1 (2026-09-29): Documented request-type selection, type-specific forms, validation, routing teams, SLAs, and workflow previews. [sources: https://main.d22r7tlcdxvmuf.amplifyapp.com/requests]
