

<img src="../../assets/images/beans-128x128.png" align="right" />

# Assignees Managements



For details of an assignee's shape please see https://www.beansroute.ai/route-api-v1.php#assignee-list-object


## Table of contents
- [Create Assignees](#create-assignees)
- [Update Assignee](#update-assignee)
- [Get Assignee List](#get-assignee-list)
- [Get Assignee](#get-assignee)
- [Delete Assignee](#delete-assignee)
- [Objects](#objects)
  - [Array of Assignee Object](#array-of-assignee-object)
  - [Assignee Object](#assignee-object)

### Create Assignees

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/assignees
```

**Body**

- disable_invite_communication - whether or not to send an email to inform the driver.

For more detail on ListAssignee please see https://www.beansroute.ai/route-api-v1.php#assignee-list-object

```json
{
  "assignee": [
    {
      "list_assignee_id": "tu1-tutorial-driver-1",
      "name": "Driver One",
      "email": "integrator@beans.ai",
      "role": "DRIVER",
      "disable_invite_communication": false,
    },
    {
      "list_assignee_id": "tu1-tutorial-driver-2",
      "name": "Driver Two"
    }
  ]
}
```

**Response Example**

```json
{
    "assignee": [
        {
            "listAssigneeId": "tu1-tutorial-driver-1",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Driver One",
            "code": "cd787cc3-fd8",
            "createdAt": 1642408164000,
            "updatedAt": 1643091861000,
            "state": "ACTIVE",
            "role": "DRIVER"
        },
        {
            "listAssigneeId": "tu1-tutorial-driver-2",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Driver Two",
            "code": "580d9ce4-8bd",
            "createdAt": 1642408164000,
            "updatedAt": 1642408164000,
            "state": "ACTIVE",
            "role": "DRIVER"
        }
    ]
}
```

### Update Assignee

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/assignees/{{list-assingee-id}}
```

**Body**

```json
{
    "name": "New Driver 2",
    "code": "c514dabe-091",
    "state": "ACTIVE",
    "role": "DRIVER",
    "employeeId": "2000001",
    "listWarehouseId": "lzt6vwxta2o0e1hsl9k75u"
}
```

### Get Assignee List

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/assignees
```

**Response Example**

```json
{
    "assignee": [
        {
            "listAssigneeId": "cadriver01",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "CA Driver 1",
            "email": "idon.chen.tw+32@gmail.com",
            "phone": "+886910000002",
            "code": "d38fdd7c-494",
            "createdAt": 1641885208000,
            "updatedAt": 1642405990000,
            "state": "DISABLED",
            "role": "DRIVER",
            "employeeId": "CA2000003",
            "listWarehouseId": "p9cc427x07b3pflmzv556rca01"
        },
        {
            "listAssigneeId": "cadriver02",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "CA Driver 2",
            "email": "idon.chen.tw+33@gmail.com",
            "phone": "+886910000002",
            "code": "5b6bb7f9-1f3",
            "createdAt": 1641885498000,
            "updatedAt": 1642405995000,
            "state": "DISABLED",
            "role": "DRIVER",
            "employeeId": "CA2000005",
            "listWarehouseId": "p9cc427x07b3pflmzv556rca01"
        }
    ]
}
```

### Get Assignee

**Request**

```
GET https://isp.beans.ai/enterprise/v1/lists/assignees/{{list-assingee-id}}
```

**Response**

```json
{
    "listAssigneeId": "cadriver01",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "name": "CA Driver 1",
    "email": "idon.chen.tw+32@gmail.com",
    "phone": "+886910000002",
    "code": "d38fdd7c-494",
    "createdAt": 1641885208000,
    "updatedAt": 1642405990000,
    "state": "DISABLED",
    "role": "DRIVER",
    "employeeId": "CA2000003",
    "listWarehouseId": "p9cc427x07b3pflmzv556rca01"
}
```

### Delete Assignee
This will perform a soft-delete action, and the deleted object will appear in get assignees and get assignee by assigneeId response with state "DISABLED"

**Request**
```
DELETE {{baseURL}}/enterprise/v1/lists/assignees/{{list-assignee-id}}
```

**Response**
```json
{
    "listAssigneeId": "1qaqac9nrq1hxk0tdfga1gs",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "name": "Tourist 001",
    "email": "donchen+t101@beans.ai",
    "phone": "+886963111111",
    "code": "087599df-943",
    "createdAt": 1645164735000,
    "updatedAt": 1646121729000,
    "state": "DISABLED",
    "hasUsedConsumerApp": true,
    "role": "DRIVER",
    "safetyStatus": "UNKNOWN",
    "safetyIntegrationStatus": "PENDING",
    "isAssigningEnabled": true
}
```

## Objects
### Array of Assignee Object
| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **assignee** | Array of Assignee Object | [] | A list of Assignee Object |

### Assignee Object
| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | string | The assignee ID | The unique id of the assignee |
| **account_buid** | string | The account ID | The account ID that this assignee is in |
| **name** | string | "" | The name of this assignee |
| **email** | string | "" | The email of this assignee |
| **phone** | string | "" | The phone number of this assignee |
| **code** | string | "" | The assignee code, if configured |
| **lat** | double | 0.0 | The last known latitude of this assignee |
| **lng** | double | 0.0 | The last known longitude of this assignee |
| **state** | string | One of ACTIVE, DISABLED | The state that this assignee is in |
| **has_used_consumer_app** | boolean | false | True when the assignee has used the consumer app |
| **role** | string | One of ADMIN, DRIVER, MANAGER, DISPTCHER | The Role of this assignee  |
| **employee_id** | string | "" | The employee ID of this assignee |
| **manager_assignee_id** | string | "" | The assignee's manager ID |
| **list_warehouse_id** | string | "" | The assignee's default warehouse ID |
| **is_safety_enabled** | boolean | false | True when safety compliance is enabled for this assignee |
| **safety_status** | string | "" | The safety compliance status |
| **safety_integration_status** | string | "" | The safety provider integration status for this assignee |
| **is_assigning_enabled** | boolean | false | True when the assignee can be put on a route |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is last updated |


