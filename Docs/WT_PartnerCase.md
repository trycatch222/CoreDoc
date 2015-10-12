# Partner application walkthrough

## Introduction 

For collaboration purposes, a 3rd party ticketing application must be able to create and update a ticket in MyHRW. This type of application is called a "Partner" application.
Partner applications are limited to:

* Read the MyHRW Customer configuration information required to create a ticket
* Search for employees 
* Create the ticket.
* Add ticket attachments
* Add comments to the ticket
* Add and update partner ticket information linked to the MyHRW ticket

A partner ticket always contains a Partner task representing the link between the MyHRW ticket and the ticket in the partner system.

In this task, the partner can provide and maintain a set of properties informing the MyHRW agent about the ticket in the source system.

*  Partner ticket id (technical id)
*  Display id
*  Status
*  Description
*  Short description
*  Status
*  Assignment group
*  Due date
*  Priority
*  URL 

In this set, a partner application can provide an URL to it's ticket. If set, a clickable link will be displayed on the MyHRW UI enabling the agent to have a detailed view of the source ticket.

## Configuration 

Before using the MyHRW API, a working MyHRW Customer configuration is mandatory in the MyHRW administration database. This configuration should include the following MyHRW components:

* An application of type “Partner” for which you will receive the application key.
* A fixed source skill (attribute) must be configured at application level.
* A generic MyHRW agent account (back-end user account) needs to be associated with the application key.
* MyHRW companies and skills must be assigned to this generic agent account.
* Service groups and services must be assigned to the companies.

The Application key or token links your application to the entire Customer configuration. This will ensure that your application performs actions within the configured boundaries.

Please contact the MyHRW on-boarding team for further questions on the client configuration and setup models.

## Companies 

In MyHRW, a customer is represented by an Organization for enterprise clients, a Company for mid-market clients or a customer skill (attribute) for UK SMB clients.
A MyHRW organization is itself divided in companies (sometimes called countries)

Example, a YourCorp organization is composed of 3 companies YourCorp BE, YouCorp MX, YourCorp US.

Each company has a unique id, called __company skill id__ (see [Get companies](/docs/API_GetCompanies)) 

When a partner tool creates a ticket, this tool should not pass the company skill id as such, he must provide a valid company name during the create ticket (see [Create ticket for Partner](/docs/API_CreateTicket_Partner)). 

The company name is mandatory and must be passed on when a partner needs to create a ticket.

Based on the configuration it is possible that the company of the employee overwrites the company passed in the companyskillid if both companies belong to the same organization. 


## Employees

Two employees need to be associated with a MyHRW ticket.

__The Requester__

The requester is the employee that contacts the HR service center. It can be the employee having an issue or it can be a manager submitting a request for one of its team members. 

__The Affected employee__

The Affected employee is the person affected by the request. In other words, it is the person having an issue or for whom a change is needed. __The ticket always belongs to the company of the affected employee__. 

In a majority of the cases, an employee is contacting the HR service center for himself so in general the Requester and the Affected employee are one and the same. 

When you create a ticket, you should provide an ID for the affected employee and and an ID for the requester. In the case you just provide one of the two ID's, the second ID will automatically be alligned with the first one.

## Services 

A service is used to categorize a ticket, it reflects the type of request.
The service also defines the SLA & OLA’s that will be applied to the ticket.

As such, a service is mandatory and the service needs to be selected before creating a ticket.

Services are defined per company. This means that the list of services we provide for a company can be different for YourCorp BE compared to YourCorp US.

To facilitate service selection, services are grouped under service groups.

## Discovering configuration information {#discover}

The MyHRW companies (countries) you will have to map can be provided by the MyHRW administration team or you can discover them using your application key calling the different APIs.

Use: 

1. __GET api/applications/current__ to retrieve your associated agent id (see [Get current application API](/docs/API_GetCurrentApplication))
2. __GET api/companies__ to retrieve all companies for which your application can create tickets (see [Get companies API](/docs/API_GetCompanies))
3. __GET api/companies/{companySkillId}/servicegroups__ to retrieve the list of service groups associated with a company (see [Get service group API](/docs/API_GetServiceGroups))   
4. __GET api/companies/{companySkillId}/services__ to retrieve the list of services associated with a company (see [Get service API](/docs/API_GetServices))  
5. __GET api/companies/{companySkillId}/privacies__ to retrieve the list of privacy skills that can be used when adding a file (see [Get privacy skills API](/docs/API_GetPrivacies) 


## Employee search

MyHRW has connectors to many HRIS systems such as SuccessFactors, SAP, WorkDay, Preceda, Fusion, Oracle Database, ResourceLink, SMB UK CDM, etc...

These connectors are configured by company and the MyHRW Core API can be used to search employees in all these systems in a generic way. 

Employee (requester of affected employee)  can be searched by multiple criteria

* By employee Id (see [Get employee by Id](/docs/API_GetEmployeeById))
* By employee first name  or/and last name (see [Search employee](/docs/API_SearchEmployee))
* By employee email address (see [Search employee](/docs/API_SearchEmployee))

## Creating a ticket

When a partner creates a ticket you must specify all parameters required such as service, short description, description and all the mandatory skills. 
Depending on the configuration some mandatory skills can have default values and can be omitted but this behavior is configuration specific.

To create a ticket see [Create ticket for partner API](/docs/API_CreateTicket_Generic) for details.

## Work with ticket files

Files can be attached to a ticket 

* At ticket creation (see [Create ticket for partner API](/docs/API_CreateTicket_Generic))
* To attach a file to a partner task (see [Upload file to partner task API](/docs/API_UploadFileToTask))

## Send message to partner task

* Send message to partner task (see [Send message to partner task API](/docs/API_AddCommentToPartnerTask))

## Update partner info

* To update partner ticket info in the ticket task (see [Update partner ticket info API](/docs/API_UpdatePartnerInfo))

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)