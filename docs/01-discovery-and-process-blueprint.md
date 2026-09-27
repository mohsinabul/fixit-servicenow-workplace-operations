# FixIt Process Blueprint

## Purpose

I built FixIt to provide one controlled way to report, route, work, and close workplace facilities issues. It replaces informal requests through email, phone calls, and conversations with a trackable ServiceNow record. I kept the first version focused on the core request process, so I could configure and test it end to end. I didn't add integrations that weren't needed for the first version.

## Users

| User | What they can do |
| --- | --- |
| Employee requester | Submit a request and read it. |
| Facilities fulfiller | Triage, assign, update, add work notes, and close a request. |
| Facilities team lead | Oversees the central team, assignments, and work in progress. |

## Data model

**Facilities Request** is a custom table that extends **Task**. It uses Task capabilities such as assignment group, assigned to, state, work notes, and a generated `FIX` number.

Custom request details are:

- Request Type
- Area
- Description
- Urgency

## Facilities support structure

Every new request starts with the **FixIt Facilities Team**. After triage, it can be assigned to a specialist group when needed.

![FixIt facilities support structure](../assets/fixit-facilities-support-structure-white.png)

| Group | Focus |
| --- | --- |
| FixIt Facilities Team | Central intake, triage, and general maintenance. |
| Electrical & HVAC | Electrical faults, heating, cooling, and ventilation. |
| Plumbing | Leaks, drainage, restrooms, and water-related issues. |
| Cleaning & Workplace Services | Cleaning, furniture, and common-area requests. |

## Process

1. An employee submits **Report a Facilities Issue**.
2. A Facilities Request is created with a unique `FIX` number.
3. The **Route Facilities Request** flow assigns it to the FixIt Facilities Team and sends the requester a confirmation.
4. If urgency is High, the flow sends an additional alert to the FixIt Facilities inbox.
5. The central team reviews the request and assigns a specialist group or fulfiller when needed.
6. The fulfiller records work notes and updates the state.
7. When the request changes to Closed Complete, Closed Incomplete, or Closed Skipped, the **Notify Requester of Request Closure** flow sends the final-status email.

![FixIt workflow](../assets/fixit-workflow-diagram.svg)

## Automation

| Flow | Trigger | Actions |
| --- | --- | --- |
| Route Facilities Request | Facilities Request created | Assign central team, email requester, alert facilities inbox for High urgency. |
| Notify Requester of Request Closure | State changes to a closed state | Email the requester with request details and final status. |

Both flows are active. The closure flow runs as **System User**, so it can create an email record when a fulfiller closes a request. This setting fixed the earlier email-create error.

## Access model

| Role | Create | Read | Update | Delete |
| --- | --- | --- | --- | --- |
| `fixit_user` | Yes | Yes | No | No |
| `fixit_fulfiller` | Yes | Yes | Yes | No |

The FixIt Facilities Team has the fulfiller role. I used the parent group so Electrical & HVAC, Plumbing, and Cleaning & Workplace Services inherit that access. This keeps the group setup simple and makes the access model easier to review.

## Verification completed

- Normal request routing and requester notification
- High-urgency requester notification and facilities alert
- Closure email for Closed Complete
- Closure email for Closed Incomplete
- Requester read-only access and fulfiller update access

## Limits

- I verified Outbox records and email previews in the PDI. External delivery was not tested.
- Closed Skipped is configured in the closure flow but was not separately tested.
- Specialist assignment is a human triage decision after central intake.
