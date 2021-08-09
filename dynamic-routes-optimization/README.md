# Dynamic Route Optimization

![Beans Route](https://www.beansroute.ai/img/img-logo.png "Beans Route")

Optimization for a collection of pickup/delivery is often one of the most critical aspects for
logistic planning and cost evaluations. With ebbs and flows of various demands, preemptive
capacity adjustments would improve your business efficiency.

For recommendations, suggestions, questions, and corrections, please contact us at
`developers@beans.ai`.

For detailed API shapes, please refer to [Beans Route API](https://www.beansroute.ai/route-api-v1.html)

## Introduction

In this tutorial, we will use the API to setup the account for simple route optimizations in
both "stateless" and "stateful" manners.

"Stateless" optimization can be used to evaluate planning feasibility and experimentation, while
"Stateful" optimization can be used to adjust existing routes to examine differences.

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

#### Setting up the account with a warehouse

`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses`

`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/warehouses
-XPOST
-d '{"warehouse":[{"list_warehouse_id":"b47c3bc1-efc0-49fb-9aad-b3095f13b31b","address":"5655 Hood Way, Tracy, CA 95377"}]}'`

```json
{
  "warehouse": [
    {
      "listWarehouseId": "b47c3bc1-efc0-49fb-9aad-b3095f13b31b",
      "accountBuid": "c2647bb5d26847faac56907f980da023",
      "address": "5655 Hood Way, Tracy, CA 95377",
      "formattedAddress": "5655 Hood Way, Tracy, CA",
      "createdAt": 1628277510865,
      "updatedAt": 1628277510865,
      "position": {
        "latitude": 37.7289493,
        "longitude": -121.5082503
      }
    }
  ]
}
```

### Configure a grouping Route for Stops

A grouping Route, although isn't required for optimization, is a convenient bucket to gather
stops to be optimized.


#### Setting up the account with a Route

`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/routes -XPOST -d '{"route":[{"list_route_id":"d27e174b-ff71-4854-af85-72c056ae1b05","name":"All Stops","date_str":"2023-08-01","status":"open","warehouse":{"list_warehouse_id":"b47c3bc1-efc0-49fb-9aad-b3095f13b31b"}}]}'`
   * It is important to set the list_route_id that is unique in your account
   * It is important to configure the date_str taking yyyy-MM-dd format
   
```json
{
  "route": [
    {
      "listRouteId": "d27e174b-ff71-4854-af85-72c056ae1b05",
      "accountBuid": "c2647bb5d26847faac56907f980da023",
      "name": "All Stops",
      "status": "OPEN",
      "createdAt": 1628277348000,
      "updatedAt": 1628287742324,
      "warehouse": {
        "listWarehouseId": "b47c3bc1-efc0-49fb-9aad-b3095f13b31b",
        "accountBuid": "c2647bb5d26847faac56907f980da023",
        "address": "5655 Hood Way, Tracy, CA 95377",
        "formattedAddress": "5655 Hood Way, Tracy, CA",
        "createdAt": 1628277511000,
        "updatedAt": 1628277511000,
        "position": {
          "latitude": 37.7289493,
          "longitude": -121.5082503
        }
      },
      "routePathMd5": "_zip_07f8fe511d25d0280d20ef5047868f7d",
      "dateStr": "2023-08-01"
    }
  ]
}
```

#### Loading Stops into the grouping Route

You will find in file [assets/stops.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/stops.json)
containing 359 stops in couples of cities in California. An important to note is that each stop
contains the route reference to the route that was created above with route id:  d27e174b-ff71-4854-af85-72c056ae1b05.

`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/lists/items -XPOST --data '@assets/stops.json'`

**Note**: the above assumes that the file "assets/stops.json" is relative to where the cURL is run.
The `--data '@xxx'` option instructed cURL to read the file as the body of the POST request.

Since there are 359 stops, the response is HUGE, you can find the visualization of the route at

[Tutorial Route Map](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/images/route_map.png)

### Simple Stateless DRO with up to 10 Routes

The Simple Scenario consists of
   * 359 stops from grouping Route `d27e174b-ff71-4854-af85-72c056ae1b05` above
   * Up to 10 routes/drivers (where optimization may not use all of them)
   * Each driver has capacity up to 50 (thus, up to 50 stops)
   * Each driver has up to 8 hours of shift time
   * Starting and Ending location can be flexible

The respective configurations for the above is at
[assets/simple_dro_request.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/simple_dro_request.json)
where the partial configuration bit is
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
The file [assets/simple_dro_request.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/simple_dro_request.json)
contains all the stops from the grouping route and thus, you can always create the DRO Request object
straight from the stops without the grouping Route. You do need to geo-code the stops to make
sure the location is specified.

Here is the cURL request
`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/run -XPOST --data '@assets/simple_dro_request.json'`

Since the response is large, an example response is at
[assets/simple_dro_response.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/simple_dro_response.json)

You can find the visualization at

[Simple DRO Output](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/images/simple_dro_result.png)
   * we specified the name of the request as "dro-tutorial-run-1" in our request, and it would be
   saved and available in the dropdown menu on the UI
   * also, we specified the name of the response with the same name, and it would also be available
   in the dropdown menu on the UI as well

#### Applying the DRO results to create routes

The segments in the [assets/simple_dro_response.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/simple_dro_response.json)
represents the routes that the optimizer found the best solution for given the constraints. To
finalize those segments, we need to **apply** them into routes for operations.

This tutorial has constructed [assets/simple_dro_apply.json](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/simple_dro_apply.json)
which included
   * the "default" warehouse
   * the "default" start time and shift length
   * the segment from the result

`curl -k -H 'Authorization: <token>' https://isp.beans.ai/enterprise/v1/dro/apply -XPOST --data '@assets/simple_dro_apply.json'`

A simple visualization showing the routes can be found at

[Simple DRO Routes applied](https://github.com/beansai/beans-tutorials/blob/main/dynamic-routes-optimization/assets/images/routes_applied.png)
   * the segments with empty stops were also created. There may be situation where you
   want to remove the empty segments
