

<img src="../../assets/images/beans-128x128.png" align="right" />

# Assignees Managements



For details of an assignee's shape please see https://www.beansroute.ai/route-api-v1.php#assignee-list-object


## Table of contents
- [Create Assignees](#create-assignees)
- [Update Assignee](#update-assignee)
- [Get Assignee List](#get-assignee-list)
- [Get Assignee](#get-assignee)

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

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/assignees/{{list-assingee-id}}
```

**Response Example**

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

