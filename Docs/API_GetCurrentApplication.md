# Get current application
```
GET /api/applications/current
```
* [Description](#description)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve the characteristics of the application associated with your application key.

## Response

| Value              | Type     | Description                                     | Remarque                                                      |
| -------------------|----------|-------------------------------------------------|---------------------------------------------------------------|
| id                 | string   | Application unique id                           | -                                                             |
| name               | string   | Application name                                | -                                                             |
| associatedAgentId  | integer  | Generic agent associated with your application  | Defines your configuration schema                             |
| applicationType    | string   | Application type                                | Defines certain API behaviour                                 |
| apiSecurityGroups  | string   | API security groups                             | Provides you the list of API groups to which you have access  |

Example

```json
{
  "id": "ASKHR",
  "name": "Ask HR (Inbox)",
  "associatedAgentId": 10073,
  "applicationType": "Inbox",
  "apiSecurityGroups": "Cache, TicketRead, TicketWrite, TicketCreate, TicketOperation, TaskRead, TaskWrite, TaskCreate, TaskOperation, TicketActionRead, TicketActionWrite, TicketActionCreate, TicketItemDownload, TicketItemUpload, PartnerInteraction, Pool, EmployeeSearch, EmployeeHistory, OLR, HRIS, AgentConfig, Alerting, Archive, BatchNotification, CompanyConfig, EmailProcessor, IVR, Logging, Report, Reminder, Survey, Telephony, Translation, TOP, Monitoring"
}
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
