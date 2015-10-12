# Get employee tickets
```
GET /api/companies/{companySkillId}/employees/{employeeId}/tickets?scope={scope}&status={status}&fromDate={fromDate}&toDate={toDate}&sortProperty={sortProperty}&sortDirection={sortDirection}&page={page}&perPage={perPage}
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve the tickets of an employee.
The API allows you to retreive open tickets, closed tickets or both.
The API returns all tickets or can be limited to the tickets between 2 dates. The API also handles the sorting by a set of properties as well as the paging.

> Remark:
>
> fromdate & todate are currently optional. As the paging and sorting are build internally, this can result in computing a large amount of data. In a future release of the API, these dates will become mandatory.  

## Parameters

| Parameter       | Type      | Description                       | Remarque                                                      |
|-----------------|-----------|-----------------------------------|---------------------------------------------------------------|
| companySkillId  |integer    | company skill id of the employee  | -                                                             |
| employeeId      |string     | HRIS employee id                  | -                                                             |
| scope           |string     | Scope of the search               | Can be equals to "Requester" (default), "Affected" or "Both"  |
| status          |string     | Status of the ticket to return    | Can be equals to "Open" (default), "Closed" or "Both"         |
| fromDate        |date time  | Date of the oldest ticket         | -                                                             |
| toDate          |date time  | Date of the newest ticket         | -                                                             |
| sortProperty    |string     | Name of the property to sort on   | List of supported properties : id (default), creationdate, employee, requester, oladuedate, sladuedate, service, lastupdate, workgroup, currentagent |
| sortDirection   |string     | sorting direction                 | "asc" (default) for ascending otherwise, "dsc" for descending |
| page            |integer    | Page number to return             | e.g. 2 to display the second page of result                   |
| perPage         |integer    | Number of items per page          | -                                                             |

## Response

| Value       | Type                  | Description                 | Remarque                                  |
|-------------|-----------------------|-----------------------------|-------------------------------------------|
| items       | List of ticket objets | Employees tickets           | Contains a subset of a full ticket object |
| totalItems  | Integer               | Total count of tickets      | Based on the query result                 |
| page        | Integer               | Number of the page returned | -                                         |
| totalPages  | Integer               | Total count of pages        | -                                         |
| perPage     | Integer               | Ticket count per page       | -                                         |


Example:

```json
{
  "items": [see below],
  "totalItems": 30,
  "page": 1,
  "totalPages": 1,
  "perPage": 50
}

// Here under the content of the items array moved out to clarify the example

[{
  "lastUpdate": "2014-11-18T13:08:29Z",
  "id": 1002433,
  "ticketUid": 897649167297,
  "creationDateTime": "2014-10-23T13:34:15Z",
  "dueDate": "2014-10-27T13:34:15Z",
  "amberDate": "2014-10-27T09:34:15Z",
  "status": "Open",
  "securityQuestions": 0,
  "flag": "FlagNoFlagged",
  "type": "External",
  "companySkillId": 26943,
  "company": {
    "id": 0,
    "name": "YourCorp BE",
    "organisationId": 0,
    "skillId": 0
  },
  "serviceSkillId": 26826,
  "service": {
    "id": 12029,
    "name": "Claims Support",
    "skillId": 26826,
    "serviceGroupId": 0,
    "isValidForInteraction": false,
    "enableDynamicDueDate": false,
    "dateModified": "0001-01-01T00:00:00Z"
  },
  "groupingSkill": {
    "id": 26732,
    "ticketUid": 0,
    "name": "NGA_T1",
    "skillTypeId": 0,
    "skillTypeName": "Service",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  },
  "prioritySkill": {
    "id": 26714,
    "ticketUid": 0,
    "name": "Priority 1",
    "skillTypeId": 0,
    "skillTypeName": "Service",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  },
  "shortDescription": "Test for redirection",
  "employeeId": "patrickg",
  "employee": {
    "firstName": "Patrick",
    "lastName": "Grey"
  },
  "requesterId": "johnb",
  "requester": {
    "firstName": "John",
    "lastName": "Brice"
  },
  "currentAgent": {
    "id": 10081,
    "firstName": "Olivier",
    "lastName": "Lambeaux",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
  },
  "creatorAgentId": 0,
  "unflaggableByOther": false,
  "solved": false,
  "isLinkedTicket": false,
  "isDueDateDynamicSet": false,
  "opmSkillId": 0,
  "buttons": "None",
  "isInteraction": false,
  "isNew": false,
  "isPending": false,
  "csatDuedate": "2014-10-27T13:34:15Z",
  "pendingType": "None",
  "trimmedDescription": "This is a test for redirection",
  "reclassifiedAfterClosure": false,
  "reclassifiedInSLAAfterClosure": false,
  "reviewCompleted": false
}, {
  "lastUpdate": "2014-10-31T16:00:35Z",
  "id": 1002440,
  "ticketUid": 897649167304,
  "creationDateTime": "2014-10-23T15:28:41Z",
  "dueDate": "2014-10-27T15:28:41Z",
  "amberDate": "2014-10-27T11:28:41Z",
  "status": "Open",
  "securityQuestions": 0,
  "flag": "FlagNoFlagged",
  "type": "External",
  "companySkillId": 26943,
  "company": {
    "id": 0,
    "name": "YourCorp BE",
    "organisationId": 0,
    "skillId": 0
  },
  "serviceSkillId": 26856,
  "service": {
    "id": 12059,
    "name": "Administer course assessment",
    "skillId": 26856,
    "serviceGroupId": 0,
    "isValidForInteraction": false,
    "enableDynamicDueDate": false,
    "dateModified": "0001-01-01T00:00:00Z"
  },
  "groupingSkill": {
    "id": 26732,
    "ticketUid": 0,
    "name": "NGA_T1",
    "skillTypeId": 0,
    "skillTypeName": "Service",
    "isAgentSkill": false,
    "isValidForInteraction": false,
    "poolMandatory": false
  },
  "shortDescription": "test 2",
  "employeeId": "johnb",
  "employee": {
    "firstName": "John",
    "lastName": "Brice"
  },
  "requesterId": "johnb",
  "requester": {
    "firstName": "John",
    "lastName": "Brice"
  },
  "creatorAgentId": 0,
  "unflaggableByOther": false,
  "solved": false,
  "isLinkedTicket": false,
  "isDueDateDynamicSet": false,
  "opmSkillId": 0,
  "buttons": "None",
  "isInteraction": false,
  "isNew": false,
  "isPending": false,
  "csatDuedate": "2014-10-27T15:28:41Z",
  "pendingType": "None",
  "trimmedDescription": "test 2",
  "reclassifiedAfterClosure": false,
  "reclassifiedInSLAAfterClosure": false,
  "reviewCompleted": false
}]
```

## Security group

Api security group: **EmployeeHistory**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)