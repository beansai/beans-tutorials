<img src="../assets/images/beans-128x128.png" align="right" />

# Dynamic Route Optimization - Plan a route with stops

Optimization for a collection of pickup/delivery is often one of the most critical aspects for
logistic planning and cost evaluations. With ebbs and flows of various demands, preemptive
capacity adjustments would improve your business efficiency.

For recommendations, suggestions, questions, and corrections, please contact us at
`developers@beans.ai`.

For detailed API shapes, please refer to [Beans Route API](https://www.beansroute.ai/route-api-v1.php)

## Table of contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Configure a warehouse](#configure-a-warehouse)
  - [Add a route to the warehouse](#add-a-route-to-the-warehouse)
  - [Loading stops into the route](#loading-stops-into-the-route)
  - [Configure an assignee](#configure-an-assignee)
  - [Run stateless DRO](#run-stateless-dro)

## Introduction

In this tutorial we will learn how to optimize a route for our assignee (driver) 
with some stops to help him go through his jorney more smoothly in the day.

### Prerequisites

To prepare your account for the tutorial, there are couples of basic elements to create so you
can examine, from our UI, the effects as well.

You will need

   * a registered account at [Beans Route](https://beansroute.ai)
   * the credential to used in Authorization in your API interactions

This tutorial uses [cURL](https://curl.se/) to illustrate the interactions with the system, and you
can use any HTTP based client to interact with the system as well.

We also recommend running cURL command piping to an output file. For example,
`curl ... | tee /tmp/my.output` would both pipe the output of the curl to the file
/tmp/my.output and also the standard output as well.

## Steps
### Configure a warehouse

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses -XPOST -d '{"warehouse":[{"list_warehouse_id":"d0686fa0-c24b-40c1-b81f-0615bfa3718a","address":"5655 Hood Way, Tracy, CA 95377"}]}'
```

- It is important to set list_warehouse_id that is unique in your account.

```json
{
  "warehouse": [
    {
      "listWarehouseId": "d0686fa0-c24b-40c1-b81f-0615bfa3718a",
      "accountBuid": "{{your-account-buid}}",
      "address": "5655 Hood Way, Tracy, CA 95377"
    }
  ]
}
```

**Note**: Your account_buid, list_warehouse_id, address would be differ.

### Add a route to the warehouse

**Request example**

```
curl -k -H 'Authorization: <token>' -X POST 'https://isp.beans.ai/enterprise/v1/lists/routes' -d '{"route":[{"name":"Tutorial Route A","warehouse":{"list_warehouse_id":"d0686fa0-c24b-40c1-b81f-0615bfa3718a"},"list_route_id":"4c432a91-6870-48d1-95ac-bec7468330d6","status":"OPEN","date_str":"2023-01-10"}]}'
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
                "list_warehouse_id": "d0686fa0-c24b-40c1-b81f-0615bfa3718a"
            },
            "list_route_id": "4c432a91-6870-48d1-95ac-bec7468330d6",
            "status": "OPEN",
            "date_str": "2023-01-10"
        }
    ]
}
```

**Note**: Your list_warehouse_id, list_route_id would be differ.

### Loading stops into the route

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/items -XPOST --data '@assets/stops.json'
```

- You will find file [assets/stops.json](assets/stops.json) containing 14 stops in couples of cities in Califonia

- An important thing to note is that each stop contains the route reference to the route that was created above with route id "leuaialveh2"

Here's a visualization of the stops with a warehouse ( the big black dot in the bottom-middle ) we just created.

![stops-on-map](assets/images/stops-on-map.png)

###  Configure an assignee

Here's an example for configuring an assignee (driver)

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/assignees -XPOST --data '{"assignee":[{"list_assignee_id":"tutorial-driver-1","name":"Tutorial Driver One"}]}'
```

- list_assignee_id should be unique in your account.

```json
{
    "assignee":[
        {
            "list_assignee_id": "tutorial-driver-1",
            "name": "Tutorial Driver One"
        }
    ]
}
```

**Note**: Your list_assignee_id should be differ.

### Run stateless DRO

**The Simple Scenario consists of**

- 14 stops from the Route `4c432a91-6870-48d1-95ac-bec7468330d6` above
- 1 route 1 driver
- Each driver has capacity up to 50 (thus, up to 50 stops)
- Each driver has up to 8 hours of shift time
- Starting and Ending location can be flexible

The respective configurations for the above is at [assets/stateless-dro-request](assets/stateless-dro-request.json)  where the partial configuration bit is

```json
  "default_shift_start_time": "07:00",
  "default_shift_length": 8,
  "default_capacity": 50,
  "default_stop_time_seconds": 60,
  "default_dropoff_time_seconds": 60,
  "default_pickup_time_seconds": 60,
  "check_seconds": 30,
  "timeout_seconds": 30,
  "start_anywhere": true,
  "end_anywhere": true,
  "use_assignees_start_address": true,
  "use_assignees_end_address": true,
  "allow_drop_time_constraints": false,
  "optimize_for": "TIME",
  "debug_print_log": true,
  "disallow_pickup_dropoff_mode": true,
  "solution_strategy": "PARALLEL_CHEAPEST_INSERTION",
  "search_strategy": "GUIDED_LOCAL_SEARCH",
  "solution_count": 200,
  "dro_request_id": "",
  "name": "dro-tutorial-run-1",
  "dro_response_id": "",
  "response_name": "dro_tutorial-run-1",
  "allow_assignee_penalty": true,
  "assignee_penalty": 1,
  "slowness": 1,
  "workarea": [],
  "disallow_transition": []
```

**Request example**

```
curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -X POST --data '@assets/stateless-dro-request.json'
```

**Note**: the above assumes that the file `assets/stateless-dro-request.json` is relative to where the cURL is run. The `--data '@xxx'` option instructed cURL to read the file as the body of the POST request.

**Response**
You can find the sample response at [assets/stateless-dro-response.json](assets/stateless-dro-response.json)


Here's a visualization of the results.

![Optimized Route](assets/images/optimized-route.png)

