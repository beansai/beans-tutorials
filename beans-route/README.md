<img src="../assets/images/beans-128x128.png" align="right" />

# Beans Route

Optimizing for a collection of pickup/delivery points is one of the most critical components of successful logistics planning and cost evaluation. It allows for preemptive capacity adjustments to respond to ebbing and flowing demand: ultimately improving your business' efficiency.

For recommendations, suggestions, questions, and corrections, please contact us at
`developers@beans.ai`.

For detailed API shapes, please refer to [Beans Route API](https://www.beansroute.ai/route-api-v1.php)

### Prerequisites

To prepare for the tutorial, you'll need a few things.

You will need

   * A registered account at [Beans Route](https://beansroute.ai)
   * A credential to authorize your API interactions

Once you have your key and secret available, you are required to specify them in the `Authorization header` of all your requests, as below.

```
Authorization: Basic OE9Bd2hiSzA6Qzc3NTJFMjQwNTkxNDk0NUU3RDA4
```

### Basic Management

Many businesses offer services that require traveling to mutilple stops every day,
and they all need an efficient way to schedule/manage the daily works.

- A stop which describes place to visit.

- A route which contains one or more stops to visit.
- An assignee (driver) who is responsible to do the delivery.
- A warehouse where a driver can pick up packages and start doing the delivery.

### Basic Tutorials

- [Warehouses management](warehouses-management)
- [Routes management](routes-management)
  - Assign a route to a warehouse
  - Assign an assignee (driver) to a route
- [Assignees (driver) management](assignees-management)
- [Stops management](stops-management)
  - [Stops management with source sequence](stops-management/source-sequence) - When we want to predetermine the ordering of stops.
- [Delegated Accounts](delegated-accounts)
- [Callback Configs](callback-configs)
- [Route Optimization](route-optimization)
  - [Route Optimization with units](route-optimization-with-units) - Group stops based on address...
- [Item Documentation](item-documentation) - To get/post item documentations

