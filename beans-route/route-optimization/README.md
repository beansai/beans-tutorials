<img src="../../assets/images/beans-128x128.png" align="right" />

# Route Optimization

## Table of contents

- [Route Optimization with Stops](#route-optimization-with-stops)
- [Route Optimization](#route-optimization-1)
- [Route Path](#route-path)

## Optimize Route with stops
![stops](assets/images/stops.png)
Let's say we have a route with 10 stops in LA, and we want to optimize the route for assignee who will start/end work at warehouse.

**Request example**

```
POST {{baseURL}}/enterprise/v1/lists/items/do/optimize/?startMode=WAREHOUSE&endMode=WAREHOUSE
```
Here is a list of startMode, endMode which we are supporting for optimization conditions.
- WAREHOUSE
- ASSIGNEE_LOCATION
- ASSIGNEE_ADDRESS
- PREVIOUS_STOP
- NONE

**Body**

You can find the full payload here [stops](assets/stops.json) which contains 10 stops in an array, while the partial is below.
```json
{
    "item": [
        {
            "listItemId": "8d156298-e779-4176-ad9a-5ea6fca79f1c-7",
            "address": "9404 Central Ave, Montclair, CA 91763, United States",
            "formattedAddress": "9404 Central Ave, Montclair, CA",
            "status": "NEW",
            "updatedAt": 1648193534000,
            "statusUpdatedAt": 1648193534000,
            "route": {
                "listRouteId": "la-route-1"
            },
            "routePriority": 32,
            "type": "DROPOFF",
            "position": {
                "latitude": 34.08418,
                "longitude": -117.68966
            },
            "displayPosition": {
                "latitude": 34.08303,
                "longitude": -117.69066
            },
            "addressComponents": {
                "city": "Montclair",
                "state": "CA",
                "zipcode": "91763",
                "street": "9404 Central Ave",
                "countryIso3": "USA"
            },
            "countryIso3": "USA"
        }
        ...
    ]
}
```

**Response example**

You can find the full response content from here [response](assets/optimize-route-response.json) while the partial is below


```json
{
    "item": [
        {
            "listItemId": "9ec8c902-cba0-483a-8c13-02ebc28f791d10",
            "address": "3845 E 3RD ST LOS ANGELES",
            "formattedAddress": "3845 E 3rd St Los Angeles",
            "status": "NEW",
            "updatedAt": 1648195367387,
            "statusUpdatedAt": 1648193171000,
            "route": {
                "listRouteId": "la-route-1"
            },
            "routePriority": 8,
            "type": "DROPOFF",
            "position": {
                "latitude": 34.03351,
                "longitude": -118.18494
            },
            "displayPosition": {
                "latitude": 34.03351,
                "longitude": -118.18494
            },
            "isExternal": true,
            "sourceSeq": 1
        }
        ...
    ],
    "route": [
        {
            "listRouteId": "la-route-1",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "LA Route 1",
            "status": "OPEN",
            "createdAt": 1648192867000,
            "updatedAt": 1648195368000,
            "warehouse": {
                "listWarehouseId": "la-union-station",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "800 N Alameda St, Los Angeles, CA 90012, United States",
                "formattedAddress": "800 N Alameda St, Los Angeles, CA",
                "createdAt": 1648192761000,
                "updatedAt": 1648192761000,
                "position": {
                    "latitude": 34.05669,
                    "longitude": -118.23621
                },
                "name": "CA - Union Station"
            },
            "routePathMd5": "_zip_dbf4d42dc5f96d74215f471db55cee6f",
            "dateStr": "2031-03-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE"
        }
    ]
}

```
***Note***
- route_priority may not start from 1, in other words the route_priority may looks like this 3,6,10,15,23,100,200...
- We have priority 0 (and -1) which is meant to be out of the path.

The Route Optimization algorithm will update each stop's route_priority which is the system's suggestion of stop visiting priority.

## Route Optimization
For some scenarios, one wishes to optimize an entire route regardless of how many stops there are, especially when the stops are being added dynamically. The following is a shorter version that would execute the same optimization process.

**Request example**

```
POST {{baseURL}}/lists/routes/{listRouteID}/do/optimize?startMode=WAREHOUSE&endMode=WAREHOUSE
```
Here is a list of startMode, endMode which we are supporting for optimization conditions.
- WAREHOUSE
- ASSIGNEE_LOCATION
- ASSIGNEE_ADDRESS
- PREVIOUS_STOP
- <lat>,<lng> (e.g. 37.12423,-123.2323)

**Body**
None

***Note***
- POST request without the body

## Route Path
The path line show on the image above can be GET via the following call

**Request example**

```
GET {{baseURL}}/lists/routes/{listRouteID}/path?enc=true&force_refresh=true
```
- enc: true/false, where true would return the route path in much much more efficient Google encoded polygon (https://github.com/googlemaps/js-polyline-codec)
- force_refresh: true/false, when true would trigger the system to recompute (this could be computational expensive, and thus, our recommendation is to call this only when something material has changed)

**Response**
```
{
  "line": [
    {
      "encoded": "}zqlFn_qaQ???K@qA?WM?iA?K?A?[?BzK@bHDhO?X?d@XAP?|B?l@AlCI|@AdHC\\?pA??N?r@?v@@dE?d@Cj@Gv@?NB^D^HRDLX^PVHNHPHNHXFVDb@Fp@PjChAGJ?Z?T@j@HZJZL\\TXTt@z@VR\\N\\H\\@V?VGVMRSLYLa@Rw@ZiAB[[C_@QIGQMa@k@Yg@So@M{@Cg@a@AIAUCYS]]o...<snipped>",
      "referenceId": "xanvvhq3ijkvgb4dnrwbz"
    },
    {
      "distanceM": 1627.3,
      "timeS": 180,
      "referenceId": "cvkxup94rnrg5gdbyaz68m"
    },
    {
      "distanceM": 729.4,
      "timeS": 115.1,
      "referenceId": "ey2vayohxe56daa9qpmlj8"
    },
    {
      "distanceM": 978.8,
<snipped>
  ]
}
```
- The lines is an array of points, where the 0th index kine contains the path. The referenceId is matching to the list_item_id of the items on the Route, and the items are sorted based on the way points


***Note***
- as usual, ignore any unknown fields in your parsing

