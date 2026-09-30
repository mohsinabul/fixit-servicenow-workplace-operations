# FixIt recording guide

Allow about 8 minutes, including time to click and show results. Treat the timings as a guide, not a deadline.

Read only the quoted paragraphs aloud. The other lines tell you what to show or prepare. Pause between sections to change tabs or users. Keep the same new FIX number throughout the live demo.

## 1. Introduce the project

**Show:** The FixIt title and logo. About 20 seconds.

> Hi, I'm Mohsin. I built FixIt in ServiceNow App Engine Studio to help employees report workplace problems, such as electrical faults or water leaks.
>
> It keeps the request, the person responsible, and the work updates in one place, so the Facilities team can follow the issue until it is closed.

**Pause:** Open the workflow diagram.

## 2. Explain the workflow

**Show:** Point to each block as you read its paragraph. About 70 seconds.

**Employee submits → Facilities Request**

> The process starts when an employee fills in the Report a Facilities Issue form. Submitting this form creates a request record with a unique number starting with FIX. We use that number to track the request.

**Central assignment → Requester email**

> The first automatic flow assigns the request to the FixIt Facilities Team. It also creates an email to let the employee know that their request has been received.

**Urgency High? → Facilities alert**

> The flow then checks the urgency. If it is High, it creates an extra email asking the Facilities team to review the issue promptly. For a lower urgency, it skips this extra email. The request still goes to the Facilities team in either case.

**Facilities triage and fulfilment**

> The team reviews the problem and chooses the right specialist. This review is called triage. The specialist works on the issue, updates its state, and records what was done in work notes.

**Requester closure email**

> When the state changes to Closed Complete, Closed Incomplete, or Closed Skipped, a separate flow creates an email showing the employee the final status.

**Pause:** Open the support structure diagram.

## 3. Explain the Facilities teams

**Show:** The parent team, then its three specialist groups. About 35 seconds.

> The FixIt Facilities Team is the central team. Beth Anglin and Bow Ruggeri are its members, and Beth is the manager.
>
> Below it are Electrical and HVAC, Plumbing, and Cleaning and Workplace Services. These groups handle different types of facilities work.
>
> The central team has the FixIt fulfiller role, which allows staff to update requests. The specialist groups inherit this role from the parent team, so their members receive the same access. For this demo, Bow will assign the electrical request to Andrew Och.

**Pause:** Open FixIt in App Engine Studio as the administrator.

## 4. Show the table, form, roles, and flows

**Show:** Facilities Request table and its fields. Then show the Record Producer, the two roles, and the two active flow designs. Pause between these screens if needed. About 75 seconds in total.

**Table**

> This is the Facilities Request table, where the requests are stored. Each record represents one reported issue.
>
> The table extends Task, which means it uses Task as its base. This lets it use fields such as State, Assignment group, Assigned to, and Work notes. The request also captures the issue type, area, description, and urgency.

**Employee form**

> This is the employee form. In ServiceNow, it is called a Record Producer because submitting it creates a record in the Facilities Request table. It asks employees for the details needed to report a problem.

**Roles**

> These two roles control access. The FixIt user role allows employees to create and read requests. The FixIt fulfiller role also allows staff to update them. Neither role is given delete access.

**Flows**

> Both flows are active. Route Facilities Request starts when a new request is created. Notify Requester of Request Closure starts when the state changes to one of the three closed states. I'll now create a request and show the results of both flows.

**Pause:** Impersonate Allie Pumphrey and open an empty Report a Facilities Issue form. Impersonation changes the user for the current session; after changing users, reopen or refresh the relevant page.

## 5. Submit the High-urgency request

**Do while recording:** Fill in these values and click Submit. About 40 seconds.

| Field | Value |
| --- | --- |
| Issue type | Electrical |
| Area | Office |
| Description | Sparks are coming from a wall outlet near the reception desk. |
| Urgency | High |

> I'm now using the app as Allie Pumphrey, an employee. This is a sample issue for the demo: sparks coming from an outlet near reception.
>
> I'll choose Electrical, select Office, and enter the description. I'm choosing High urgency because the reported issue needs prompt attention. Now I'll submit the form.

**Pause after submitting:** Find the new record and note its FIX number. Do not change its assignment. Open it for the next section.

