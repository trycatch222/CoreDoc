# Send message to partner task
```
POST /api/tickets/{ticketUid}/messages
```
* [Description](#description)
* [Parameters](#parameters)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Add a comment to an existing partner task

## Parameters

Parameter| Type | Description | Remarque
----------------|-------|------|-------
ticketUid| Unsigned long| ticket unique id |

## Body

Content-Type: application/json

Value| Type | Description | Remarque
----------------|-------|------|-------
taskid| integer | Partner task id |
text| string | Message text  |
privacySkillId| integer | (optional) privacy skill id | 32 bits

Example

```json
{   
   "taskid":"1",
   "text":"This is a sample comment"
}
```

## Response

None (code 204, No Content)

## Security group

API security group: __TicketOperation__

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
