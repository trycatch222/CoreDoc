# Download a file attached to ticket
```
GET /api/tickets/{ticketUid}/files/{id}
```
* [Description](#description)
* [Parameters](#param)
* [Response](#response)
* [Security group](#security-group)

## Description

Download a file attached to a ticket.
> To upload a file, the binary should be encoded as a Base64 string. ([see RFC 2045](http://tools.ietf.org/html/rfc2045)).

## Parameters

| Parameter  | Type           | Description           | Remarque  |
|------------|----------------|-----------------------|-----------|
| ticketUid  | Unsigned long  | ticket unique id      | -         |
| id         | integer        | Ticket item unique id | -         |

## Response

| Value       | Type    | Description       | Remarque                                                                        |
| ------------|---------|-------------------|---------------------------------------------------------------------------------|
| binaryData  | string  | the file content  | encoded as a Base64 string. ([see RFC 2045](http://tools.ietf.org/html/rfc2045) |

Example

```json
{
  "id": 1,
  "ticketUid": 897649167517,
  "fileName": "clock.txt",
  "contentType": "text/plain",
  "contentLength": 129,
  "binaryData": "ZnJpZGF5IDEwaDMwIHRvIDEyaA0KDQpTYXR1cmRheSAwMGggdG8gMmgzMCAmIDEwaCB0byAxNWggJiAyMmggdG8gMjNoMzANClN1bmRheSAxMGggdG8gMTNoDQoNCg0KMWgzMA0KMmgzMA0KNWgNCjFoMzANCjNoDQoNCjEzaDMw",
  "creationDateTime": "2014-11-25T15:31:27Z",
  "privacySkillId": -1,
  "privacySkillName": "",
  "documentTypeName": "",
  "agent": {
    "id": 10073,
    "firstName": "Ask",
    "lastName": "HR",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
  }
}
```
## Security group

API security group: **TicketItemDownload**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)