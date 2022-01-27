

<img src="../assets/images/beans-128x128.png" align="right" />

# Vehicles routing optimization with shift time

![Stops](assets/images/stops.png)

As we have more and more partners working together, we'll start to schedule working hours in order to keep the business running efficiently.

We've previously talked about [packages delivering with time window](https://github.com/beansai/beans-tutorials/tree/main/dynamic-routes-optimization/vehicles-routing-optimization-with-time-windows), and in this tutorial we'll include a time shift factor.

Let's assume we have two drivers who need to deliver 6 packages... which we can see from the map above.

- Driver One - Starts work at 07:00 for 4 hours.
- Driver Two - Starts work at 13:00 for 4 hours.
- Left side of the map - Packages needing to be delivered in the morning.
- Right side of the map - Packages needing to be delivered in the afternoon.


## Table of contents
- [Vehicles routing optimization with shift time](#vehicles-routing-optimization-with-shift-time)
  - [Table of contents](#table-of-contents)
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
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses -XPOST -d '{"warehouse":[{"list_warehouse_id":"cabb46d6-776a-11ec-90d6-0242ac120003","address":"401 Superior Way, Discovery Bay, CA 94505"}]}'
```

- It is important to set list_warehouse_id to a value that is unique within your account.

```json
{
  "warehouse": [
    {
      "listWarehouseId": "cabb46d6-776a-11ec-90d6-0242ac120003",
      "accountBuid": "{{your-account-buid}}",
      "address": "401 Superior Way, Discovery Bay, CA 94505"
    }
  ]
}
```

**Note**: Your account_buid, list_warehouse_id, address will e different from the example

### Create a route

A grouping Route is not required for optimization, but it is a convenient way to 'bucket' stops that will be optimized.

**Request example**

```
curl -k -H 'Authorization: <token>' -X POST 'https://isp.beans.ai/enterprise/v1/lists/routes' -d '{"route":[{"name":"Tu Route ea29","warehouse":{"list_warehouse_id":"cabb46d6-776a-11ec-90d6-0242ac120003"},"list_route_id":"e6d3785d-ffb0-40f6-b1c4-00793bb276f1","status":"OPEN","date_str":"2023-01-10"}]}'
```

- It is important to set list_route_id to a value that is unique within your account
- It is important to confgure date_str with the yyyy-MM-dd format

```json
{
    "route":[
        {
            "name": "Tu Route ea29",
            "warehouse":
            {
                "list_warehouse_id": "cabb46d6-776a-11ec-90d6-0242ac120003"
            },
            "list_route_id": "e6d3785d-ffb0-40f6-b1c4-00793bb276f1",
            "status": "OPEN",
            "date_str": "2023-01-10"
        }
    ]
}
```

**Note**: Your list_warehouse_id, list_route_id will be different from the example

### Add stops to the route

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/items -XPOST --data '@assets/stops.json'
```

- The file[assets/stops.json](assets/stops.json) contains 6 stops in a few cities in California

- An important thing to note is that each stop contains the route reference to the route that was created above with route id `e6d3785d-ffb0-40f6-b1c4-00793bb276f1`

Here's a visualization of the stops with a warehouse ( the big black dot in the middle ) we just created.

![stops](assets/images/stops.png)

### Configure assignees

Here's how to configure one driver for delivering.

**Request**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/assignees -XPOST -d '{"assignee":[{"list_assignee_id":"tu1-tutorial-driver-1","name":"Driver One"},{"list_assignee_id":"tu1-tutorial-driver-2","name":"Driver Two"}]}'
```

- list_assignee_id should be unique within your account.

```json
{
  "assignee": [
    {
      "list_assignee_id": "tu1-tutorial-driver-1",
      "name": "Driver One"
    },
    {
      "list_assignee_id": "tu1-tutorial-driver-2",
      "name": "Driver Two"
    }
  ]
}
```

**Note**: Your list_assignee_id will be different from the example

### Run stateless DRO

**The Simple Scenario consists of**

- 6 stops from the above Route `e6d3785d-ffb0-40f6-b1c4-00793bb276f1`
- Driver shift length is 4 hours.
- Driver one's shift start time is at 07:00.
- Driver two's shift start time is at 13:00.

The configurations for above are in [assets/stateless-dro-request](assets/stateless-dro-request.json) The partial configuration is:

```json
    "assignee_with_vehicle":
    [
        {
            "list_assignee_id": "tu1-tutorial-driver-1",
            "shift_start_time": "07:00"
        },
        {
            "list_assignee_id": "tu1-tutorial-driver-2",
            "shift_start_time": "13:00"
            
        }
    ],
    "default_shift_length": 4
```

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -X POST --data '@assets/stateless-dro-request.json'
```

**Note**: The above assumes that the file `assets/stateless-dro-request.json` is relative to where cURL is run. The `--data '@xxx'` option instructs cURL to read the file as the body of the POST request.

**Response example**
You can find the sample response at [assets/stateless-dro-response.json](assets/stateless-dro-response.json) You can see the result with multiple segments ( assignee with packages )

Here's a visualization of the map. We can find the stop visiting sequence is related to the time window and shift time.

![DRO Result](assets/images/dro-result.png)



