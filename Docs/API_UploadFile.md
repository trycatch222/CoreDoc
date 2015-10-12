# Upload file to ticket
```
POST /api/tickets/{ticketUid}/files
```
* [Description](#description)
* [Parameters](#parameters)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Upload a file and attach it to a ticket.
> To upload a file, the binary should be encoded as a Base64 string. ([see RFC 2045](http://tools.ietf.org/html/rfc2045)).

## Parameters

| Parameter | Type          | Description       | Remarque  |
|-----------|---------------|-------------------|-----------|
| ticketUid | Unsigned long | ticket unique id  | -         |

## Body

Content-Type: application/json

| Value           | Type    | Description                               | Remarque            |
|-----------------|---------|-------------------------------------------|---------------------|
| description     | String  | Description of the ticket item            | max 2000 charaters  |
| privacySkillId  | integer | privacy skill id                          | 32 bits             |
| fileName        | string  | Nameof                                    | max 2000 charaters  |
| binaryData      | string  | file binaries encoded in a base64 string  | -                   |

Example

```json
{
  "description": "test item",
  "privacySkillId": "",
  "fileName": "clock.txt",
  "binaryData": "ZnJpZGF5IDEwaDMwIHRvIDEyaA0KDQpTYXR1cmRheSAwMGggdG8gMmgzMCAm\nIDEwaCB0byAxNWggJiAyMmggdG8gMjNoMzANClN1bmRheSAxMGggdG8gMTNo\nDQoNCg0KMWgzMA0KMmgzMA0KNWgNCjFoMzANCjNoDQoNCjEzaDMw\n"
}
```

## Response

| Value | Type  | Description           | Remarque                    |
|-------|-------|-----------------------|-----------------------------|
| id    | int   | Ticket item unique id | Needed to download the file |

Example:

```json
{
  "id": 2,
  "ticketUid": 897649167433,
  "creationDateTime": "2014-11-25T14:54:13.4073121Z",
  "type": "File",
  "agent": {
    "id": 10073,
    "firstName": "Ask",
    "lastName": "HR",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
  },
  "description": "test item",
  "file": {
    "fileName": "clock.txt",
    "contentType": "text/plain",
    "contentLength": 129
  }
}
```

## Security group

API security group: **TicketItemUpload**


## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)