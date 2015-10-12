# Get ticket
```
GET /api/tickets/{ticketUid}
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve the details of a ticket.

## Parameters

| Parameter | Type          | Description      | Remarque |
|-----------|---------------|------------------|----------|
| ticketUid | unsigned long | ticket unique id | -        |

## Response

| Value                   | Type                  | Description                                           | Remarque                                    |
|-------------------------|-----------------------|-------------------------------------------------------|---------------------------------------------|
| id                      | integer               | UI Ticket id                                          | Technical id for internal use only          |
| ticketUid               | unsigned long         | ticket unique id                                      | -                                           |
| dueDate                 | date time             | OLA due date of the current entity                    | -                                           |
| serviceGroupId          | integer               | Unique id of the service group                        | -                                           |
| amberDate               | date time             | OLA Amber date                                        | -                                           |
| usePriority             | boolean               | Requires a priority skill                             | -                                           |
| company                 | Company object        | Properties of company of the ticket                   | -                                           |
| enableDynamicDueDate    | boolean               | A dynamic due date can be set for this service        | -                                           |
| serviceSkillId          | integer               | Service skill id                                      | -                                           |
| dateModified            | Date time             | Last modification date of the service in the admin db | -                                           |
| groupingSkillId         | integer               | Grouping skill id                                     | -                                           |
| groupingSkill           | Skill object          | Properties of the ticket group                        | -                                           |
| prioritySkillId         | integer               | Priority skill id                                     | -                                           |
| prioritySkill           | Skill object          | Properties of the ticket priority                     | -                                           |
| shortDescription        | string                | Short description                                     | -                                           |
| description             | string                | Description                                           | -                                           |
| trimmedDescription      | string                | Trimmed description                                   | 1000 first characters of the description without white spaces and blank lines  |
| solution                | string                | Solution                                              | -                                           |
| employeeId              | string                | HRIS employee ID of the affected employee             | -                                           |
| employee                | Employee object       | Affected employee details                             | -                                           |
| requesterId             | string                | HRIS employee ID of the requester employee            | -                                           |
| requester               | Employee object       | Requester employee details                            | -                                           |
| currentAgent            | Agent object          | Detail on the agent owning the ticket                 | -                                           |
| requesterClientSkillId  | integer               | Company skill id of the requester                     | -                                           |
| skills                  | List of skill objects | List of skills / attribute defining the ticket        | -                                           |
| isNew                   | boolean               | Ticket is in a "New" state if true                    | Indicate that no agent has touch the ticket |
| isPending               | boolean               | Ticket is in pending state if true                    | Sla or Ola is stopped                       |
| pendingType             | string                | Pending type                                          | Entity = the OLA is stopped only, Employee = OLA and SLA are stopped  |
| entityId                | integer               | Current entity id of the ticket                       | -                                           |

Example:
```json
{
  "lastUpdate": "2014-11-20T14:10:56Z",
  "id": 1002569,
  "ticketUid": 897649167433,
  "creationDateTime": "2014-11-18T08:54:19Z",
  "currentStartTime": "2014-11-20T14:10:56Z",
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
    "name": "Application/System Support",
    "serviceAreaId": 1,
    "olrId": "",
    "order": 3
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
    "skillTypeName": "Agent level",
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
  "currentAgent": {
    "id": 10082,
    "firstName": "Lucas",
    "lastName": "Romano",
    "fullName": "Lucas Romano",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
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
    "id": 26723,
    "ticketUid": 897649167433,
    "name": "No",
    "skillTypeId": 1239,
    "skillTypeName": "04. Payroll Impact (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26725,
    "ticketUid": 897649167433,
    "name": "No",
    "skillTypeId": 1240,
    "skillTypeName": "05. SLA Impact (YCP)",
    "isAgentSkill": true,
    "isValidForInteraction": false,
    "poolMandatory": false
  }, {
    "id": 26727,
    "ticketUid": 897649167433,
    "name": "No",
    "skillTypeId": 1241,
    "skillTypeName": "06. Invoicing (YCP)",
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
  "csatDuedate": "2014-11-25T08:54:19Z",
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

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
