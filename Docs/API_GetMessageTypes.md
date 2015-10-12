# Get message types of a company
```
GET /api/companies/{companySkillId}/messageTypes
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve all the message types that you can use to send a message on a ticket.

## Parameters

| Parameter       | Type    | Description       | Remarque  |
|-----------------|---------|-------------------|-----------|
| CompanySkillId  | Integer | Company skill id  | -         |

## Response

| Value       | Type    | Description                                                       | Remarque                                   |
|-------------|---------|-------------------------------------------------------------------|--------------------------------------------|
| id          | integer | message type id                                                   | -                                          |
| name        | string  | Name of the message type                                          | -                                          |  
| template    | string  | Predefined message type that can be used when sending the message | Is not added automatically if message is sent blank. Can be modified before sending.|
| description | string  | description of the message type                                   | -                                           |

Example:

```json
[{
  "id": 9068,
  "name": "Result of Testing",
  "template": "Result of testing (OK/NOK) : \ \ if \"NOK\", remarks : \ \ Request for transport to production (Yes/No) : \ \ Proof of testing attached to parent ticket (Yes/No) :\ \ if \"No\", reason why not :",
  "description": ""
}, {
  "id": 9069,
  "name": "4-eyes Review",
  "template": "4-eyes review completed",
  "description": ""
}, {
  "id": 9070,
  "name": "Inbound call",
  "template": "",
  "description": ""
}, {
  "id": 9071,
  "name": "Outbound call",
  "template": "",
  "description": ""
}, {
  "id": 9073,
  "name": "Connect to system",
  "template": "",
  "description": ""
}, {
  "id": 9074,
  "name": "Contacted 3rd party",
  "template": "",
  "description": ""
}, {
  "id": 9075,
  "name": "Contacted HRO",
  "template": "",
  "description": ""
}, {
  "id": 9076,
  "name": "Contacted customer",
  "template": "",
  "description": ""
}, {
  "id": 9077,
  "name": "Information update",
  "template": "",
  "description": ""
}, {
  "id": 9078,
  "name": "Internal remark",
  "template": "",
  "description": ""
}, {
  "id": 9079,
  "name": "Superuser Access",
  "template": "",
  "description": ""
}]
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
