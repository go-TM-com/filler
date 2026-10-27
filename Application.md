# NexusFlow Knowledge Base

_Last updated: 2026-10-05T07:45:00Z_

| Skill File | Summary | Tags | Confidence |
|---|---|---|---|
| [Request List and Drafts](./Request-List-and-Drafts.md) | The Requests workspace lists operational requests and drafts with search, four filters, tabs, pagination, and row navigation into request detail. | requests, search, filtering, drafts, pagination | high |
| [Request Creation](./Request-Creation.md) | Create New Request starts by selecting one of ten request types, then collects type-specific details, attachments, priority/deadline data, and routes the request through a displayed workflow preview. | requests, creation, forms, routing, SLA | high |
| [Request Detail and Workflow](./Request-Detail-and-Workflow.md) | A request detail screen presents request metadata, type-specific information, attachments, comments, activity, workflow status, and action controls such as assignment, review, approval, rejection, and change requests. | requests, detail, workflow, approvals, comments, attachments | high |
| [Notifications](./Notifications.md) | In-application notification center showing unread counts, a list of recent notifications, and quick navigation to related requests. | notifications, inbox, alerts | high |
| [Approvals](./Approvals.md) | The Approvals page lists requests waiting at an approval stage, with Awaiting Approval, Due Today, Approved This Week, and Rejected counters and Review, Approve, and Reject actions on each card. | approvals, workflow, queue | high |

## Relationships
- Request List and Drafts --supports--> Request Creation
- Request List and Drafts --supports--> Request Detail and Workflow
- Request List and Drafts --supports--> Notifications
- Request Creation --supports--> Request List and Drafts
- Request Creation --supports--> Request Detail and Workflow
- Request Creation --supports--> Approvals
- Request Detail and Workflow --supports--> Request List and Drafts
- Request Detail and Workflow --supports--> Request Creation
- Request Detail and Workflow --supports--> Notifications
- Request Detail and Workflow --supports--> Approvals
- Notifications --supports--> Request List and Drafts
- Notifications --supports--> Request Detail and Workflow
- Approvals --supports--> Request Creation
- Approvals --supports--> Request Detail and Workflow
