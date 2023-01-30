<img src="assets/images/beans-128x128.png" align="right" />

# Dynamic Route Optimization

Optimizing for a collection of pickup/delivery points is one of the most critical components of successful logistics planning and cost evaluation. It allows for preemptive capacity adjustments to respond to ebbing and flowing demand: ultimately improving your business' efficiency.

For recommendations, suggestions, questions, and corrections, please contact us at
`developers@beans.ai`.

For detailed API shapes, please refer to [Beans Route API](https://www.beansroute.ai/route-api-v1.php)

### Prerequisites

To prepare for the tutorial, you'll need a few things.

You will need

   * A registered account at [Beans Route](https://beansroute.ai)
   * A credential to authorize your API interactions

### Optimizations

Many businesses offer services that require traveling to multiple stops every day. These businesses all need an efficient way to visit their stops in an order that minimizes distance traveled, minimizes time spent, and takes into account any other applicable contraints. Some examples of this include:

- A logistics comapny wants to assign routes for drivers to deliver packages.
- A real estate agent wants to optimize routes for visiting houses with customers.
- A firestation wants to assign routes for a fireman to check fire facilities.

The following tutorials explain how we solve these problems with DRO ( Dynamic route optimization )

- [General Tutorial](general-tutorial)
  - [All Parameters](https://www.beansroute.ai/route-api-v1.php#optimization-stateful)
- [Basic routing optimization](basic-routing-optimization) in which there's only one vehicle.
- [Vehicles routing optimization](vehicles-routing-optimization).
- [Vehicles routing optimization with capacity constraints](vehicles-routing-optimization-with-capacity-constraints) when vehicles have limited capcities for items they can carry.
- [Vehicles routing optimization with time windows](vehicles-routing-optimization-with-time-windows) when each stop has a time window for visiting.
- [Vehicles routing optimization with shift time](vehicles-routing-optimization-with-shift-time) when drivers have different schedules for working.
- [Vehicles routing optimization with floating drivers](vehicles-routing-optimization-with-floating-drivers) when drivers have no schedule, or want to plan in advance.
- [Vehicles routing optimization with pickups dropoffs](vehicles-routing-optimization-with-pickups-dropoffs)
- [Vehicles routing optimization with dimensions](vehicles-routing-optimization-with-dimensions) when vehicles have constraints like weight or  volume.
- [Vehicles routing optimization with flavors](vehicles-routing-optimization-with-flavors) when packages have constraints like COLD, HOT, FRAGILE...
- [Vehicles routing optimization with assignee start/end anywhere](vehicles-routing-optimization-with-assignee-start-end-anywhere) when assignee will not start or end a daily work at warehouse.
- [Vehicles routing optimization with stops time](vehicles-routing-optimization-with-stop-time)
- [Vehicles routing optimization with customized assignee location](vehicles-routing-optimization-with-customized-assignee-location) when we want to customize assignees' start or end location.