# Evidence

This folder contains the screenshots used to verify the FixIt build and its manual test scenarios. All people, email addresses, and requests shown are fictional sample data from a Personal Developer Instance.

## Build evidence

The [build folder](build/) contains 24 ordered screenshots covering the application, data model, form, Record Producer, roles, groups, routing flow, access views, and closure-notification flow.

## Test evidence

| Test | Included evidence | Result |
| --- | --- | --- |
| [TC01: Normal request](testing/TC01-normal-request/) | Request routing, flow execution, and requester confirmation | Passed |
| [TC02: High-urgency request](testing/TC02-high-urgency-request/) | Request input, routing, flow execution, requester confirmation, and facilities alert | Passed |
| [TC03: Closed Complete](testing/TC03-closed-complete/) | Work in progress, closed record, closure flow, and closure email | Passed |
| [TC04: Closed Incomplete](testing/TC04-closed-incomplete/) | Test input, closed record, and closure email | Passed |
| [TC05: Role access](testing/TC05-role-access/) | Requester read-only access and fulfiller update access | Passed |

The screenshots verify email records and previews in the ServiceNow Outbox. They do not claim delivery to external mailboxes.

Only approved and fictional evidence belongs in this repository. Credentials, customer information, and unredacted production records must not be committed.
