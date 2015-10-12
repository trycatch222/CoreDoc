# HRW Core REST API development landscape

## Introduction

An API caller is a third party application calling the MyHRW Core API for interacting with the MyHRW case management tool. In general, the API caller calls the CORE API for Inbox integration (Inbox type) or case management integration (Partner type). 

This document describes the MyHRW landscape that a caller should understand and must map with his own landscape during his SDLC.

As best practice, the caller should follow the classic SDLC: starting on the development system, testing on the quality and acceptance system and finally moving the solution to the production system.


## Environments description

### Development (SCT-DEV)

SCT DEV is the development  system and is the place where an API caller will connect to make his development using the MyHRW Core API. The configuration is always customer agnostic and is using the generic YourCorp organization.

### Quality & Acceptance (TST)

TST is the customer QA system, it is the place where the quality & acceptance tests are performed before the application using the MyHRW Core API is going live. The configuration is always customer specific.

### Production (PRD)

PRD is the production environment where live applications are running. The configuration is always customer specific.

## Customer agnostic vs. customer specific environment.

When you want to create a ticket in MyHRW, you have to provide a set of values based upon the MyHRW customer specific configuration. These values are materialized by various ID's you need to pass as parameters in each call to the API e.g. service skill ID, customer skill ID, etc...

The minimum information you need to pass in a call can vary from customer to customer configurations. For example, for a given customer you have to pass the API the customer and service skill ID to successfully create a ticket but for another customer you may have to provide more ticket attributes (such as language, priority, etc...) because these attributes have been set as mandatory in the customer configuration.

In the MyHRW landscape, the Development system is segregated from the QA & Production systems and are managed by different teams. Be adviced that their setup is likely to be different. 

Development is managed by the NGAHR Products SCT Development team and will never reflect a specific customer configuration. In the development system you will only find generic customers such as YourCorp & MyCorp which are  overall representative and generic configurations.

QA & Production are managed by the NGA GT&AS (Global Technology and Application Services) SCT (Service Center Technology) team and these systems contain the same customers configuration data. This means that the tests you will perform on QA, using specific customer ID’s, service ID’s, will be 100% representative for what will occur on the Production system just because both systems share the same ID’s.

Please refer to the table below to find information on the systems you need to connect to and to understand which team you have to contact to request information & access.

## Environment specific data

### Development SCT-DEV

|Type                 |Development                                                                     |
| --------------------|--------------------------------------------------------------------------------|
|MyHRWCore URL        |https://sctdevmyhrw-api.ngahr.com                                               |
|Documentation URL    |[https://sctdevmyhrw-api.ngahr.com/docs](https://sctdevmyhrw-api.ngahr.com/docs)|
|Configuration        |Generic                                                                         |
|Responsible team     |NGAHR Products SCT Development                                                    |
|Contact person       |Thibaud Galand                                                                  |
|Contact email address|[thibaud.galland@ngahr.com](thibaud.galland@ngahr.com)                                                       |


For the customer specific environments, the best way to reach out to the NGA GT&AS SCT Support team is to raise a Service-NOW ticket, NGA’s IT case management tool, using the Service Catalog to submit your request for the correct team as shown below:

![Service Catalog > Product Offering > Service Center Technologies](/content/images/docs/snow.png)

Alternatively, if you do not have access to the Service-NOW portal you can submit your request by sending an email to [iso@ngahr.com](iso@ngahr.com), our Global Service Desk will then dispatch your request.

### Quality & Acceptance (TST)

|Type                 |QA                                                                              |
| --------------------|--------------------------------------------------------------------------------| 
|MyHRWCore URL        |https://tstmyhrw-api.ngahr.com/api                                              |
|Documentation URL    |[https://tstmyhrw-api.ngahr.com/docs](https://tstmyhrw-api.ngahr.com/docs)      |
|Responsible team     |NGAHR GT&AS SCT Support                                                            |
|Contact person       |Pablo Munoz                                                                     |
|Contact email address|[pablo.munoz@ngahr.com](pablo.munoz@ngahr.com)                                                           |

### Production (PRD)

|Type                 |PRD                                                                             |
| --------------------|--------------------------------------------------------------------------------|
|MyHRWCore URL        |https://myhrw-api.ngahr.com/api                                                 |
|Documentation URL    |[https://myhrw-api.ngahr.com/docs](https://myhrw-api.ngahr.com/docs)            |
|Responsible team     |NGAHR GT&AS SCT Support                                                            |
|Contact person       |Pablo Munoz                                                                     |
|Contact email address|[pablo.munoz@ngahr.com](pablo.munoz@ngahr.com)                                                               |

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)