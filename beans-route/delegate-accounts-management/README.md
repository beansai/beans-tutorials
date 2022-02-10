

<img src="../../assets/images/beans-128x128.png" align="right" />

# Delegate Accounts

A delegated account is a Beans Route account that are created and delegated by another Beans Route Account.

For example, ACME shipping company (delegator) would partner with Brainiac Delivery service (delegated) to service the customers in an area. ACME shipping company, having a Beans Route account, could create a delegated account for Brainiac Delivery service so Brainiac Delivery service could use features offered by Beans Route.

As we are in the world of APIs, Beans Route provides RPC (remote procedure calls) on its secured and scalable service platforms. Beans Route's JSON payload on HTTPS protocol is a powerful integration point for workflows running across organizational boundaries!



## Table of contents

- [Delegate Accounts Managerment](#delegate-accounts-management)
  - [Terms](#terms)
  - [Prerequisites on the Delegator](#prerequisties-on-the-delegator)
  - [API Examples](#api-examples)
    - [Create a Delegated Account](#create-a-delegated-account)
    - [Get Delegated Account-List](#get-delegated-account-list)
    - [On behalf of](#on-behalf-of)



## Terms

- Delegator - the account with an authentication and with authorization to create and manage other accounts
- Delegated account - an account that is created by a delegator
- On behalf of - the activity that is performed by the delegator (with delegator's authorization) to read/update information on the delegated account



## Prerequisites on the Delegator

Please contact Beans team to enable the delegator role.



## API Examples

### Create a delegated account

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/delegated_account
```

**Body**

```json
{
  "owner": {
    "name": "Don Delegator Owner 10",
    "email": "donchen+delegator-10@beans.ai",
    "phone": "650-555-1231",
    "password": "donchen10"
  },
  "name": "Delegator Logistics 10",
  "timezone": "America/New_York",
  "country_iso3": "USA",
  "id": "delegator-10"
}
```

- owner ( Required ) - The owner of the delegated account, must be specified
  - name ( Optional ) - The full name of the owner
  - email ( Required ) - The email of the owner account for Beans Route login.
  - phone ( Optional ) - The phone # of the owner, optional, though strongly recommended
  - password ( Required )- The password of owner account for Beans Route login.
- name ( Optional ) - The name of the delegated account
- timezone - ( Optional )
  The timezone of the delegated account, e.g. America/New_York
  If this is not specified, the delegator account's timezone, if specified would be used, 
  and if delegator account does not have a timezone, this would be set to America/Los_Angeles
- country_iso3 ( Optional ) - The ISO3 code for the country, default is USA
- id ( Optional ) - The reference ID in the delegator's system for cross reference

**Response Example**

```json
{
    "accountBuid": "35138aee-b003-3ac9-ba7a-9c8bca9eb906",
    "email": "donchen+delegator-10@beans.ai",
    "subscriptionPlan": "beans_routes-free-trial-01",
    "createdAt": 1644478996220,
    "updatedAt": 1644478996220,
    "accountName": "Delegator Logistics 10",
    "tags": [
        {
            "key": "/ACCOUNT/DEFAULT/TIMEZONE_ID",
            "value": "America/New_York"
        },
        {
            "key": "/ACCOUNT/DELEGATOR",
            "value": "4022a1aada0e4c4684e61e3f73290a68"
        },
        {
            "key": "/ACCOUNT/DELEGATOR/REFID",
            "value": "delegator-10"
        },
        {
            "key": "/ACCOUNT/ROUTE/PREFERENCE/USE_BEANS_SEQUENCING",
            "value": "true"
        }
    ]
}
```

- accountBuid - This is the unique identifier in Beans Route for this account
- email - The email address of the owner
- subscriptionPlan - The subscription plan of the account, this is inherited from the delegator
- createdAt - Epoch in milliseconds on when this account was created
- updatedAt - Epoch in milliseconds on when this account was updated
- accountName - The name of the account
- tag of key "/ACCOUNT/DELEGATOR"
  - value is the account ID of the delegator
- tag of key "/ACCOUNT/DELEGATOR/REFID"
  - value is the reference ID as specified



### Get Delegated Account List

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/delegated_account
```

**Response Example**

```json
{
    "accounts": [
        {
            "accountBuid": "35138aee-b003-3ac9-ba7a-9c8bca9eb906",
            "email": "donchen+delegator-10@beans.ai",
            "subscriptionPlan": "beans_routes-free-trial-01",
            "createdAt": 1644478996000,
            "updatedAt": 1644478996000,
            "accountName": "Delegator Logistics 10",
            "tags": [
                {
                    "key": "/ACCOUNT/DEFAULT/TIMEZONE_ID",
                    "value": "America/New_York"
                },
                {
                    "key": "/ACCOUNT/DELEGATOR",
                    "value": "4022a1aada0e4c4684e61e3f73290a68"
                },
                {
                    "key": "/ACCOUNT/DELEGATOR/REFID",
                    "value": "delegator-10"
                },
                {
                    "key": "/ACCOUNT/ROUTE/PREFERENCE/USE_BEANS_SEQUENCING",
                    "value": "true"
                }
            ]
        },
        {
            "accountBuid": "593522e9-7b41-310a-bde7-9d160c5daf7e",
            "email": "don.chen@beans.ai",
            "subscriptionPlan": "beans_routes-free-trial-01",
            "createdAt": 1644478071000,
            "updatedAt": 1644478071000,
            "accountName": "Brainiac Delivery",
            "tags": [
                {
                    "key": "/ACCOUNT/DEFAULT/TIMEZONE_ID",
                    "value": "America/New_York"
                },
                {
                    "key": "/ACCOUNT/DELEGATOR",
                    "value": "4022a1aada0e4c4684e61e3f73290a68"
                },
                {
                    "key": "/ACCOUNT/DELEGATOR/REFID",
                    "value": "acme-40081dd3"
                },
                {
                    "key": "/ACCOUNT/ROUTE/PREFERENCE/USE_BEANS_SEQUENCING",
                    "value": "true"
                }
            ]
        }
    ]
}
```



### On Behalf Of

To read/update information on the delegated account, the only change is adding HTTP Header

```
X-Beansai-On-Behalf-Of: <delegated_account's accountBUID>
```

One can obtain the accountBUID of the delegated account via [Get Delegated Account List](#get-delegated-account-list) for API request calls.

