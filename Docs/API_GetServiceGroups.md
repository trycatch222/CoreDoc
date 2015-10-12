# Get service groups of a company
```
GET /api/companies/{companySkillId}/servicegroups?labelId={labelId}
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve all the service groups assigned to a company.
The list can be restricted providing a label id (grouping label).

## Parameters

| Parameter       | Type    | Description                 | Remarque                                            |
|-----------------|---------|-----------------------------|-----------------------------------------------------|
| companySkillId  | Integer | Company skillid             | -                                                   |
| labelId         | Integer | Id of the label (optional)  | Used to limit the number of returned service groups |

## Response

| Value           | Type    | Description                                             | Remarque  |
|-----------------|---------|---------------------------------------------------------|-----------|
| id              | integer | ID of the service group                                 | -         |
| serviceAreaId   | integer | Service area id                                         | -         |  
| olrId           | string  | Online reference mapping Id                             | -         |  
| order           | int     | Used to sort service groups as defined by the customer  | -         |

Example:

```json
[
  [{
    "id": 1494,
    "name": "Organizational Management",
    "serviceAreaId": 1,
    "olrId": "",
    "order": 10
  }, {
    "id": 1623,
    "name": "Payroll Management",
    "serviceAreaId": 1,
    "olrId": "",
    "order": 11
  }]
]
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)