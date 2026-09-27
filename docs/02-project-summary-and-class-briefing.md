# FixIt Project Summary

FixIt is a ServiceNow application for workplace facilities requests. It gives employees a short form to report an issue and gives Facilities staff a structured queue to triage, assign, update, and close the work.

## Build summary

- Task-extended Facilities Request table with `FIX` numbering
- Employee-facing Record Producer
- Central Facilities triage group and three specialist groups
- Requester and fulfiller roles with least-privilege access
- New-request routing and high-urgency email alert flow
- Closure email notification flow
- Manual testing for routing, urgent requests, closure, and access

## Demonstration path

1. Submit a High-urgency electrical request.
2. Show the request routed to the FixIt Facilities Team.
3. Show the Outbox confirmation and high-urgency alert previews.
4. Assign a specialist fulfiller, add work notes, and close the request.
5. Show the closure-email preview and completed flow execution.

## Honest limits

The project uses fictional data in a ServiceNow Personal Developer Instance. Email records are generated and previewed in the Outbox; external delivery is not claimed.
