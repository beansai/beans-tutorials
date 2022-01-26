

<img src="../assets/images/beans-128x128.png" align="right" />

# Vehicles routing optimization with pickups dropoffs

![Stops](assets/images/stops.png)

The above map is a common scenario of delivery service.
There are some packages on the left-hand side to pick up which we need to deliver to the right-hand side.
Let's see how to configure the packages for pairing up pickups and dropoffs.


## Table of contents
- [Create the data](#create-the-data)
  - [Create a warehouse](#create-a-warehouse)
  - [Create a route](#create-a-route)
  - [Add stops to the route](#add-stops-to-the-route)
  - [Configure assignees](#configure-assignees)
- [Run stateless DRO](#run-stateless-dro)



## Create the data
### Create a warehouse

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses -XPOST -d '{"warehouse":[{"list_warehouse_id":"7bc71186-9d6f-4541-a1b3-ffcfe0b6234f","address":"14840 CA-4, Discovery Bay, CA 94505"}]}'
```

- It is important to set list_warehouse_id that is unique in your account.

```json
{
  "warehouse": [
    {
      "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
      "accountBuid": "{{your-account-buid}}",
      "address": "14840 CA-4, Discovery Bay, CA 94505"
    }
  ]
}
```

**Note**: Your account_buid, list_warehouse_id, address would be differ.

### Create a route

A grouping Route, although isn't required for optimization, is a convenient bucket to gather
stops to be optimized.

**Request example**

```
curl -k -H 'Authorization: <token>' -X POST 'https://isp.beans.ai/enterprise/v1/lists/routes' -d '{"route":[{"name":"Tu Route ea29","warehouse":{"list_warehouse_id":"7bc71186-9d6f-4541-a1b3-ffcfe0b6234f"},"list_route_id":"9d0b5ee9-fa02-4d6e-8633-f7980b225ae1","status":"OPEN","date_str":"2023-01-10"}]}'
```

- It is important to set the list_route_id that is unique in your account
- It is important to confgure the date_str with yyyy-MM-dd format

```json
{
    "route":[
        {
            "name": "Tu Route 9d0b",
            "warehouse":
            {
                "list_warehouse_id": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f"
            },
            "list_route_id": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1",
            "status": "OPEN",
            "date_str": "2023-01-10"
        }
    ]
}
```

**Note**: Your list_warehouse_id, list_route_id would be differ.

### Add stops to the route

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/items -XPOST --data '@assets/stops.json'
```

- You will find file [assets/stops.json](assets/stops.json) containing 8 stops in a city.
- An important thing to note is that each stop contains the route reference to the route that was created above with route id `ea2928e6-2548-412b-8b19-7f1043324ec3`

A pickup-dropoff pair example.

We have two different type of stops with a same tracking_id `9d0b-001`

```java
    {
      "list_item_id": "9d0b-a801b3605afbd726df743cc66",
      "address": "3365 Deer Valley Rd, Antioch, CA 94531",
      "route": {
        "list_route_id": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1"
      },
      "type":"PICKUP",
      "tracking_id":"9d0b-001"
    },
    {
      "list_item_id": "9d0b-8eca53fefb635f19958ab0cbf",
      "address": "4320 E Summer Lake Dr, Oakley, CA 94561",
      "route": {
        "list_route_id": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1"
      },
      "type":"DROPOFF",
      "tracking_id":"9d0b-001"
    }
```

Here's the visualization of the stops with a warehouse we created.

![stops](assets/images/stops.png)

### Configure assignees

To configure one driver for delivering.

**Request**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/assignees -XPOST -d '{"assignee":[{"list_assignee_id":"tu1-tutorial-driver-1","name":"Driver One"}]}'
```

- list_assignee_id should be unique in your account.

```json
{
  "assignee": [
    {
      "list_assignee_id": "tu1-tutorial-driver-1",
      "name": "Driver One"
    }
  ]
}
```

**Note**: Your list_assignee_id should be differ.

### Run stateless DRO

**The Simple Scenario consists of**

- 4 pickup-dropoff paired stops from the Route `9d0b5ee9-fa02-4d6e-8633-f7980b225ae1` above
- One driver.
- Enable pickup dropoff mode.

The respective configurations for the above is at [assets/stateless-dro-request](assets/stateless-dro-request.json)  where the partial configuration is

```json
"disallow_pickup_dropoff_mode": false
```

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -X POST --data '@assets/stateless-dro-request.json'
```

**Note**: the above assumes that the file `assets/stateless-dro-request.json` is relative to where the cURL is run. The `--data '@xxx'` option instructed cURL to read the file as the body of the POST request.

**Response example**
You can find the sample response at [assets/stateless-dro-response.json](assets/stateless-dro-response.json) where you can see the result with multiple segments ( assignee with packages )

Here's a visualization of map, we can find the stops' visiting sequence are related to the time window.

![DRO Result](assets/images/dro-result.png)



