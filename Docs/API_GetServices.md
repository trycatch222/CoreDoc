# Get services of a company
```
GET /api/companies/{companySkillId}/services?labelId={labelId}
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve all the services assigned to a company.
The list can restricted providing a label id (grouping label).

## Parameters

| Parameter       | Type    | Description                 | Remarque                                      |
|-----------------|---------|-----------------------------|-----------------------------------------------|
| CompanySkillId  | Integer | Company skillid             | -                                             |
| LabelId         | Integer | Id of the label (optional)  | Used to limit the number of returned service  |

## Response

| Value                   | Type      | Description                                           | Remarque                                        |
|-------------------------|-----------|-------------------------------------------------------|-------------------------------------------------|
| id                      | integer   | id of the service                                     | Technical id for internal use only              |
| name                    | string    | Name of the service                                   | -                                               |
| skillId                 | integer   | unique id of the service                              | Used in other API calls to identify the service |
| serviceGroupId          | integer   | Unique id of the service group                        | -                                               |
| labelId                 | integer   | uid of the label                                      | -                                               |
| usePriority             | boolean   | Requires a priority skill                             | -                                               |
| isValidForInteraction   | boolean   | Can be used for a first touch resolution ticket       | -                                               |
| enableDynamicDueDate    | boolean   | A dynamic due date can be set for this service        | -                                               |
| olrId                   | string    | Online reference mapping Id                           | -                                               |
| dateModified            | Date time | Last modification date of the service in the admin db | -                                               |

Example:

```json
[{
  "id": 12075,
  "name": "Cost Center Maintenance",
  "skillId": 26872,
  "serviceGroupId": 1494,
  "labelId": 2,
  "usePriority": false,
  "isValidForInteraction": false,
  "enableDynamicDueDate": false,
  "olrId": "",
  "dateModified": "2014-01-27T16:21:25Z"
}, {
  "id": 12076,
  "name": "Inaccurate Data Entry",
  "skillId": 26873,
  "serviceGroupId": 1494,
  "labelId": 2,
  "usePriority": false,
  "isValidForInteraction": false,
  "enableDynamicDueDate": false,
  "olrId": "",
  "dateModified": "2014-01-27T16:21:25Z"
}, {
  "id": 12077,
  "name": "Job Catalog Maintenance",
  "skillId": 26874,
  "serviceGroupId": 1494,
  "labelId": 2,
  "usePriority": false,
  "isValidForInteraction": false,
  "enableDynamicDueDate": false,
  "olrId": "",
  "dateModified": "2014-01-27T16:21:25Z"
}, {
  "id": 12078,
  "name": "Job Maintenance",
  "skillId": 26875,
  "serviceGroupId": 1494,
  "labelId": 2,
  "usePriority": false,
  "isValidForInteraction": false,
  "enableDynamicDueDate": false,
  "olrId": "",
  "dateModified": "2014-01-27T16:21:25Z"
}]
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)