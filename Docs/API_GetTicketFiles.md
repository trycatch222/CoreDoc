# Get ticket files
```
GET /api/tickets/{ticketUid}/files
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security)

## Description

Allows you to retrieve all the files attached to a ticket.
This API does not download the binaries of each files, it retreives only the metadata. See the [download file API](API_DownloadFile.html) to download a file.

## Parameters

| Parameter | Type          | Description       | Remarque  |
|-----------|---------------|-------------------|-----------|
| ticketUid | Unsigned long | ticket unique id  | -         |

## Response

| Value             | Type          | Description                               | Remarque                                      |
|-------------------|---------------|-------------------------------------------|-----------------------------------------------|
| id                | integer       | unique id of the file in the ticket       | -                                             |
| ticketUid         | unsigned long | Ticket unisque id that the file belongs   | -                                             |
| contentType       | string        | content type                              | -                                             |
| contentLength     | long          | size of the file                          | -                                             |
| creationDateTime  | date time     | creation date time                        | -                                             |
| privacySkillId    | integer       | privacy skill id                          | -                                             |
| privacySkillName  | string        | privacy skill name                        | -                                             |
| documentTypeName  | string        | MyHRW document type name                  | Document type is used to export file to a DMS |
| agent             | Agent object  | Properties of the agent who add the file  | -                                             |

Example:

```json
[{
  "id": 1,
  "ticketUid": 897649167517,
  "fileName": "clock.txt",
  "contentType": "text/plain",
  "contentLength": 129,
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
}, {
  "id": 3,
  "ticketUid": 897649167517,
  "fileName": "RedisBase.cs",
  "contentType": "application/octet-stream",
  "contentLength": 846,
  "creationDateTime": "2014-11-25T15:43:00Z",
  "privacySkillId": -1,
  "privacySkillName": "",
  "documentTypeName": "",
  "agent": {
    "id": 10085,
    "firstName": "Frederic",
    "lastName": "Verjans",
    "isSpecialAgent": false,
    "createTicketWithStatusNew": false,
    "entityId": 0,
    "status": "None"
  }
}]
```

## Security group

API security group: **TicketItemDownload**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
