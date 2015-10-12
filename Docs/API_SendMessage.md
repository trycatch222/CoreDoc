# Send message
```
POST /api/tickets/{ticketUid}/messages
```
* [Description](#description)
* [Parameters](#parameters)
* [Body](#body)
* [Response](#response)
* [Security group](#security)

## Description

Send a message to an existing ticket

## Parameters

| Parameter | Type          | Description       | Remarque  |
|-----------|---------------|-------------------|-----------|
| ticketUid | Unsigned long | ticket unique id  | -         |

## Request

Content-Type: application/json

| Value           | Type    | Description       | Remarque  |
|-----------------|---------|-------------------|-----------|
| messageTypeId   | Integer | Message type id   | __The message type cannot be use by application of type Inbox, value will be ignored__         |
| text            | string  | Message text      | -         |
| privacySkillId  | integer | privacy skill id  | 32 bits   |

Example

```json
{
  "messageTypeId":"9077",
  "text":"test",
  "privacySkillId":"26763"
}
```

## Response

None

## Security group

API security group: **TicketOperation**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)