## 6. Check the new record

**Show:** The new FIX number, submitted details, and assignment fields. About 25 seconds.

> Here is the request we just created. The details match the employee's form, and this FIX number identifies the record.
>
> The Assignment group is already the FixIt Facilities Team. That was set by the flow. Assigned to is empty because the team has not yet selected a person to do the work.

**Pause:** End impersonation and return to the administrator. Find the Route Facilities Request execution for this record. Check its trigger record or details to confirm it is the correct run; do not rely only on it being the newest.

## 7. Check the routing flow and two emails

**Show:** The matching execution marked Complete and its action results. Then preview each matching email in the Outbox. About 60 seconds. Pause between the flow screen and Outbox if needed.

> This is the flow execution for our new request. An execution is the record of what happened when the flow ran. It is marked Complete.
>
> The update action assigned the central team, and the next action created the requester confirmation. The High-urgency condition was true, so the additional Facilities alert action also ran.

**Show the requester email.**

> This email confirms receipt to Allie. It contains the same FIX number and the issue details.

**Show the Facilities alert.**

> This second email alerts the Facilities team to the High-urgency issue and includes the description for review.
>
> These are generated email records in my ServiceNow development instance. I checked their contents here in the Outbox; delivery to an external mailbox was not tested.

**Pause:** Impersonate Bow Ruggeri. Open the same FIX record.

## 8. Assign the specialist

**Do while recording:** Set Assignment group to Electrical & HVAC, Assigned to to Andrew Och, and State to Work in Progress. Click Update. Reopen the record to confirm the saved values. About 40 seconds.

> I'm now using the app as Bow Ruggeri from the central Facilities team. Bow reviews the description and decides which team should handle it.
>
> I'll select Electrical and HVAC, then Andrew Och, who belongs to that group. I'll change the state to Work in Progress and save it.
>
> This specialist assignment is a manual decision. The automatic flow handles the first assignment to the central team.

**Pause:** End Bow's impersonation, impersonate Andrew Och, and open the same request.

## 9. Record the work and close the request

**Do while recording:** Add the sample note below, select Closed Complete, and click Update. About 40 seconds.

```text
Demo scenario: The damaged outlet was replaced and checked. The reported issue is resolved.
```

> I'm now using the app as Andrew, the assigned specialist. His fulfiller role allows him to update this request.
>
> For this sample scenario, I'll record that the outlet was replaced and checked. Work notes explain what happened so other Facilities staff can follow the work.
>
> I'll select Closed Complete and save. This means the reported work is finished, and the state change starts the closure flow.

**Pause:** Return to the administrator. Find the closure-flow execution for this request and prepare its closure email in the Outbox.

## 10. Check the closure flow and email

**Show:** The matching closure execution and its successful email action, then the matching email preview. About 45 seconds.

> The closure flow has now run for this request. It is marked Complete, and its email action succeeded.
>
> I found a permission problem during testing: the email action failed when the flow ran with the closing user's permissions. I changed this closure flow to run as System User and tested it again successfully. That change applies to the flow; it does not give Andrew an administrator role.
>
> Here is the resulting email. It shows our FIX number and the final status, Closed Complete. We have now followed the same request from submission through closure.

**Pause:** Open the Tested scenarios table in the GitHub README.

## 11. Finish with the other test results

**Show:** The test table and links to screenshots. About 30 seconds.

> The repository also contains evidence for a Medium-urgency request, where the extra Facilities alert was not created, and a Closed Incomplete request, where the email showed that final status.
>
> I also compared requester and fulfiller access. Closed Skipped is configured in the flow, but I have not tested that path separately.
>
> The blueprint, diagrams, and screenshots are all available here on GitHub. Thanks for watching.

**Stop recording.**

## Recording reminders

- Keep this guide outside the area being recorded. Read only the quoted paragraphs.
- Pause to prepare screens, change users, or wait for flows. Keep submissions, assignment changes, and closure visible in the recording.
- Say that a step succeeded only after checking its result. If something fails, resolve it before continuing the demo.
- Check the same FIX number in the record and all three emails. Use the matching record when selecting flow executions.
- The repair is a fictional demo scenario, not evidence that real electrical work took place.
- After recording, send the Loom share link so the video can be linked from the README.
