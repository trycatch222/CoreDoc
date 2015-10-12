# Get ticket communications
```
GET /api/tickets/{ticketUid}/communications
```
* [Description](#description)
* [Parameters](#parameters)
* [Response](#response)
* [Security group](#security)

## Description

Allows you to retrieve all the communications attached to a ticket.
In a ticket, communications represent all the events in ticket which are relevant for an agent.

Communications includes:

*  Mail sent or received.
*  Comment added by an agent
*  Messages exchanged between agents collaborating on the ticket
*  Messages exchanged with the requester through the employee portal.
*  Ticket or tasks re-assignment.
*  Tasks completion
*  Partner ticket updates

For Inbox/askHR like application you can specify the optional parameter "__forInbox=true__" to return only __messages & emails__ exchanged between the __agents and the requester__.
 

## Parameters

| Parameter | Type          | Description       |                                                     Remarque  |
|-----------|---------------|-----------------------------------------------------------------------|-----------|
| ticketUid | Unsigned long | ticket unique id  | -                                                 |           |
| taskId    | int           | taskid, returns only the communication associated with the a task      | -         |
| limit     | int           | returns only the {limit} last communications                           | -         |
| forInbox  | bool          | if true, returns only communications between the requester and the agent | cannot be used with the limit parameter         |

## Response

| Value             | Type          | Description                                     | Remarque                                      |
|-------------------|---------------|-------------------------------------------------|-----------------------------------------------|
| id                | integer       | unique id of the communication in the ticket    | -                                             |
| ticketUid         | unsigned long | ticket unique id that the communication belongs to | -                                             |
| dateCreated       | date time     | creation date of the communication              | -                                             |
| type              | string        | type                                            | -                                             |
| ticketItemId      | date time     | ticket item id                                  |When the communication is of type "AddMail", this id represents the id of the ticket item containing the full mail |
| ticketActionId    | integer       | id of the associated ticket action id     | -                                             |
| sender            | string        | sender name                               | -                                             |
| senderAgentId     | integer       | sender technical agent id                 | Represent the agent sending the communication or the technical agent associated with the source application (Such as for messages sent from askHR portal)  |
| receiver          | string        | receiver name                             | -                                             |
| subject           | string        | subject of the communication              | Used for mail
| message           | string        | message text                              | For email, this field contains the mail body, trimmed, without blank line and limited to the 2000 first characters |
| isIncomingPartnerAction | bool      | Message coming from a partner case tool   | Used for integration                          |
| ownershipChangeReason   | string    | ownership change reason                   | SendTicketToAgent, SendTicketToWorkgroup, ... |
| targetWorkgroup         | string    | target work group                         | -                                             |
| targetWorkgroupSkillId  |   integer | target work group skill id                | -                                             |
| sourceWorkgroup         | string    | source work group                         | -                                             |
| sourceWorkgroupSkillId  |  integer  | source work group skill id                | -                                             |

Example:
```
/api/tickets/897649275306/communications?forinbox=true
```

```json
[
  {
    "id": 1,
    "dateCreated": "2015-09-21T07:45:07Z",
    "ticketUid": 897649275306,
    "type": "AddMail",
    "ticketItemId": 1,
    "sender": "Olivier.Legrand@yourcorp.com",
    "senderAgentId": 10078,
    "receiver": "yourcorp.be@sct.arindemo.com",
    "subject": "Issue with my payslip",
    "message": "sample message",
    "isIncomingPartnerAction": false,
    "ownershipChangeReason": "None",
    "targetWorkgroup": "",
    "sourceWorkgroup": ""
  },
  {
    "id": 3,
    "dateCreated": "2015-09-21T07:49:33Z",
    "ticketUid": 897649275306,
    "type": "MessageReceivedFromInbox",
    "ticketActionId": 4,
    "sender": "Olivier Legrand",
    "senderAgentId": 10378,
    "receiver": "",
    "subject": "",
    "message": "Message from fred in his inbox hellloooo",
    "isIncomingPartnerAction": false,
    "ownershipChangeReason": "None",
    "targetWorkgroup": "",
    "sourceWorkgroup": ""
  },
  {
    "id": 4,
    "dateCreated": "2015-09-21T11:38:20Z",
    "ticketUid": 897649275306,
    "type": "AddMail",
    "ticketItemId": 2,
    "sender": "yourcorp.be@sct.arindemo.com",
    "senderAgentId": 10085,
    "receiver": "Olivier.Legrand@yourcorp.com",
    "subject": "[TICKETID:1110442] Issue with my payslip",
    "message": "test mail sent",
    "isIncomingPartnerAction": false,
    "ownershipChangeReason": "None",
    "targetWorkgroup": "",
    "sourceWorkgroup": ""
  }
]
```

## Security group

API security group: **TicketRead**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
