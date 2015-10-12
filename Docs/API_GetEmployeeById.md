# Get employee by ID
```
POST /api/companies/{companySkillId}/employees/{employeeId}
```
* [Description](#description)
* [Parameter](#parameters)
* [Response](#response)
* [Security group](#security-group)

## Description

Returns the information for an employee searched by id. MyHRw performs the search in the HRIS system connected to the company. (Also called the employee configured backend system)

The various information returned depends on the configuration and can vary for each company.

Always returns only one employee

## Parameters

| Parameter       | Type    | Description             | Remark                                |
|-----------------|---------|-------------------------|---------------------------------------|
| companySkillId  | integer | MyHrw company skill id  | -                                     |
| employeeId      | string  | Employee id (HRIS)      | The employee id used is the HRIS one  |


## Response

| Value             | Type      | Description                                                 | Remark                                        |
|-------------------|-----------|-------------------------------------------------------------|-----------------------------------------------|
| id                |string     | Employee unique id                                          | -                                             |
| firstName         |string     | First name                                                  | -                                             |
| lastName          |string     | Last name                                                   | -                                             |
| email             |string     | Email address                                               | -                                             |
| company           |collection | Information about the MyHRW company of that employee        | -                                             |
| employeeInfo      |collection | Various information returned on about the employee          | Optional, based on the backend configuration  |
| skills            |collection | Specific skills and there possible values for that employee | Optional, based on the backend configuration  |
| securityQuestions |collection | Sercurity question & response                               | Optional, based on the backend configuration  |
| source            |string     | Logical name given to that backend/HRIS system connector    | -                                             |
| backendType       |string     | Type of backend                                             | -                                             |

Example

```json
{
  "id": "patrickg",
  "firstName": "Patrick",
  "lastName": "Grey",
  "email": "patrick.grey@yourcorp.com",
  "company": {
    "id": 0,
    "name": "YourCorp BE",
    "organisationId": 0,
    "skillId": 26943
  },
  "employeeInfo": [{
    "name": "street",
    "defaultLabel": "Street",
    "translationId": 6,
    "value": "Rue de Waremme",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "housenumber",
    "defaultLabel": "House Number",
    "translationId": 7,
    "value": "5",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "postalcode",
    "defaultLabel": "Postal Code",
    "translationId": 8,
    "value": "4300",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "city",
    "defaultLabel": "City",
    "translationId": 9,
    "value": "Huy",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "birthdate",
    "defaultLabel": "Date of birth",
    "translationId": 10,
    "value": "20140317",
    "valueType": "DATE",
    "customField": ""
  }],
  "skills": [],
  "securityQuestions": [{
    "id": 4936,
    "question": "What is your birth date?",
    "answer": "20140317"
  }, {
    "id": 4935,
    "question": "What is your address house number?",
    "answer": "5"
  }, {
    "id": 4934,
    "question": "What is your address street name?",
    "answer": "Rue de Waremme"
  }, {
    "id": 4933,
    "question": "What is your postal code?",
    "answer": "4300"
  }],
  "source": "TP2",
  "backendType": "Oracle"
}
```
## Security group

API security group: **EmployeeSearch**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)