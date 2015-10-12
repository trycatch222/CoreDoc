# Create ticket
```
POST /api/tickets
```
* [Description](#description)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Create a new ticket in MyHRW.
The behaviour of the create ticket API is strongly linked to the application type selected for your application key. Based on the application type, the validation and value required in the payload may vary. The examples provided in the next topics are specific to an application of the type "Partner".

A ticket has 2 employees

*  The requester
*  The affected employee

The ticket is always created in the company of the affected employee.
If at ticket creation you only specify requester or affected employee, the API is considering them as being equal.

The company of the requester and the affected employee can be different but must always be under the same organisation/customer .

Having a different requester and affected employee is useful in the scenario where a manager is requesting something for an employee. Note that the relationship between the employee and the requester is never validated by the API, the caller should verify this relationship in the HRIS system.

At ticket creation, the API also offers you the possibility to directly attach one or more files to the ticket.
The binary should be encoded as a Base64 string. ([see RFC 2045](http://tools.ietf.org/html/rfc2045)).


## Body

Content-Type: application/json

| Value					| Type			| Description											| Remark																|
|-----------------------|---------------|-------------------------------------------------------|-----------------------------------------------------------------------|
|companySkillId			| integer		| Company skill id										| 32 bits																|
|serviceSkillId			| integer		| Service skill id of the selected service				| 32 bits																|
|shortDescription		| string		| Short description										| max 128 characters													|
|description            | string		| Description											|	-																	|
|requesterId			| string		| Requester unique id									| max 40 characters														|
|employeeId				| string		| Employee unique id									| max 40 characters														|
|requesterClientSkillId | string		| Requester company skill id							| Company of the requester when employee and requester are not the same.|
|Items					| collection	| Collection of file to add to the ticket				|	-																	|
|skills					| collection	| Collection of skill object like the source, priority	|	-																	|

Item object details

| Value				| Type			| Description					| Remark	|
|-------------------|---------------|-------------------------------|-----------|
| type				| string		| Must be equal to "File"		| -  		|
| description		| string		| Description of the file item	| - 		|
| privacySkillId	| int			| Privacy skill id				| -  		|
| file				| File object	|								| -  		|

File object details

| Value			| Type		| Description								| Remark				|
|---------------|-----------|-------------------------------------------|-----------------------|
| fileName		| string	| Nameof									| max 2000 charaters	| 
| binaryData	| string	| file binaries encoded in a base64 string  |	-					|

Skill object details

| Value	| Type		| Description	| Remark	|
| ------|-----------|---------------|-----------|
| id	| integer	|skill id		|	-		|

Example (new ticket with 1 file attached to it)

```json
{
    "companySkillId":26943,
    "serviceSkillId":"26810",
    "shortDescription":"test",
    "description":"dfsdf",
    "employeeId":"patrickg",
    "requesterId":"patrickg",
    "requesterClientSkillId":26943,
    "skills":[{"id":"26749"}],
    "items":[{
		"type" : "File",
		"description":"test item",
		"privacySkillId":"",
		"File": {
			"filename" : "clock.txt",
			"binaryData":"ZnJpZGF5IDEwaDMwIHRvIDEyaA0KDQpTYXR1cmRheSAwMGggdG8gMmgzMCAm\nIDEwaCB0byAxNWggJiAyMmggdG8gMjNoMzANClN1bmRheSAxMGggdG8gMTNo\nDQoNCg0KMWgzMA0KMmgzMA0KNWgNCjFoMzANCjNoDQoNCjEzaDMw\n"
		}
	}]
}
```

## Response

Create ticket returns the created ticket in JSON.
The properties returned in the ticket's object depends on the configuration.

Two id's are really important in the returned structure

| Value		| Description																					|
|-----------|-----------------------------------------------------------------------------------------------|
| Id		| Id of the created ticket as displayed in the UI, it is the id used by the agent				|
| ticketUid	| Unique technical identifier of the created ticket used as a parameter in all the API calls.	|

Example

```json
{
  "lastUpdate": "0001-01-01T00:00:00Z",
  "id": 1109416,
  "ticketUid": 897649274280,
  "creationDateTime": "2015-05-07T12:25:35.0434735Z",
  "currentStartTime": "2015-05-07T12:25:35.0434735Z",
  "dueDate": "2015-05-08T08:25:35.043Z",
  "amberDate": "2015-05-07T13:25:36Z",
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
  "serviceSkillId": 26810,
  "service": {
    "id": 12013,
    "name": "Ticket created",
    "skillId": 26810,
    "serviceGroupId": 1489,
    "usePriority": false,
    "isValidForInteraction": true,
    "enableDynamicDueDate": false,
    "olrId": "",
    "dateModified": "2014-03-19T05:29:55Z"
  },
  "serviceGroup": {
    "id": 1489,
    "name": "Service Center",
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
    "ticketUid": 897649274280,
    "name": "NGA_T1",
    "skillTypeId": 1242,
    "skillTypeName": "Usergroup (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  },
  "shortDescription": "test",
  "description": "dfsdf",
  "employeeId": "patrickg",
  "employee": {
    "id": "patrickg",
    "firstName": "Patrick",
    "lastName": "Grey",
    "company": {
      "id": 1791,
      "name": "YourCorp BE",
      "organisationId": 209,
      "organisationName": "YourCorp",
      "skillId": 26943,
      "email": "company@YCP_BE.com",
      "countryCode": "US",
      "hrIsId": "BE"
    },
    "backendType": "Sap"
  },
  "requesterId": "patrickg",
  "requester": {
    "id": "patrickg",
    "firstName": "Patrick",
    "lastName": "Grey",
    "company": {
      "id": 1791,
      "name": "YourCorp BE",
      "organisationId": 209,
      "organisationName": "YourCorp",
      "skillId": 26943,
      "email": "company@YCP_BE.com",
      "countryCode": "US",
      "hrIsId": "BE"
    },
    "backendType": "Sap"
  },
  "currentAgent": {
    "id": 10085,
    "firstName": "Frederic",
    "lastName": "Verjans",
    "fullName": "Frederic Verjans",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None",
    "enableBulkFtr": false
  },
  "creatorAgent": {
    "id": 10085,
    "firstName": "Frederic",
    "lastName": "Verjans",
    "fullName": "Frederic Verjans",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None",
    "enableBulkFtr": false
  },
  "requesterClientSkillId": 26943,
  "unflaggableByOther": false,
  "solved": false,
  "isLinkedTicket": false,
  "skills": [{
    "id": 26943,
    "ticketUid": 897649274280,
    "name": "YourCorp BE",
    "skillTypeId": 1,
    "skillTypeName": "Company",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  }, {
    "id": 26810,
    "ticketUid": 897649274280,
    "name": "Ticket created",
    "skillTypeId": 0,
    "skillTypeName": "Service",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  }, {
    "id": 0,
    "ticketUid": 897649274280,
    "name": "T1",
    "skillTypeId": 2,
    "skillTypeName": "SCAgentLevel",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  }, {
    "id": 26732,
    "ticketUid": 897649274280,
    "name": "NGA_T1",
    "skillTypeId": 1242,
    "skillTypeName": "Usergroup (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": true
  }, {
    "id": 26749,
    "ticketUid": 897649274280,
    "name": "Call",
    "skillTypeId": 1243,
    "skillTypeName": "Source",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26717,
    "ticketUid": 897649274280,
    "name": "External",
    "skillTypeId": 1238,
    "skillTypeName": "Type",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26723,
    "ticketUid": 897649274280,
    "name": "No",
    "skillTypeId": 1239,
    "skillTypeName": "Payroll Impact",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26725,
    "ticketUid": 897649274280,
    "name": "No",
    "skillTypeId": 1240,
    "skillTypeName": "SLA Impact",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26727,
    "ticketUid": 897649274280,
    "name": "No",
    "skillTypeId": 1241,
    "skillTypeName": "Invoicing",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26761,
    "ticketUid": 897649274280,
    "name": "Employee",
    "skillTypeId": 1245,
    "skillTypeName": "Requestor",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26772,
    "ticketUid": 897649274280,
    "name": "Complete",
    "skillTypeId": 1247,
    "skillTypeName": "Technical Phase",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 27551,
    "ticketUid": 897649274280,
    "name": "Accepted Close Note",
    "skillTypeId": 1258,
    "skillTypeName": "Close Note Type",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 29287,
    "ticketUid": 897649274280,
    "name": "Internal Claim",
    "skillTypeId": 1341,
    "skillTypeName": "Claim Type",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  }],
  "actions": [{
    "id": 1,
    "ticketUid": 897649274280,
    "assignedAgentId": 10085,
    "assignedWorkGroupSkillId": 26732,
    "agent": {
      "id": 10085,
      "firstName": "Frederic",
      "lastName": "Verjans",
      "isSpecialAgent": false,
      "createTicketWithStatusNew": false,
      "entityId": 0,
      "status": "None",
      "enableBulkFtr": false
    },
    "type": "CreateTicket",
    "timeSpent": 0,
    "creationDateTime": "2015-05-07T12:25:35.0434735Z",
    "ticketCurrentAgentID": 10085,
    "ownershipChangeReason": "None",
    "ticketCurrentWorkGroupSkillId": 26732,
    "entityName": "NGAHR",
    "dueDateChangeType": "None"
  }, {
    "id": 2,
    "ticketUid": 897649274280,
    "agent": {
      "id": 10085,
      "firstName": "Frederic",
      "lastName": "Verjans",
      "isSpecialAgent": false,
      "createTicketWithStatusNew": false,
      "entityId": 0,
      "status": "None",
      "enableBulkFtr": false
    },
    "type": "AddAttachment",
    "description": "test item",
    "relatedTicketItemId": 1,
    "timeSpent": 0,
    "creationDateTime": "2015-05-07T12:25:35.0434735Z",
    "ticketCurrentAgentID": 10085,
    "ownershipChangeReason": "None",
    "entityName": "",
    "dueDateChangeType": "None"
  }],
  "items": [{
    "id": 1,
    "ticketUid": 897649274280,
    "creationDateTime": "0001-01-01T00:00:00Z",
    "type": "File",
    "agent": {
      "id": 10085,
      "firstName": "Frederic",
      "lastName": "Verjans",
      "isSpecialAgent": false,
      "createTicketWithStatusNew": false,
      "entityId": 0,
      "status": "None",
      "enableBulkFtr": false
    },
    "description": "test item",
    "file": {
      "fileName": "clock.txt",
      "contentType": "text/plain",
      "contentLength": 0
    }
  }],
  "isDueDateDynamicSet": false,
  "opmSkillId": 0,
  "buttons": "Pend, SendToAgent, SendToWorkgroup, SetReminder, Unassign, Close, Save, Email, Upload, AddCommunication",
  "isInteraction": true,
  "isNew": false,
  "isPending": false,
  "csatDuedate": "2015-05-08T08:25:35.043Z",
  "entityId": 8,
  "pendingType": "None",
  "trimmedDescription": "dfsdf",
  "reclassifiedAfterClosure": false,
  "reclassifiedInSLAAfterClosure": false,
  "reviewCompleted": false,
  "initiatedBy": "TESTAPP",
  "createdBy": "TESTAPP"
}
```

## Security group

API security group: **TicketCreate**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
