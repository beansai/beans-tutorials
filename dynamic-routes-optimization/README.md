<img src="assets/images/beans-128x128.png" align="right" />

# Dynamic Route Optimization

Optimization for a collection of pickup/delivery is often one of the most critical aspects for
logistic planning and cost evaluations. With ebbs and flows of various demands, preemptive
capacity adjustments would improve your business efficiency.

For recommendations, suggestions, questions, and corrections, please contact us at
`developers@beans.ai`.

For detailed API shapes, please refer to [Beans Route API](https://www.beansroute.ai/route-api-v1.php)

### Prerequisites

To prepare your account for the tutorial, there are couples of basic elements to create so you
can examine, from our UI, the effects as well.

You will need

   * A registered account at [Beans Route](https://beansroute.ai)
   * The credential to used in Authorization in your API interactions

### Optimizations

When we are offering services that need to travel on the way every day, we might want to find an efficient way to visit all the locations with shorter distances or time. Also, sometimes, we might have limitations for location visits.

- A logistic comapny wants to assign routes for drivers to delivery packages.
- A real estate agent wants to optimize routes for visiting houses with customers.
- A firestation wants to assign routes for fireman to check fire facilities.

The followings are how we solve these problems with DRO ( Dynamic route optimization )

- [Basic routing optimization](basic-routing-optimization) in which there's only one vehicle.
- [Vehicles routing optimization](vehicles-routing-optimization).
- [Vehicles routing optimization with capacity constraints](vehicles-routing-optimization-with-capacity-constraints) that vehicles have limitation capcities for items they can carry.
- [Vehicles routing optimization with time windows](vehicles-routing-optimization-with-time-windows) that each stop has time window for visiting.
- [Vehicles routing optimization with shift time](vehicles-routing-optimization-with-shift-time) which drivers have a different schedule for working.
- [Vehicles routing optimization with floating drivers](vehicles-routing-optimization-with-floating-drivers) that drivers have no schedule or we want to plan in advance.
- [Vehicles routing optimization with pickups dropoffs](vehicles-routing-optimization-with-pickups-dropoffs)
