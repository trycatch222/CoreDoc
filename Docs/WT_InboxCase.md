# Inbox/AskHR application walkthrough

## Introduction

The Inbox application (also referred to as askHR or HR Request) is used to develop the integration between any employee portal and MyHRW. Inbox allows employees or managers to create a ticket by selecting the service (type of request) and providing a short description and description as well as uploading an attachment.
In order to accomplish this, web sites or HRIS systems having the Inbox integration should authenticate the employee. The MyHRW API will not validate the identity of employee or manager submitting the request.

## Configuration

Before using the MyHRW API, a working customer configuration must be available in the MyHRW administration database. This configuration should include the following MyHRW components:

* An application of type “Inbox” for which you will receive the application key
* A fixed source skill (attribute) must be configured at application level
* A generic MyHRW agent (user) must be associated with the application key
* MyHRW companies and skills must be assigned to the generic agent.
* Service groups and services must be assigned to the companies

The Application key or token links your application to the entire above configuration. This will ensure that your application performs actions within the configured boundaries.

Please contact the MyHRW administration teams for further questions on the client onboarding and setup models.

## Companies

In MyHRW, a customer is represented by an Organization for Enterprise clients, a Company for mid-market clients or a customer skill (attribute) for UK SMB clients.
The MyHRW organization is itself divided in companies (sometimes called countries)

Example, a YourCorp organization is composed by 3 companies YourCorp BE, YouCorp MX, YourCorp US.

Each company has a unique id, called **company skill id** (see [Get companies](/docs/API_GetCompanies)) 

In a typical Inbox development the MyHRW companies will be selected based on the employee country. It is obvious that for product integrating, the Inbox solution has to perform an internal mapping between MyHRW companies and their internal representation. 

## Services

A service is used to categorize a ticket, it represent type of request.
The service also defines the SLA & OLA’s that will be applied to the ticket.

As such, a service is mandatory and the service needs to be known before creating a ticket.

Services are defined per company. This means that the list of services we provide for a company can be different for YourCorp BE compared to YourCorp US

To facilitate services selection, services are grouped under different service groups.

When developing an employee portal integration, it is possible to limit the list of services exposed to an employee and only show a subset of the list displayed to a user. Limiting the list for the employee is facilitated by using "Labels" that need to be setup in the configuration.

A label is a virtual group of services that you can used to retrieve only a subset of the service list.

## Discovering configuration information

The MyHRW companies (countries) you will have to map can be provided by the MyHRW administration team or you can discover them using your application key and by calling the different APIs.

Use: 

1. `GET api/applications/current` to retrieve your associated agent id (see [Get current application API](/docs/API_GetCurrentApplication))
2. `GET api/companies` to retrieve all companies for which your application can create ticket (see [Get companies API](/docs/API_GetCompanies))
3. `GET api/companies/{companySkillId}/servicegroups` to retrieve the list of service groups associated with a company (see [Get service group API](/docs/API_GetServiceGroups))   
4. `GET api/companies/{companySkillId}/services` to retrieve the list of services associated with a company (see [Get service API](/docs/API_GetServices))  
5. `GET api/companies/{companySkillId}/privacies` to retrieve the list of privacy skills that can be use when adding a file (see [Get privacy skills API](/docs/API_GetPrivacies))
6. `GET api/companies/{companySkillId}/messageTypes` to retrieve the list of available message types to use when employee wants to send an update on an existing ticket (see [Get message types API](/docs/API_GetMessageTypes))

## Create a ticket

When an employee creates a ticket from the Inbox, he or she has to specify a minimum of arguments which are service, short description and description. 
The API takes care of setting the source skill automatically following the aivailable customer configuration.
All other mandatory fields, such as priority, will be set by the Agent when he or she will take ownership of the ticket created in MyHRW.

To create a ticket from an Inbox see [Create ticket for Inbox API](/docs/API_CreateTicket_Inbox) for details.

## Get ticket

To display information of a specific ticket, you can call the Get ticket API see [Get ticket API](/docs/API_GetTicket)

## Get employee tickets

To retrieve tickets created by an employee and that are open or closed, you can use the Get emplyee tickets API see [Get employee tickets API](/docs/API_GetEmployeeTickets)

## Work with ticket files

Files can be attached to a ticket, listed and retrieved. 

* To attach a file to a ticket see [Upload file to ticket API](/docs/API_UploadFile.md)
* To retrieve the list of files attached to a ticket see [Get ticket files API](/docs/API_GetTicketFiles.md)
* To download a file attached to a ticket see [download file API](/docs/API_DownloadFile)

## Send message on ticket

To send a message from the Inbox to an open ticket see the [Send message API](/docs/API_SendMessage)

To retrieve messages exchanged between the requester and the service center agent see the [Get ticket communications API](/docs/API_GetCommunications). 
Always use the "forinbox=true" parameter to avoid showing agent to agent communications. Also ensure that emails send to or received from the requester are included in the returned communications. 

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)