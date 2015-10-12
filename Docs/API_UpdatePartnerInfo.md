# Update partner ticket information 
```
PUT {{hrwcore_localhost}}/tickets/{ticketUid}/tasks/{taskid}/partnertickets/{PartnerTechnicalId}
```
* [Description](#description)
* [Parameters](#parameters)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

MyHRW stores information about the ticket in the partner system in the partner task. This information provider, by the partner, can be updated at anytime with this call.

Note that every porperty can be updated, even the technical id which enables a partner case management tool to link the MyHRW ticket to another of its own tickets.

__Make sure that you provide all the values for the properties you have initialy provided on ticket creation. Properties not provided will be defaulted to an empty string and will be erased.__

## Parameters

Parameter| Type | Description | Remarque
----------------|-------|------|-------
ticketUid| unsigned long| Ticket unique id |
taskid| integer| Task id |
partnerTechnicalId| string | Technical id of the partner ticket in the partner system |

## Body

Content-Type: application/json

| Value	| Type		| Description	| Remark	|
| ------|-----------|---------------|-----------|
| shortdescription | string | (optional) Short description of the third party ticket |-|
| description | String | (optional) Description |-|
| id | string | technical id | Used when MyHRW need to callback the partner system |
| displayid | string | (optional) Display id | If needed, partner system can provide a more userfriendly id|
| type | string | (optional) Type of the partner ticket  | Such as incident, change request, defect, ...|
| priority | string | (optional) Priority |-|
| status | string | (optional) Status |-|
| category | string | (optional) Category  |-|
| assignmentgroup | string | (optional) Assignement group |-|
| assignedto | string | (optional) Name of the agent sending the partner ticket to myHRW |-|

Example
```json
{
	"shortdescription":"Test task short descr",
	"description":"test task description",
	"id":"TKT0196",
	"displayid":"INC1068302",
	"type":"incident",
	"priority":"1 - Urgent",
	"status":"Open",
	"category":"Area: AMPS Oracle, Category: Talent Management, Subcategory: Performance Management",
	"assignmentgroup":"GTSP",
	"assignedto":"Olivier Legrand"
	}
```

## Response

return the properties as they have been set

```json
{
  "id": "TKT0196",
  "displayId": "INC1068302",
  "ticketUid": 1202591952749,
  "partnerId": 17,
  "ticketTaskId": 1,
  "type": "incident",
  "shortDescription": "Test task short descr",
  "description": "test task description",
  "category": "Area: AMPS Oracle, Category: Talent Management, Subcategory: Performance Management",
  "status": "Open",
  "assignmentGroup": "GTSP",
  "assignedTo": "Olivier Legrand",
  "priority": "2 - Urgent"
}
```

## Security group

API security group: __PartnerInteraction__

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
