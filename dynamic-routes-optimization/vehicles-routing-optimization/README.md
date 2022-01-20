

<img src="../assets/images/beans-128x128.png" align="right" />

# Vehicles routing optimization

![Stops](assets/images/stops.png)

For drivers who are working at a logistic company, a common daily life would be gathering at warehouse , loading  packages to the truck, visiting locations to pickup/dropoff packages then go back to the warehouse at last.

This is an example of how to optimize the routes for drivers to complete all the deliveries as soon as possible with DRO.

We can also see routes optimizations with different constraints.

- [Capacity constraint](https://github.com/beansai/beans-tutorials/tree/main/dynamic-routes-optimization/vehicles-routing-optimization-with-capacity-constraint) which vehicles have maximum capacities for items they can carry.
- [Time windows](https://github.com/beansai/beans-tutorials/tree/main/dynamic-routes-optimization/vehicles-routing-optimization-with-time-windows) which locations need to be visit in specfic time window.

## Table of contents
- [Create the data](#create-the-data)
  - [Create a warehouse](#create-a-warehouse)
  - [Create a route](#create-a-route)
  - [Add stops to the route](#add-stops-to-the-route)
  - [Configure assignees](#configure-assignees)
- [Run stateless DRO](#run-stateless-dro)



## Vehicles routing optimization with DRO

The following example will show how to do vehicles routing optimizations with DRO

### Create the data

#### Create a warehouse

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses -XPOST -d '{"warehouse":[{"list_warehouse_id":"d0686fa0-c24b-40c1-b81f-0615bfa3718a","address":"5655 Hood Way, Tracy, CA 95377"}]}'
```

- It is important to set list_warehouse_id that is unique in your account.

```json
{
  "warehouse": [
    {
      "listWarehouseId": "cabb46d6-776a-11ec-90d6-0242ac120003",
      "accountBuid": "{{your-account-buid}}",
      "address": "5655 Hood Way, Tracy, CA 95377"
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
curl -k -H 'Authorization: <token>' -X POST 'https://isp.beans.ai/enterprise/v1/lists/routes' -d '{"route":[{"name":"Tutorial Route A","warehouse":{"list_warehouse_id":"cabb46d6-776a-11ec-90d6-0242ac120003"},"list_route_id":"eab60a1e-f773-480f-87b5-1f968a1a26b9","status":"OPEN","date_str":"2023-01-10"}]}'
```

- It is important to set the list_route_id that is unique in your account
- It is important to confgure the date_str with yyyy-MM-dd format

```json
{
    "route":[
        {
            "name": "Tutorial Route A",
            "warehouse":
            {
                "list_warehouse_id": "cabb46d6-776a-11ec-90d6-0242ac120003"
            },
            "list_route_id": "cdd60756-b662-404f-be64-af33b317ac60",
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

- You will find file [assets/stops.json](assets/stops.json) containing 359 stops in couples of cities in Califonia

- An important thing to note is that each stop contains the route reference to the route that was created above with route id `eab60a1e-f773-480f-87b5-1f968a1a26b9`

### Configure assignees

Here's an example of configuring assignees (drivers)

**Request example**

You can see the example data at [assets/assignees.json](assets/assignees.json)

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/assignees -XPOST --data '@assets/assignees.json'
```

- list_assignee_id should be unique in your account.

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
    },
    {
      "list_assignee_id": "tu1-tutorial-driver-3",
      "name": "Driver Three"
    },
    {
      "list_assignee_id": "tu1-tutorial-driver-4",
      "name": "Driver Four"
    },
    {
      "list_assignee_id": "tu1-tutorial-driver-5",
      "name": "Driver Five"
    }
  ]
}
```

**Note**: Your list_assignee_id should be differ.

### Run stateless DRO

**The Simple Scenario consists of**

- 359 stops from the Route `eab60a1e-f773-480f-87b5-1f968a1a26b9` above
- Up to 5 drivers (where optimization may not use all of them)
- Each driver has up to 6 hours of shift time
- Each driver's shift start at 7:00

The respective configurations for the above is at [assets/stateless-dro-request](assets/stateless-dro-request.json)  where the partial configuration bit is

```json
  "default_shift_start_time": "07:00",
  "default_shift_length": 6,
  "default_capacity": 0,
  "default_stop_time_seconds": 60,
  "default_dropoff_time_seconds": 60,
  "default_pickup_time_seconds": 60,
```

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -X POST --data '@assets/stateless-dro-request.json'
```

**Note**: the above assumes that the file `assets/stateless-dro-request.json` is relative to where the cURL is run. The `--data '@xxx'` option instructed cURL to read the file as the body of the POST request.

**Response**
You can find the sample response at [assets/stateless-dro-response.json](assets/stateless-dro-response.json) where you can see the result with multiple segments ( assignee with packages )

Here's a visualization of DRO result.

![DRO Result](assets/images/dro-result.png)
