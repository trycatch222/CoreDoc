# Search employee ticket
```
POST /api/companies/{companySkillId}/employees/search
```
* [Description](#description)
* [Parameter](#parameters)
* [Body](#body)
* [Response](#response)
* [Security group](#security-group)

## Description

Search for an employee in the HRIS system connected to the company. (Also called the employee configured backend system). The various EE data returned depends on the configuration and can vary for each company.

Returns a collection of matching employees.

Employee can be searched by

* Email address
* First name, last name or both

Also

* All criterias accept wildcard search. If no wildcard is specified the search returns only the exact match.
* Search is case insensitive.
* Wildcard search criteria should be at least 3 characters long including the * e.g. "Pa*" is accepted, "P*" is refused.


Search examples for employee matching:

* First name = pat\*
* First name = pat\* and last name = gra\*
* Last name =  gray
* Email = patrick.gray@yourcorp.be
* Email = \*@yourcorp.be

## Parameters

| Parameter       | Type    | Description             | Remark  |
|-----------------|---------|-------------------------|---------|
| companySkillId  | integer | MyHRW company skill id  | -       |

## Body

Content-Type: application/json

| Value     | Type    | Description | Remark  |
|-----------|---------|-------------|---------|
| firstName | string  | first name  | -       |
| lastName  | string  | last name   | -       |
| email     | string  | email       | -       |

Example 1 (search for First name = pat\* and last name = gra\*)

```json
{
  "firstName":"pat*",
  "lastName":"gra*"
}
```

Example 2 (search for employee with email patrick.gray@yourcorp.be)

```json
{
  "email":"patrick.gray@yourcorp.be"
}
```

## Response

| Value             | Type                | Description                                                 | Remark                                        |
|-------------------|---------------------|-------------------------------------------------------------|-----------------------------------------------|
| id|string         | Employee unique id  |                                                             | -                                             |
| firstName         | string              | First name                                                  | -                                             |
| lastName          | string              | Last name                                                   | -                                             |
| email             | string              | Email address                                               | -                                             |
| company           | collection          | Information about the MyHRW company of that employee        | Based on the configured backend security, the employees returned can be from  another company of the same organization  |
| employeeInfo      | collection          | Various information returned on about the employee          | Optional, based on the backend configuration  |
| skills            | collection          | Specific skills and there possible values for that employee | Optional, based on the backend configuration  |
| securityQuestions | collection          | Sercurity question & response                               | Optional, based on the backend configuration  |
| source            | string              | Logical name given to that backend/HRIS system connector    | -                                             |
| backendType       | string              | Type of backend                                             | -                                             |

Example

```json
[{
  "id": "johnz",
  "firstName": "John",
  "lastName": "Zorro",
  "email": "john.brice@yourcorp.com",
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
    "value": "blablabla",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "housenumber",
    "defaultLabel": "House Number",
    "translationId": 7,
    "value": "455",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "postalcode",
    "defaultLabel": "Postal Code",
    "translationId": 8,
    "value": "4500",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "city",
    "defaultLabel": "City",
    "translationId": 9,
    "value": "Lasnes",
    "valueType": "NVARCHAR2",
    "customField": ""
  }, {
    "name": "birthdate",
    "defaultLabel": "Date of birth",
    "translationId": 10,
    "value": "19650414",
    "valueType": "DATE",
    "customField": ""
  }],
  "skills": [],
  "securityQuestions": [{
    "id": 4936,
    "question": "What is your birth date?",
    "answer": "19650414"
  }, {
    "id": 4935,
    "question": "What is your address house number?",
    "answer": "455"
  }, {
    "id": 4934,
    "question": "What is your address street name?",
    "answer": "blablabla"
  }, {
    "id": 4933,
    "question": "What is your postal code?",
    "answer": "4500"
  }],
  "source": "TP2",
  "backendType": "Oracle"
}, {
  "id": "johnb",
  "firstName": "John",
  "lastName": "Brice",
  "email": "john.brice@yourcorp.com",
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
}]
```

## Security group

API security group: **EmployeeSearch**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
