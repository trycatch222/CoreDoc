# Create ticket for Partner
```
POST /api/tickets
```
* [Description](#description)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Create a new ticket in MyHRW.
The behavior of the create ticket API is strongly linked to the application type selected for your application key. Based on the application type, the validation and value required in the payload may vary. The examples provided in the next topics are specific to an application of the type "Partner".

The ticket is always created in the company of the affected employee.
If at ticket creation, you only specify requester or affected employee, the API is considering them as being equal.

The company of the requester and the affected employee can be different but must always be under the same organization/customer .

Having a different requester and affected employee is useful in the scenario where a manager is submitting a request for an employee. Note that the relationship between the employee and the requester is never validated by the API, the caller should verify this relationship in the HRIS system.

For a partner ticket, based on the configuration, it is possible to avoid passing both requester and affected employee when the thidparty system is not able to know them. In that specific case a dummy employee (or proxy employee) which is already configured in the system via the MyHRW administration tool is assigned to the ticket.

At creation, the API caller must always specify the company by passing the name of the MyHRW company.

A partner ticket is always having a attached partner task. This partner task represents the link between the MyHRW ticket and the partner ticket. In this partner task, the API caller can pass information about its ticket in the partner system such as:

*  Partner ticket id
*  Status
*  Description
*  Short description
*  Status
*  Assignement group
*  Display id
*  Due date
*  Priority
*  URL

Also the partner is not required to provide a service. By configuration, the system can provide a default service. Nevertheless, in MyHRW the ticket OLA & SLA are based on the Service, therefor it's better to provide a valid service.

At ticket creation, the API also offers you the possibility to directly attach one or more files to the ticket. The binary should be encoded as a Base64 string. ([see RFC 2045](http://tools.ietf.org/html/rfc2045)).
All files passed when a partner create a ticket will be linked to the partner task.

There is two place where you can specify the short description and the description :

*  In the ticket object where they represent the work you are requesting from the MyHRW agent (mandatory)
*  In the Partner info attached to the partner task where they repesent the original short description and description on the ticket in the partner system (no mandatory)

## Body

Content-Type: application/json


| Value					| Type			 | Description											| Remark																|
|-----------------------|----------------|------------------------------------------------------|-----------------------------------------------------------------------|
|serviceSkillId			| integer		 | (optional) Service skill id of the selected service	| 32 bits																|
|shortDescription		| string		 | Short description									| max 128 characters													|
|description            | string		 | Description											| -																	    |
|requesterId			| string		 | (Optional) Requester unique id						| max 40 characters														|
|employeeId			    | string		 | (Optional) Employee unique id						| max 40 characters														|
|Company				| Company object | Object used to specify the company name	            | -                                                                     |
|Task					| collection	 | For a partner ticket, that collection will only contain one task corresponding to the partner ticket | -                    |
|Items					| collection	 | Collection of files to add to the ticket				|	-																	|
|skills					| collection	 | Collection of skill objects like the source, priority	|	-																	|

Company Object

| Value	| Type		| Description	                    | Remark	|
| ------|-----------|-----------------------------------|-----------|
| name	| string	 | Name of the company object		|	-		|

Task object details

| Value	        | Type		     | Description	                                | Remark	|
| --------------|----------------|----------------------------------------------|-----------|
| PartnerTicket	| PartnerTicket	 | Object representing the partner ticket		|	-		|

PartnerTicket object details (Information on the ticket in the partner system)

| Value	               | Type	| Description	                                                                       | Remark	|
| -------------------- |--------|--------------------------------------------------------------------------------------|-----------|
| shortdescription     | string | (optional) Short description of the third party ticket                               |-|
| description          | string | (optional) Description                                                               |-|
| id                   | string | technical id                                                                         | Used when MyHRW need to callback the partner system |
| displayid            | string | (optional) Display id                                                                | If needed, the partner system can provide a more userfriendly id |
| type                 | string | (optional) Type of the partner ticket                                                | such as incident, change request, defect, ...|
| priority             | string | (optional) Priority                                                                  |-|
| status               | string | (optional) Status                                                                    |-|
| category             | string | (optional) Category                                                                  |-|
| assignmentgroup      | string | (optional) Assignment group                                                         |-|
| assignedto           | string | (optional) Name of the agent sending the partner ticket to myHRW                     |-|


Item object details

| Value				| Type			| Description					| Remark	|
|-------------------|---------------|-------------------------------|-----------|
| type				| string		| Must be equal to "File"		| -  		|
| description		| string		| Description of the file item	| - 		|
| privacySkillId	| int			| Privacy skill id				| -  		|
| file				| File object	|								| -  		|

File object details

| Value			| Type		| Description								| Remark			 |
|---------------|-----------|-------------------------------------------|--------------------|
| fileName		| string	| Nameof									| max 2000 charaters | 
| binaryData	| string	| File binary encoded in a base64 string  |	-				 |

Skill object details

| Value	| Type		| Description	| Remark  |
| ------|-----------|---------------|---------|
| id	| integer	|skill id		|	-	  |

Example (new ticket with partner info)

```json
{
       "shortdescription":"short description for agent",
       "description":"description for agent",
       "company":{"name":"YourCorp BE"},
       "status":"Open",
       "serviceskillid":"26824",
       "tasks":[
           {
               "partnerticket":{
                "shortdescription":"Test task short descr",
                "description":"test task description",
                "id":"TKT0142096",
                "displayid":"INC1068302",
                "type":"incident",
                "priority":"5 - Planning",
                "status":"Open",
                "category":"Area: AMPS Oracle, Category: Talent Management, Subcategory: Performance Management",
                "assignmentgroup":"GTSP",
                "assignedto":"Olivier Legrand"}
            }]
 }
```

Example (new ticket with 1 file attached to it)

```json
{
       "shortdescription":"short description for agent",
       "description":"kidibul",
       "company":{"name":"YourCorp BE"},
       "status":"Open",
       "serviceskillid":"26824",
       "tasks":[
           {
               "partnerticket":{
                "shortdescription":"Test task short descr",
                "description":"test task description",
                "id":"TKT0142096",
                "displayid":"INC1068302",
                "type":"incident",
                "priority":"5 - Planning",
                "status":"Open",
                "category":"Area: AMPS Oracle, Category: Talent Management, Subcategory: Performance Management",
                "assignmentgroup":"GTSP",
                "assignedto":"Olivier Legrand"}
            }],
        "items":[
            {
		        "type" : "File",
		        "description":"test item",
		        "privacySkillId":"",
		        "File": {
			        "filename" : "clock.txt",
			    "binaryData":"ZnJpZGF5IDEwaDMwIHRvIDEyaA0KDQpTYXR1cmRheSAwMGggdG8gMmgzMCAm\nIDEwaCB0byAxNWggJiAyMmggdG8gMjNoMzANClN1bmRheSAxMGggdG8gMTNo\nDQoNCg0KMWgzMA0KMmgzMA0KNWgNCjFoMzANCjNoDQoNCjEzaDMw\n"
		}
	}]    
```

## Response

Create ticket returns the created ticket in JSON.
The properties returned in the ticket's object depends on the configuration.

Two ID's are really important in the returned structure

| Value		| Description																					|
|-----------|-----------------------------------------------------------------------------------------------|
| Id		| Id of the created ticket as displayed in the UI, it is the ID used by the agent				|
| ticketUid	| Unique technical identifier of the created ticket used as a parameter in all the API calls.	|

Example

```json
{
    "lastUpdate": "0001-01-01T00:00:00Z",
    "id": 1109867,
    "ticketUid": 897649274731,
    "creationDateTime": "2015-09-07T09:44:24.2751717Z",
    "currentStartTime": "2015-09-07T09:44:24.2751717Z",
    "dueDate": "2015-09-09T09:44:24.275Z",
    "amberDate": "2015-09-08T14:44:25Z",
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
    "serviceSkillId": 26824,
    "service": {
        "id": 12027,
        "name": "Access to TPV System",
        "skillId": 26824,
        "serviceGroupId": 1490,
        "usePriority": false,
        "isValidForInteraction": false,
        "enableDynamicDueDate": true,
        "olrId": "BE.AF",
        "dateModified": "2014-10-22T12:24:25Z",
        "isHrSensitiveData": false
    },
    "serviceGroup": {
        "id": 1490,
        "name": "Benefits",
        "serviceAreaId": 1,
        "olrId": "BE"
    },
    "serviceArea": {
        "id": 1,
        "name": "No Service Area"
    },
    "groupingSkillId": 26732,
    "groupingSkill": {
        "id": 26732,
        "ticketUid": 897649274731,
        "name": "NGA_T1",
        "skillTypeId": 1242,
        "skillTypeName": "Usergroup (YCP)",
        "isAgentSkill": true,
        "isValidForInteraction": false,
        "poolMandatory": true
    },
    "shortDescription": "short description for agent",
    "description": "description for agent",
    "employeeId": "EMPLOYEE",
    "employee": {
        "id": "EMPLOYEE",
        "firstName": "EMPLOYEE",
        "lastName": "EMPLOYEE",
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
        "backendType": "Sap",
        "backendHandleInbox": false
    },
    "requesterId": "EMPLOYEE",
    "requester": {
        "id": "EMPLOYEE",
        "firstName": "EMPLOYEE",
        "lastName": "EMPLOYEE",
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
        "backendType": "Sap",
        "backendHandleInbox": false
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
    "skills": [
        {
            "id": 26943,
            "ticketUid": 897649274731,
            "name": "YourCorp BE",
            "skillTypeId": 1,
            "skillTypeName": "Company",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": true
        },
        {
            "id": 26824,
            "ticketUid": 897649274731,
            "name": "Access to TPV System",
            "skillTypeId": 0,
            "skillTypeName": "Service",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": true
        },
        {
            "id": 0,
            "ticketUid": 897649274731,
            "name": "T1",
            "skillTypeId": 2,
            "skillTypeName": "SCAgentLevel",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": true
        },
        {
            "id": 26732,
            "ticketUid": 897649274731,
            "name": "NGA_T1",
            "skillTypeId": 1242,
            "skillTypeName": "Usergroup (YCP)",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": true
        },
        {
            "id": 26753,
            "ticketUid": 897649274731,
            "name": "Interface",
            "skillTypeId": 1243,
            "skillTypeName": "Source",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26717,
            "ticketUid": 897649274731,
            "name": "External",
            "skillTypeId": 1238,
            "skillTypeName": "Type",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26723,
            "ticketUid": 897649274731,
            "name": "No",
            "skillTypeId": 1239,
            "skillTypeName": "Payroll Impact",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26725,
            "ticketUid": 897649274731,
            "name": "No",
            "skillTypeId": 1240,
            "skillTypeName": "SLA Impact",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26727,
            "ticketUid": 897649274731,
            "name": "No",
            "skillTypeId": 1241,
            "skillTypeName": "Invoicing",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26761,
            "ticketUid": 897649274731,
            "name": "Employee",
            "skillTypeId": 1245,
            "skillTypeName": "Requestor",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 26765,
            "ticketUid": 897649274731,
            "name": "New",
            "skillTypeId": 1247,
            "skillTypeName": "Technical Phase",
            "isAgentSkill": true,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 27551,
            "ticketUid": 897649274731,
            "name": "Accepted Close Note",
            "skillTypeId": 1258,
            "skillTypeName": "Close Note Type",
            "isAgentSkill": false,
            "isValidForInteraction": false,
            "poolMandatory": false
        },
        {
            "id": 29287,
            "ticketUid": 897649274731,
            "name": "Internal Claim",
            "skillTypeId": 1341,
            "skillTypeName": "Claim Type",
            "isAgentSkill": false,
            "isValidForInteraction": false,
            "poolMandatory": false
        }
    ],
    "actions": [
        {
            "id": 1,
            "ticketUid": 897649274731,
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
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "ticketCurrentAgentID": -1,
            "ownershipChangeReason": "None",
            "ticketCurrentWorkGroupSkillId": 26732,
            "entityName": "NGAHR",
            "dueDateChangeType": "None"
        },
        {
            "id": 2,
            "ticketUid": 897649274731,
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
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "ticketCurrentAgentID": 10085,
            "ownershipChangeReason": "None",
            "entityName": "",
            "dueDateChangeType": "None"
        },
        {
            "id": 3,
            "ticketUid": 897649274731,
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
            "type": "AddTicketTask",
            "timeSpent": 0,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "relatedTicketTaskId": 1,
            "ticketCurrentAgentID": 10085,
            "ownershipChangeReason": "None",
            "entityName": "",
            "dueDateChangeType": "None"
        },
        {
            "id": 4,
            "ticketUid": 897649274731,
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
            "type": "AttachPartnerTicketToPartnerTask",
            "timeSpent": 0,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "relatedTicketTaskId": 1,
            "ticketCurrentAgentID": 10085,
            "ownershipChangeReason": "None",
            "entityName": "",
            "dueDateChangeType": "None",
            "summary": [
                {
                    "label": "Short Description",
                    "value": "Test task short descr",
                    "type": "String"
                },
                {
                    "label": "Status",
                    "value": "Open",
                    "type": "String"
                },
                {
                    "label": "Assignment group",
                    "value": "GTSP",
                    "type": "String"
                },
                {
                    "label": "Category",
                    "value": "Area: AMPS Oracle, Category: Talent Management, Subcategory: Performance Management",
                    "type": "String"
                },
                {
                    "label": "Assigned To",
                    "value": "Olivier Legrand",
                    "type": "String"
                },
                {
                    "label": "Priority",
                    "value": "5 - Planning",
                    "type": "String"
                }
            ]
        },
        {
            "id": 5,
            "ticketUid": 897649274731,
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
            "type": "AddTicketTask",
            "description": "Review Request",
            "timeSpent": 0,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "relatedTicketTaskId": 2,
            "ticketCurrentAgentID": 10085,
            "ownershipChangeReason": "None",
            "entityName": "",
            "dueDateChangeType": "None"
        },
        {
            "id": 6,
            "ticketUid": 897649274731,
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
            "type": "AddTicketTask",
            "description": "Communicate Claim to Stakeholders",
            "timeSpent": 0,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "relatedTicketTaskId": 3,
            "ticketCurrentAgentID": 10085,
            "ownershipChangeReason": "None",
            "entityName": "",
            "dueDateChangeType": "None"
        }
    ],
    "items": [
        {
            "id": 1,
            "ticketUid": 897649274731,
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
                "contentLength": 0,
                "binaryData": "ZnJpZGF5IDEwaDMwIHRvIDEyaA0KDQpTYXR1cmRheSAwMGggdG8gMmgzMCAmIDEwaCB0byAxNWggJiAyMmggdG8gMjNoMzANClN1bmRheSAxMGggdG8gMTNoDQoNCg0KMWgzMA0KMmgzMA0KNWgNCjFoMzANCjNoDQoNCjEzaDMw"
            }
        }
    ],
    "tasks": [
        {
            "ticketId": 1109867,
            "ticketUid": 897649274731,
            "id": 1,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "status": "Open",
            "subject": "Test task short descr",
            "description": "test task description",
            "resolutionTimeMandatory": false,
            "timeSpent": 0,
            "buttons": "None",
            "partnerId": 17,
            "partner": {
                "id": 17,
                "name": "ServiceNow",
                "groupSkillTypeId": 0
            },
            "type": "Partner",
            "isActive": true,
            "closeTicketMandatory": false
        },
        {
            "ticketId": 1109867,
            "ticketUid": 897649274731,
            "id": 2,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "dueDate": "2015-09-07T09:54:24.2751717Z",
            "resolutionTime": 10,
            "workgroup": {
                "id": 26732,
                "name": "NGA_T1",
                "entityId": 0,
                "canViewHrSensitiveData": false
            },
            "status": "Open",
            "predefTaskId": 65,
            "subject": "Review Request",
            "description": "Review Request",
            "resolutionTimeMandatory": true,
            "timeSpent": 0,
            "buttons": "TakeOwnership",
            "type": "Planned",
            "isActive": true,
            "closeTicketMandatory": true
        },
        {
            "ticketId": 1109867,
            "ticketUid": 897649274731,
            "id": 3,
            "creationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "dueDate": "2015-09-09T09:44:24.275Z",
            "resolutionTime": 1080,
            "workgroup": {
                "id": 26732,
                "name": "NGA_T1",
                "entityId": 0,
                "canViewHrSensitiveData": false
            },
            "status": "Open",
            "predefTaskId": 64,
            "subject": "Communicate Claim to Stakeholders",
            "description": "Communicate Claim to Stakeholders",
            "resolutionTimeMandatory": true,
            "timeSpent": 0,
            "buttons": "None",
            "type": "Planned",
            "parentTaskId": 2,
            "isActive": false,
            "closeTicketMandatory": true
        }
    ],
    "isDueDateDynamicSet": false,
    "opmSkillId": 0,
    "buttons": "TakeOwnership, Upload, AddCommunication",
    "isInteraction": false,
    "isNew": false,
    "isPending": false,
    "csatDuedate": "2015-09-09T09:44:24.275Z",
    "entityId": 8,
    "pendingType": "None",
    "trimmedDescription": "description for agent",
    "reclassifiedAfterClosure": false,
    "reclassifiedInSLAAfterClosure": false,
    "reviewCompleted": false,
    "initiatedBy": "EMPLOYEE",
    "createdBy": "EMPLOYEE",
    "companyFormFields": [
        {
            "ticketUid": 897649274731,
            "ticketId": 1109867,
            "taskId": -1,
            "fieldId": 5,
            "formFieldId": 60,
            "name": "Employee Fullname",
            "shortDescription": "",
            "order": 0,
            "isMandatory": true,
            "type": "Text",
            "minValueOrLength": 1,
            "maxValueOrLength": 10,
            "value": "",
            "predefinedValues": [],
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationBy": 10085,
            "skillId": -1
        },
        {
            "ticketUid": 897649274731,
            "ticketId": 1109867,
            "taskId": -1,
            "fieldId": 6,
            "formFieldId": 61,
            "name": "Employee Country",
            "shortDescription": "",
            "order": 1,
            "isMandatory": false,
            "type": "Text",
            "value": "BE",
            "predefinedValues": [
                {
                    "id": 1,
                    "order": 0,
                    "displayName": "Belgium",
                    "value": "BE",
                    "isDefault": true
                },
                {
                    "id": 2,
                    "order": 1,
                    "displayName": "France",
                    "value": "FR",
                    "isDefault": false
                },
                {
                    "id": 3,
                    "order": 2,
                    "displayName": "United States",
                    "value": "US",
                    "isDefault": false
                }
            ],
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationBy": 10085,
            "skillId": -1
        }
    ],
    "serviceFormFields": [
        {
            "ticketUid": 897649274731,
            "ticketId": 1109867,
            "taskId": -1,
            "fieldId": 22,
            "formFieldId": 58,
            "name": "BonusPoint",
            "shortDescription": "",
            "order": 0,
            "isMandatory": true,
            "type": "UnsignedInteger",
            "minValueOrLength": 5,
            "maxValueOrLength": 6,
            "value": "",
            "predefinedValues": [],
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationBy": 10085,
            "skillId": 26824
        },
        {
            "ticketUid": 897649274731,
            "ticketId": 1109867,
            "taskId": -1,
            "fieldId": 4,
            "formFieldId": 59,
            "name": "Employee Salary (EUR)",
            "shortDescription": "EU",
            "order": 1,
            "isMandatory": false,
            "type": "Double",
            "minValueOrLength": 1999,
            "maxValueOrLength": 9999,
            "value": "",
            "predefinedValues": [],
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationBy": 10085,
            "skillId": 26824
        },
        {
            "ticketUid": 897649274731,
            "ticketId": 1109867,
            "taskId": -1,
            "fieldId": 1,
            "formFieldId": 69,
            "name": "Employee Birthdate",
            "shortDescription": "",
            "order": 2,
            "isMandatory": false,
            "type": "DateAndTime",
            "value": "",
            "predefinedValues": [],
            "lastModificationDateTime": "2015-09-07T09:44:24.2751717Z",
            "lastModificationBy": 10085,
            "skillId": 26824
        }
    ]
}
```

## Security group

API security group: **TicketCreate**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)