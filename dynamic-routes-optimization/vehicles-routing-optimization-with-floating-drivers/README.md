

<img src="../assets/images/beans-128x128.png" align="right" />

# Vehicles routing optimization with floating drivers

![Stops](assets/images/stops.png)

Sometimes we want to be flexible for the rapid changes in business or we want to plan in advance without assignning a particular driver for the tasks.

Let's assume that we have received a manifest of delivering 95 packages for the day with 3 drivers who will work for 4 hours a day and 3 trucks with different capacities.

- Car One - capacity of 10
- Car Two - capacity of 50
- Car Three - capacity of 50
- Three drivers - each works 4 hours a day.


## Table of contents
- [Create the data](#create-the-data)
  - [Create a warehouse](#create-a-warehouse)
  - [Create a route](#create-a-route)
  - [Add stops to the route](#add-stops-to-the-route)
- [Run stateless DRO](#run-stateless-dro)

## Create the data
### Create a warehouse

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses -XPOST -d '{"warehouse":[{"list_warehouse_id":"cabb46d6-776a-11ec-90d6-0242ac120003","address":"401 Superior Way, Discovery Bay, CA 94505"}]}'
```

- It is important to set list_warehouse_id that is unique in your account.

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

**Note**: Your account_buid, list_warehouse_id, address would be differ.

### Create a route

A grouping Route, although isn't required for optimization, is a convenient bucket to gather
stops to be optimized.

**Request example**

```
curl -k -H 'Authorization: <token>' -X POST 'https://isp.beans.ai/enterprise/v1/lists/routes' -d '{"route":[{"name":"Tu Route ea29","warehouse":{"list_warehouse_id":"cabb46d6-776a-11ec-90d6-0242ac120003"},"list_route_id":"f07d7425-1776-4abc-9790-35cb1a0696aa","status":"OPEN","date_str":"2023-01-10"}]}'
```

- It is important to set the list_route_id that is unique in your account
- It is important to confgure the date_str with yyyy-MM-dd format

```json
{
    "route":[
        {
            "name": "Tu Route 1d8e",
            "warehouse":
            {
                "list_warehouse_id": "cabb46d6-776a-11ec-90d6-0242ac120003"
            },
            "list_route_id": "f07d7425-1776-4abc-9790-35cb1a0696aa",
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

- You will find file [assets/stops.json](assets/stops.json) containing 95 stops in couples of cities in Califonia

- An important thing to note is that each stop contains the route reference to the route that was created above with route id `f07d7425-1776-4abc-9790-35cb1a0696aa`

Here's a visualization of the stops with a warehouse ( the big black dot in the middle ) we just created.

![stops](assets/images/stops.png)

### Run stateless DRO

**The Simple Scenario consists of**

- 95 stops from the Route `f07d7425-1776-4abc-9790-35cb1a0696aa` above
- Three drivers/vehicles with different capicities
- Each driver's shift length is 4 hours
- Each driver will start to work at 07:00

The respective configurations for the above is at [assets/stateless-dro-request](assets/stateless-dro-request.json)  where the partial configuration is

```json
    "assignee_with_vehicle":
    [
        {
            "list_assignee_id": "extra-driver-0",
            "capacity": 10
        },
        {
            "list_assignee_id": "extra-driver-1",
            "capacity": 50
        },
        {
            "list_assignee_id": "extra-driver-2",
            "capacity": 50
        }
    ],
    "default_shift_start_time": "07:00",
    "default_shift_length": 4
```

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -X POST --data '@assets/stateless-dro-request.json'
```

**Note**: the above assumes that the file `assets/stateless-dro-request.json` is relative to where the cURL is run. The `--data '@xxx'` option instructed cURL to read the file as the body of the POST request.

**Response example**
You can find the sample response at [assets/stateless-dro-response.json](assets/stateless-dro-response.json) where you can see the result with multiple segments ( assignee with packages )

A visualization of the assignment

![Floating drivers](assets/images/floating-drivers.png)

A visualization of the optimized routes.

![DRO Result](assets/images/dro-result.png)



