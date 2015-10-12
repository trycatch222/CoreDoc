# Get companies assigned to the current agent
```
GET /api/companies
```
* [Description](#description)
* [Response](#response)
* [Security group](#security-group)

## Description

Allows you to retrieve skills assigned to your API user (agent).

Based on your message header:

* If you call the API having only a application token/key, it return the companies for that token.
* If you call the API with a correct authenticated agent token/key for this paricular agent.

In the returned properties for a company, the **skillid** is the company skill id requested in many other API calls. Be careful not use the field "id" in other calls.

## Response

| Value             | Type    | Description                   | Remarque                                  |
|-------------------|---------|-------------------------------|-------------------------------------------|
| id                | integer | Company unique id             | Used only internaly, not in the api calls |
| name              | string  | company name                  | -                                         |
| organisationId    | integer | organization unique id        | -                                         |
| organisationName  | string  | organization name             | -                                         |
| **skillid**       | integer | **company skill id**          | **unique id used in all other API calls** |
| email             | string  | company email                 | used for the survey only                  |
| country           | string  | ISO country code in 2 letters |	-										                      |

Example: Returned values for an agent allowed to work for 3 companies

```json
[{
  "id": 1791,
  "name": "YourCorp BE",
  "organisationId": 209,
  "organisationName": "YourCorp",
  "skillId": 26943,
  "email": "company@YCP_BE.com",
  "country": "BE"
}, {
  "id": 1799,
  "name": "YourCorp MX",
  "organisationId": 209,
  "organisationName": "YourCorp",
  "skillId": 26959,
  "email": "company@YCP_MX.com",
  "country": ""
}, {
  "id": 1801,
  "name": "YourCorp US",
  "organisationId": 209,
  "organisationName": "YourCorp",
  "skillId": 26963,
  "email": "company@YCP_US.com",
  "country": "US"
}]
```

## Security group

API security group: **CompanyConfig**

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)
