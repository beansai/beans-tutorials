<img src="../assets/images/beans-128x128.png" align="right" />

# What-if

Given a small list of stops (let's say N stops) and some routes (let's say M routes), Beans Optimizations can be leveraged to determined the best distribution of those N stops onto those M routes given the constraints via [Stateful Route Optimization](https://github.com/beansai/beans-tutorials/tree/main/dynamic-routes-optimization)

However, another important use case for route estimation is to determine the cost differences (in time and distance) that those N stops on each of the M routes.

In other words, if those N stops were grouped together and MUST be serviced by a single route, what would be the delta costs in time and distance for each of the M routes?

This is termed "what-if" routes computations.

Beans has provided an API that would assist in this computation.

### Prerequisites

To prepare for the tutorial, you'll need a few things.

You will need

   * A registered account at [Beans Route](https://beansroute.ai)
   * A credential to authorize your API interactions

Once you have your key and secret available, you are required to specify them in the `Authorization header` of all your requests, as below.

```
Authorization: Basic OE9Bd2hiSzA6Qzc3NTJFMjQwNTkxNDk0NUU3RDA4
```

## Tutorials

- [General Tutorial](general)
  - All attributes we can use
  - Run What-if
  - Run What-if async
- [Source Sequence](source-sequence) - When we want to see how Stops' ordering will impact the result.
- [Route Size Limit](route-size-limit) - When a route has a upper limit of stops size.
- [Warehouse as terminal](warehouse-as-terminal) - When we want to observe the difference between use warehouse as terminal or not.
- [Stops outside current date](stops-outside-current-date) - When we want to decide whether or not to use stops which has no intersect with current date.
- [Multiple Day Stops](multiple-day-stops) - When we want to decide whether or not to use stops which deliver from/by is within 24 hours.