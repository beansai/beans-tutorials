

<img src="../../assets/images/beans-128x128.png" align="right" />

# Callback Configs

If we want to receive callbacks when data was changed, we can set the globalUrl for callbacks and enable the feature through [Update Callback Configs](#update-callback-configs)


## Table of contents

- [Callback Configs](#callback-configs)
  - [Supported Callbacks](#supported-callbacks)
  - [Callback Config API](#callback-config-api)
    - [Get Callback Configs](#get-callback-configs)
    - [Update Callback Configs](#update-callback-configs)
  - [Callback](#callback)
    - [Enumerations](#enumerations)
    - [Callback Examples](#callback-examples)
      - [Account Callback Example](#account-callback-example)
      - [Warehouse Callback Example](#warehouse-callback-example)
      - [Route Callback Example](#route-callback-example)
      - [Item Callback Example](#item-callback-example)
      - [Item Documentation Callback Example](#item-documentation-callback-example)
      - [Assignee Callback Example](#assignee-callback-example)
      - [Assignee Vehicle Callback Example](#assignee-vehicle-callback-example)
      - [Route What-If Async Callback Example](#route-what-if-async-callback-example)
      - [Distance Matrix Async Callback Example](#distance-matric-async-callback-example)

## Supported Callbacks

Callbacks would trigger an HTTP POST on the following object types when modified.

- Account
- Route
- Item (Stop)
- ItemDocumentation
- Assignee (Driver)
- Warehouse
- AssigneeVehicle
- RouteWhatifAsync
- DistanceMatrix

## Callback Config API

### Get Callback Configs

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/callback_configs
```

**Response Example**

```json
{
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "account": true,
    "route": true,
    "item": true,
    "assignee": true,
    "warehouse": true,
    "assigneeVehicle": true,
    "globalUrl": "https://6f0c-36-237-93-205.ngrok.io",
    "routeWhatifAsync": true,
    "itemDocumentation": true,
    "distanceMatrix": true,
    "headers": [
        {
            "key": "X-Special-Header-1",
            "value": "special-value1"
        },
        {
            "key": "X-Special-Header-2",
            "value": "special-value2"
        }
    ]
}
```

### Update Callback Configs

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/callback_configs
```

```json
{
  "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
  "account": true,
  "route": true,
  "item": true,
  "assignee": true,
  "warehouse": true,
  "assigneeVehicle": true,
  "routeWhatifAsync": true,
  "itemDocumentation": true,
  "globalUrl": "https://6f0c-36-237-93-205.ngrok.io",
  "headers": [{"key":"X-Special-Header-1","value":"special-value1"},{"key":"X-Special-Header-2","value":"special-value2"}]
}
```
- globalUrl is for where you want to receive the callback POST.
- Headers are a list of key/value objects that the callback POST call would include in every single call.

**Response Example**

```json
{
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "account": true,
    "route": true,
    "item": true,
    "assignee": true,
    "warehouse": true,
    "assigneeVehicle": true,
    "globalUrl": "https://6f0c-36-237-93-205.ngrok.io",
    "routeWhatifAsync": true,
    "itemDocumentation": true,
    "distanceMatrix": true,
    "headers": [
        {
            "key": "X-Special-Header-1",
            "value": "special-value1"
        },
        {
            "key": "X-Special-Header-2",
            "value": "special-value2"
        }
    ]
}
```


## Callback

We can dynamically resolve the object type by parsing the "type" field to determine the type of the object.

### Enumerations

**Types**

- ACCOUNT
- WAREHOUSE
- ROUTE
- ITEM
- ITEM_DOCUMENTATION
- ASSIGNEE
- ASSIGNEE_VEHICLE
- ROUTE_WHATIF_ASYNC
- DISTANCE_MATRIX

**Actions**

- CREATE
- UPDATE
- DELETE

**Watermark**

The system ensures that the value of the watermark is strictly increasing. In other words, if the receiver of the callback receives a message on the same object with earlier watermark, the receiver can safely assume that payload represented an earlier version of the object.

### Callback Examples

#### Account Callback Example

```json
{
    "type": "ACCOUNT",
    "action": "UPDATE",
    "account_buid": "35138aee-b003-3ac9-ba7a-9c8bca9eb906",
    "object": {
        "account_buid": "35138aee-b003-3ac9-ba7a-9c8bca9eb906",
        "email": "donchen+delegator-10@beans.ai",
        "subscription_plan": "beans_routes-free-trial-01",
        "created_at": "1644478996000",
        "updated_at": "1644550508947",
        "account_name": "don-delegated",
        "tags": [
            {
                "key": "/ACCOUNT/DEFAULT/TIMEZONE_ID",
                "value": "America/New_York"
            },
            {
                "key": "/ACCOUNT/DELEGATOR",
                "value": "4022a1aada0e4c4684e61e3f73290a68"
            },
            {
                "key": "/ACCOUNT/DELEGATOR/REFID",
                "value": "delegator-10"
            },
            {
                "key": "/ACCOUNT/ROUTE/PREFERENCE/USE_BEANS_SEQUENCING",
                "value": "true"
            }
        ]
    },
    "watermark": "1644550508947"
}
```

#### Warehouse Callback Example

```json
{
    "type": "WAREHOUSE",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_warehouse_id": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f2",
        "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
        "address": "14840 CA-4, Discovery Bay, CA 94505",
        "formatted_address": "14840 CA-4, Discovery Bay, CA",
        "created_at": "1644384027000",
        "updated_at": "1644543893077",
        "position": {
            "lat": 37.88946,
            "lng": -121.6215
        },
        "name": "Tutorial Warehouse 2"
    },
    "watermark": "1644543893077"
}
```

#### Route Callback Example

```json
{
    "type": "ROUTE",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_route_id": "xbzqzamtj7e1664jmvcdd8",
        "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
        "name": "Route Name 3-1",
        "status": "OPEN",
        "created_at": "1644387971000",
        "updated_at": "1644548534781",
        "route_path_md5": "faae252de0e2c9d56b1df8cb57977331",
        "date_str": "2022-02-10",
        "start_mode": "WAREHOUSE",
        "end_mode": "WAREHOUSE",
        "tags": [
            {
                "key": "/UNASSIGNED_MANUALLY",
                "value": "true"
            }
        ]
    },
    "watermark": "1644548534781"
}
```

#### Item Callback Example

```json
{
    "type": "ITEM",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_item_id": "d3f6-a801b3605afbd726df743cc66",
        "address": "3365 Deer Valley Rd, Antioch, CA 94531",
        "formatted_address": "3365 Deer Valley Rd, Antioch, CA",
        "status": "NEW",
        "updated_at": "1644548585670",
        "status_updated_at": "1643267011000",
        "route": {
            "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
        },
        "route_priority": 6,
        "type": "PICKUP",
        "position": {
            "lat": 37.98784,
            "lng": -121.78451
        },
        "display_position": {
            "lat": 37.98784,
            "lng": -121.78445
        },
        "deliver_from_str": "2033-01-01 13:00",
        "deliver_by_str": "2033-01-01 18:00",
        "address_components": {
            "zipcode": "94531",
            "country_iso3": "USA"
        }
    },
    "watermark": "1644548585670"
}
```

#### Item Documentation Callback Example
```json
{
    "type": "ITEM_DOCUMENTATION",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_item_id": "ca8d-fae5d3b6b9c9f2f1a14c43b0a1",
        "list_route_id": "ca8daa7f-0625-4ebe-9b57-6314e6746fef",
        "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
        "timestamp_epochSecond": "1652340862",
        "notes": [
            "014-DroppedOfAtCustomer"
        ],
        "images": [
            {
                "url": "https://storage.googleapis.com/beans-images/testing/original/2022-03-03/2022-03-03_fc181e29-8bcd-4c50-b388-cd13994fe0e0.jpeg",
                "type": "proof"
            },
            {
                "url": "https://storage.googleapis.com/beans-images/testing/original/2022-03-02/2022-03-02_b695d615-4d32-4222-ba34-f34a68f1cee4.png",
                "type": "proof",
                "position": {
                    "lat": 20.2,
                    "lng": -30.2
                }
            }
        ],
        "event_code": {
            "code": "014",
            "name": "DroppedOfAtCustomer"
        },
        "tags": [
            {
                "key": "/FEDEX/package_size",
                "value": "large"
            }
        ]
    },
    "watermark": "1652340862"
}
```

#### Assignee Callback Example

```json
{
    "type": "ASSIGNEE",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_assignee_id": "tu1-tutorial-driver-1",
        "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
        "name": "New Driver 2",
        "code": "cd787cc3-fd8",
        "created_at": "1642408164000",
        "updated_at": "1644548633326",
        "state": "ACTIVE",
        "role": "DRIVER",
        "employee_id": "2000001",
        "list_warehouse_id": "lzt6vwxta2o0e1hsl9k75u"
    },
    "watermark": "1644548633326"
}
```

#### Assignee Vehicle Callback Example

```json
{
    "type": "ASSIGNEE_VEHICLE",
    "action": "UPDATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "capacity": 8,
        "updated_at": "1644548670282",
        "dimensions": {}
    },
    "watermark": "1644548670282"
}
```

#### Route What-if Async Callback Example

```json
{
    "type": "ROUTE_WHATIF_ASYNC",
    "action": "CREATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "item": [
            {
                "list_item_id": "bdf4489a1f7c374691fd38657fe8c7b1",
                "address": "685 PROVIDENCE MAIN ST NW, HUNTSVILLE, AL 35806264414"
            }
        ],
        "list_route_ids": [
            "0c515c53ae9632319302d2af4badb329",
            "1f3ce17c77893509905cc9851b4745af",
            "2ee5b6974d263d4fb4489562095b4b64"
        ],
        "route_size_limit": 60,
        "request_id": "35b4284e-1d07-483a-ac4a-c2bd6d9969aa001",
        "asynchronous": true,
        "internal_ref": "7f572f3b325d4348880010b80dbb1bed",
        "start_time_epoch": "1644549843",
        "end_time_epoch": "1644549844",
        "result": {},
        "message": "There are 3 routes where 3 are not suitable and 0 are possibilities"
    },
    "watermark": "1644549844"
}
```

#### Distance Matric Async Callback Example

```json
{
  "type": "DISTANCE_MATRIX",
  "action": "CREATE",
  "account_buid": "aCUYkl5jtq8-BrBTr3pTdzmnVQyb8Im5ODarcMg-ucyDFHSJ3D9bvdxlnbFyeoikFo2BKlATE0PPgah7IXvKqFe7TdcD_uCZdUgiMLVGqbyy6JGxPta73ZdaPjBARsfIuq65qQ",
  "object": {
    "rows": [
      {
        "value": [
          0.8,
          84.6
        ]
      },
      {
        "value": [
          2478.5,
          2481.6
        ]
      },
      {
        "value": [
          12.7,
          98.1
        ]
      }
    ],
    "stat": {
      "unique_source": 3,
      "unique_destination": 2,
      "total_cells": 6
    },
    "request_id": "matrix-005",
    "start_time_epoch": "1663001528",
    "account_buid": "aCUYkl5jtq8-BrBTr3pTdzmnVQyb8Im5ODarcMg-ucyDFHSJ3D9bvdxlnbFyeoikFo2BKlATE0PPgah7IXvKqFe7TdcD_uCZdUgiMLVGqbyy6JGxPta73ZdaPjBARsfIuq65qQ",
    "request": {
      "request_id": "matrix-005",
      "points": [
        {
          "position": {
            "lat": 34.546310804961294,
            "lng": -82.68218827032248
          }
        },
        {
          "position": {
            "lat": 34.546310804961294,
            "lng": -82.6832
          }
        },
        {
          "position": {
            "lat": 34.546310804961294,
            "lng": -82.6822
          }
        },
        {
          "position": {
            "lat": 34.5462,
            "lng": -82.6822
          }
        },
        {
          "position": {
            "lat": 34.5469,
            "lng": -82.6822
          }
        }
      ],
      "sources_idx": [
        0,
        1,
        3
      ],
      "destinations_idx": [
        2,
        4
      ],
      "asynchronous": true,
      "country_iso3": "USA"
    }
  },
  "watermark": "1663001528712"
}
```
