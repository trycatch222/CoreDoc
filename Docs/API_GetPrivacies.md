# Get privacy skills of a company
```
GET /api/companies/{companySkillId}/privacies
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve all the privacy skills that can be used when attaching files or a message to a ticket.

## Parameters

| Parameter       | Type    | Description     | Remarque  |
|-----------------|---------|-----------------|-----------|
| CompanySkillId  | Integer | Company skillid | -         |

## Response

| Value     | Type    | Description                                                                         | Remarque  |
|-----------|---------|-------------------------------------------------------------------------------------|-----------|
| id        | integer | skill id of the privacy                                                             | -         |
| name      | string  | Name of the privacy skill                                                           | -         |
| isDefault | bool    | if true this privacy skill will be added to a item if no other have been specified  | -         |

Example:

```json
[{
  "id": 26763,
  "name": "External",
  "isDefault": false
}, {
  "id": 26764,
  "name": "Internal",
  "isDefault": false
}]
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
