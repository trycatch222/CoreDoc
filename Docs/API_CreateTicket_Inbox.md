# Create ticket for inbox app
```
POST /api/tickets
```
* [Description](#description)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Create a new ticket in MyHRW.
The behaviour of the create ticket API is strongly linked to the application type selected for your application key. Based on the application type, the validation and value required in the payload may vary. The examples provided in the next topics are specific to an application of the type "Inbox".

A ticket have 2 employees

*  The requester
*  The affected employee

The ticket is always created under the company of the affected employee.
If at creation you specify only requester or affected employee, the API is considering them equal.

Company of the requester and the affected employee can be different but must always be under the same organisation/customer .

Having a different requester and affected employee is useful in the scenario where a manager is requesting something for an employee. Note that the relationship between the employee and the requester is never validated by the API, the caller should verify this relationship in the HRIS system.

## Body

Content-Type: application/json

| Value						| Type		| Description								| Remarque																	|
|---------------------------|-----------|-------------------------------------------|---------------------------------------------------------------------------|
| companySkillId			| integer	| Company skill id							| 32 bits																	|
| serviceSkillId	        | integer	| Service skill id of the selected service	| 32 bits																	|
| shortDescription	  	    | string	| Short description							| max 128 characters														|
| description				| string	| Description								|																			|
| requesterId				| string	| Requester unique id						| max 40 characters															|
| employeeId				| string	| Employee unique id						| max 40 characters															|
| requesterClientSkillId	| string	| Requester company skill id				| Company of the requester when employee and requester are not the same.	|

Example 1 (Requester & Affected employee are the same)

```json
{
 "companySkillId":"26943",
 "serviceSkillId":"26914",
 "shortDescription":"Sample ticket short description description",
 "description":"Sample ticket description",
 "requesterId":"johnb"
}
```

Example 2 (Requeser & Affected employee are different

```json
{
  "companySkillId": "26943",
  "serviceSkillId": "26914",
  "shortDescription": "Sample ticket short description description",
  "description": "Sample ticket description",
  "requesterId": "johnb",
  "employeeId": "patrickg",
  "requesterClientSkillId": "26943"
}
```

## Response

Create ticket returns the created ticket in JSON.
The properties returned in the ticket's object depends on the configuration.

Two ids are really important in the returned structure

| Value		|																								|
|-----------|-----------------------------------------------------------------------------------------------|
| Id		| Id of the created ticket as displayed in the UI, it is the id used by the agent				|
| ticketUid | Unique technical identifier of the created ticket used as a parameter in all the API calls.	|

Example

```json
{
  "lastUpdate": "2014-11-18T08:54:19Z",
  "id": 1002569,
  "ticketUid": 897649167433,
  "creationDateTime": "2014-11-18T08:54:19Z",
  "currentStartTime": "2014-11-18T08:54:19Z",
  "dueDate": "2014-11-25T08:54:19Z",
  "amberDate": "2014-11-24T13:54:19Z",
  "status": "Open",
  "securityQuestions": 0,
  "flag": "FlagNoFlagged",
  "type": "External",
  "companySkillId": 26943,
  "company": {
    "id": 1791,
    "name": "YourCorp BE",
    "organisationId": 209,
    "skillId": 26943
  },
  "serviceSkillId": 26914,
  "service": {
    "id": 12117,
    "name": "Expat admin",
    "skillId": 26914,
    "serviceGroupId": 1498,
    "usePriority": true,
    "isValidForInteraction": false,
    "enableDynamicDueDate": false,
    "olrId": "",
    "dateModified": "2014-01-27T16:21:25Z"
  },
  "serviceGroup": {
    "id": 1498,
    "name": "03. Application/System Support (YCP)",
    "serviceAreaId": 1,
    "olrId": ""
  },
  "serviceArea": {
    "id": 1,
    "name": "No Service Area"
  },
  "groupingSkillId": 26732,
  "groupingSkill": {
    "id": 26732,
    "ticketUid": 897649167433,
    "name": "NGA_T1",
    "skillTypeId": 1242,
    "skillTypeName": "Usergroup (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  },
  "tierLevelSkillId": 0,
  "tierLevelSkill": {
    "id": 0,
    "ticketUid": 897649167433,
    "name": "T1",
    "skillTypeId": 2,
    "skillTypeName": "SCAgentLevel",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  },
  "prioritySkillId": 26713,
  "prioritySkill": {
    "id": 26713,
    "ticketUid": 897649167433,
    "name": "Priority 3",
    "skillTypeId": 1237,
    "skillTypeName": "Priority (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  },
  "shortDescription": "Sample ticket short description description",
  "description": "Sample ticket description",
  "solution": "",
  "employeeId": "johnb",
  "employee": {
    "id": "johnb",
    "firstName": "John",
    "lastName": "Brice",
    "company": {
      "id": 1791,
      "name": "YourCorp BE",
      "organisationId": 209,
      "organisationName": "YourCorp",
      "skillId": 26943,
      "email": "company@YCP_BE.com",
      "countryCode": "BE",
      "hrIsId": ""
    }
  },
  "requesterId": "johnb",
  "requester": {
    "id": "johnb",
    "firstName": "John",
    "lastName": "Brice",
    "company": {
      "id": 1791,
      "name": "YourCorp BE",
      "organisationId": 209,
      "organisationName": "YourCorp",
      "skillId": 26943,
      "email": "company@YCP_BE.com",
      "countryCode": "BE",
      "hrIsId": ""
    }
  },
  "creatorAgent": {
    "id": 10085,
    "firstName": "Frederic",
    "lastName": "Verjans",
    "fullName": "Frederic Verjans",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
  },
  "requesterClientSkillId": 26943,
  "unflaggableByOther": false,
  "solved": false,
  "isLinkedTicket": false,
  "skills": [{
    "id": 26717,
    "ticketUid": 897649167433,
    "name": "External",
    "skillTypeId": 1238,
    "skillTypeName": "03. Type (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26761,
    "ticketUid": 897649167433,
    "name": "Employee",
    "skillTypeId": 1245,
    "skillTypeName": "02. Requestor (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26772,
    "ticketUid": 897649167433,
    "name": "Complete",
    "skillTypeId": 1247,
    "skillTypeName": "08. Technical Phase (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 29206,
    "ticketUid": 897649167433,
    "name": "Payroll Exchange",
    "skillTypeId": 1243,
    "skillTypeName": "01. Source (YCP)",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  }],
  "isDueDateDynamicSet": false,
  "opmSkillId": 26943,
  "buttons": "TakeOwnership, Upload, AddCommunication",
  "isInteraction": false,
  "isNew": false,
  "isPending": false,
  "csatDuedate": "2014-11-25T08:54:18.995Z",
  "entityId": 8,
  "pendingType": "None",
  "trimmedDescription": "Sample ticket description",
  "reclassifiedAfterClosure": false,
  "reclassifiedInSLAAfterClosure": false,
  "reviewCompleted": false,
  "payrollGroup": "",
  "pexBodId": "",
  "initiatedBy": "ASKHR",
  "createdBy": "ASKHR"
}
```

## Security group

API security group: **TicketCreate**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
