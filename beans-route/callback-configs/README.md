

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
      - [Driver Start Callback Example](#driver-start-callback-example)
      - [Missing Info on Packages Add Example](#missing-info-on-packages-add)

## Supported Callbacks

Callbacks would trigger an HTTP POST on the following object changes or event issues.

- Account
- Route
- Item (Stop)
- ItemDocumentation
- Assignee (Driver)
- Warehouse
- AssigneeVehicle
- RouteWhatifAsync
- DistanceMatrix
- DriverStart
- Missing info on Packages Add

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
    "globalUrl": "https://96d2-36-237-115-38.ngrok.io",
    "routeWhatifAsync": true,
    "headers": [
        {
            "key": "X-Special-Header-1",
            "value": "special-value1"
        },
        {
            "key": "X-Special-Header-2",
            "value": "special-value2"
        }
    ],
    "itemDocumentation": true,
    "distanceMatrix": true,
    "driverStart": true,
    "barcodeMissingInfo": true
}
```

### Config Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **accountBuid** | string | account ID of authenticated call | The account ID of the config |
| **account** | boolean | false | Whether to receive Account object callbacks  |
| **route** | boolean | false | Whether to receive Route object callbacks  |
| **item** | boolean | false | Whether to receive Item object callbacks  |
| **assignee** | boolean | false | Whether to receive Assignee object callbacks  |
| **warehouse** | boolean | false | Whether to receive Warehouse object callbacks  |
| **assigneeVehicle** | boolean | false | Whether to receive Assignee Vehicle object callbacks  |
| **routeWhatifAsync** | boolean | false | Whether to receive Route What if Async object callbacks  |
| **itemDocumentation** | boolean | false | Whether to receive Item Documentation, PoD, object callbacks  |
| **distanceMatrix** | boolean | false | Whether to receive Distance Matrix object callbacks  |
| **driverStart** | boolean | false | Whether to receive Driver Start object callbacks  |
| **barcodeMissingInfo** | boolean | false | Whether to receive Barcode missing info callbacks. This is only triggered when a scanned barcode does not have sufficient amount of information to be resolved by the system. |
| **globalUrl** | string | "" | The global endpoint to POST the callback object to  |
| **headers** | Array of Header | Empty List| Headers to include while performing the POST |
| **includeDefaultValues** | boolean | false | Whether or not default values of callback object should be included in the payload |

#### Header Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **key** | string | "" | The header key in HTTP request |
| **value** | string | "" | The header value in HTTP request |


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
  "distanceMatrix":true,
  "driverStart":true,
  "barcodeMissingInfo": true,
  "globalUrl": "https://96d2-36-237-115-38.ngrok.io",
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
    "globalUrl": "https://96d2-36-237-115-38.ngrok.io",
    "routeWhatifAsync": true,
    "headers": [
        {
            "key": "X-Special-Header-1",
            "value": "special-value1"
        },
        {
            "key": "X-Special-Header-2",
            "value": "special-value2"
        }
    ],
    "itemDocumentation": true,
    "distanceMatrix": true,
    "driverStart": true,
    "barcodeMissingInfo": true
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
- DRIVER_START
- BARCODE_MISSING_INFO

**Actions**

- CREATE
- UPDATE
- DELETE

### Envelop

The callback is structured as an envelop that wraps around the object of concern. Unless otherwise noted, the envelops for all callbacks are shaped the same.

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **type** | string | Types enum | The object type of the callback |
| **action** | string | Actions enum | The object lifecycle of the callback |
| **account_buid** | string | The account ID of the object | The account ID of which the object is in |
| **object** | dynamic | Object type | The respective object given the type |
| **watermark** | long | 0 | The watermark of the callback. The system ensures that the value of the watermark is **strictly increasing**. In other words, if the receiver of the callback receives a message on the same object with earlier watermark, the receiver can safely assume that payload represented an earlier version of the object. |

### Notes on object processing

   - With default configurations, fields with default value (e.g. empty string, 0 numeric, false booleans) would be omitted from the object payloads
      - includeDefaultValues = true would return those fields with their default values
   - New fields may be introduced as we have dynamic bindings of callbacks to the actual object's life cycles. Thus, those new fields may be ignored till they are ready to be incorporated into your workflows
   - The object in the callback is **always** the **full** shape of the object, no partials.
   - On an existing object, callback is triggered when there is **any** update to the object. It is up to the receiver to determine the differences and whether or not they are relevant
      - Since new fields may be introduced, it is very possible that none of the fields that you incorporated are modified
   
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

##### Account Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **account_buid** | string | The account ID | Unique identifier of an account |
| **account_name** | string | "" | The name of the account |
| **email** | string | "" | The email of the account |
| **subscription_plan** | string | "" | The plan(s) that this account has subscribed |
| **subscription_seat_count** | int32 | 0 | The number of seats that this account has subscribed |
| **third_party_account_type** | string | "" | The type of the account |
| **third_party_account_id** | string | "" | Third party reference ID for this account |
| **current_imports** | string | "" | The status of manifest imports, if appropriate |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this account is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this account is last updated |
| **seats_safety_module** | int32 | 0 | The number of safety seats that this account has subscribed |
| **is_safety_enabled** | boolean | false | Whether safety training is enabled for this account |
| **safety_provider** | string | "" | The provider name of the safety training |
| **safety_account_id** | string | "" | The safety provider reference ID, where appropriate |
| **safety_integration_status** | string | "" | The integration status between Beans and the Safety Provider for this account |
| **tags** | Array of Tag | Empty Array | A list of account tags. These are account preferences |

##### Tag object
| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **key** | string | "" | The key of the tag |
| **value** | string | "" | TThe value of the tag |

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

##### Warehouse Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_warehouse_id** | string | The warehouse ID | The unique id of the warehouse |
| **account_buid** | string | The account ID | The account ID that this warehouse is in |
| **address** | string | "" | The address of the warehouse |
| **formatted_address** | string | "" | The formatted address |
| **country_iso3** | string | "" | The country ISO3 code of the warehouse |
| **name** | string | "" | The name of the warehouse |
| **domicile** | string | "" | The domicile code of the warehouse |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this warehouse is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this warehouse is last updated |
| **deleted** | boolean | false | Whether or not the warehouse is deleted |
| **partner_warehouse_uuid** | string | "" | An associated warehouse reference to a partner |
| **position** | LatLng | {} | The Lat/Lng of the warehouse |
| **tags** | Array of Tag | Empty Array | A list of warehouse tags. These are warehouse preferences |

##### LatLng Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **lat** | double | 0.0 | The latitude |
| **lng** | double | 0.0 | The longitude |

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

##### Route Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_route_id** | string | The Route ID | The unique id of the route |
| **account_buid** | string | The account ID | The account ID that this route is in |
| **name** | string | "" | The name of the route |
| **date_str** | string | "" | The date str (yyyy-mm-dd) |
| **status** | string | "" | One of OPEN, CLOSED  |
| **manifest_name** | string | "" | The name of the manifest that was loaded to create this route |
| **assignee** | Assignee Object | {} | The Assignee object associated with this route |
| **warehouse** | Warehouse Object | {} | The warehouse object associated with this route |
| **route_path_md5** | string | "" | The md5 hash of the path last computed for this route |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this route is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this route is last updated |
| **providers** | Array of string | Empty array | 0 or more providers that are associated with this route |
| **assignee_secondarys** | Array of string | Empty array | A list of assignee IDs acting as secondary assignees to this route |
| **route_type** | string | "" | One of DEFAULT, STORAGE, OMBUDSMAN or empty string to indicate the type of the route |
| **tags** | Array of Tag | Empty Array | A list of route tags. These are route preferences |
| **start_mode** | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the start location of the route |
| **end_mode** | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the end location of the route |

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

##### List Item Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_item_id** | string | The item ID | The unique id of the item |
| **account_buid** | string | The account ID | The account ID that this item is in |
| **address** | string | "" | The original address for this item |
| **unit** | string | "" | The original unit for this item, or secondary address line |
| **notes** | string | "" | The notes associated with this item, this is free form text |
| **formatted_address** | string | "" | Formatted address for this item, often is generated and cleaned during geocoding process if geocoder is enabled |
| **deliver_from_str** | string | "" | The start of the time window that this item could be done by |
| **deliver_by_str** | string | "" | The end of the time window that this item should be done by |
| **tracking_id** | string | "" | The tracking ID of the stop |
| **num_packages** | int32 | 0 | The number of packages associated with this stop |
| **type** | string | Enum | One of PICKUP, DROPOFF |
| **customer_name** | string | "" | The name of the customer associated with this item |
| **customer_phone** | string | "" | The phone number of the customer associated with this item |
| **status** | string | Enum | One of NEW, IN_PROCESS, FINISHED, FAILED< MISLOAD, NOLOCATION, DELETED |
| **status_updated_at** | int64 | 0 | The epoch-millis when the status of the stop was updated |
| **route** | **Dimmunitive Route object** | {} | The Route that this stop is in. This is **dimmunitive** because only the list_route_id would be populated to non-default value if there is any association with other route values set to default. Otherwise, an empty object would be returned. |
| **route_priority** | int32 | 0 | The ordering of ths stop in the route |
| **master_address** | string | "" | The leasing office address or community address, if associative |
| **parent_list_item_id** | string | "" | The ID of the parent item if this list is in a group |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this item is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this item is last updated |
| **position** | LatLng | {} | Usually the navigate location of the address |
| **display_position** | LatLng | {} | Usually the rooftop location of the address |
| **is_external** | boolean | false | Whether or not the geocoders are external to Beans |
| **origination** | string | "" | The origin of the item, set when the item is created |
| **provider** | string | "" | The provider of the item, set when the item is created |
| **signature_required** | boolean | false | True when signature is required to close out the item |
| **url** | string | "" | Associated URL of the item |
| **source_seq** | int32 | 0 | The sequence of the item, may not be correlated in a route |
| **transfer** | string | "" | Note on whether or not this item is transferred out or tranferred in |
| **placement** | string | "" | Free form string, usually denote the placement of the item in a truck |
| **country_iso3** | string | "" | The ISO3 country code of the address |
| **customer_email** | string | "" | The email of the customer associated with this item |
| **flavors** | string | "" | Comma separated associated constrains, this is used for route planning, and is used to match, exactly, to trucks that contain all the flavors. For example, if a item has flavors "a,b", then, only trucks that has both "a", and "b" flavors can be used for this item |
| **stop_time_seconds** | int32 | 0 | The stop time, in seconds, that this item should carry |
| **transferred_in** | boolean | false | True when this item was transferred in from another stop or route |
| **transferred_out** | boolean | false | True when this item was transferred out into another route |
| **dimensions** | Dimensions object | {} | This to denote constrains on various dimensions for Route planning |
| **third_party_reference_id** | string | "" | Third party reference ID for this stop |
| **third_party_status** | string | "" | Third party reference status for this stop |

##### Dimensions Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **dims** | Array of Dimension object | [] | An Array of dimension |

##### Dimension Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **t** | string | Enum | Type of the dimension. One of WEIGHT, VOLUME, COUNT |
| **v** | string | "" | respective value of the dimension. As long as the unit is aligned with the vehicle's, a numeric is sufficient |

#### Item Documentation Callback Example

As part of the driver/dispatcher workflows, Item Documentation (PoD) may be generated, updated, or removed. For most of the use cases, UPDATE/CREATE callbacks would be generated. It is important to note that DELETE callback can also be generated when the PoD is being reset.

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

##### Item Documentation Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_item_id** | string | The id of the list item | The ID of the list item (stop) that this documentation is for |
| **list_route_id** | string | "" | The ID of the route that the item is currently on |
| **account_buid** | string | "" | The ID of the account that the item is in |
| **timestamp_epochSecond** | int64 | 0 | The timestamp in epoch when this documentation were entered into the system |
| **notes** | Array of string | [] | Notes that were put down either by agents or by system |
| **images** | Array of Image Info Object | [] | An array of images that are associated with this documentation |
| **event_code** | Event code object | {} | The chosen event code by an agent to be associated with this documentation  |
| **tags** | Array of Tag | Empty Array | A list of route tags. These are route preferences |

##### Event Code Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **code** | string | "" | The short code for the event |
| **name** | string | "" | The name for the event |

##### Image Info Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **url** | string | "" | The URL of the image where it may be downloaded |
| **type** | string | "" | The type of an image. "proof" usually denotes the proof of delivery, "signature" usually denotes the signature blocks. New types may be added in the future  |
| **position** | LatLng | {} | The lat/lng associated with the image |

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

##### Assignee Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | string | The assignee ID | The unique id of the assignee |
| **account_buid** | string | The account ID | The account ID that this assignee is in |
| **name** | string | "" | The name of this assignee |
| **email** | string | "" | The email of this assignee |
| **phone** | string | "" | The phone number of this assignee |
| **code** | string | "" | The assignee code, if configured |
| **lat** | double | 0.0 | The last known latitude of this assignee |
| **lng** | double | 0.0 | The last known longitude of this assignee |
| **state** | string | One of ACTIVE, DISABLED | The state that this assignee is in |
| **has_used_consumer_app** | boolean | false | True when the assignee has used the consumer app |
| **role** | string | One of ADMIN, DRIVER, MANAGER, DISPTCHER | The Role of this assignee  |
| **employee_id** | string | "" | The employee ID of this assignee |
| **manager_assignee_id** | string | "" | The assignee's manager ID |
| **list_warehouse_id** | string | "" | The assignee's default warehouse ID |
| **is_safety_enabled** | boolean | false | True when safety compliance is enabled for this assignee |
| **safety_status** | string | "" | The safety compliance status |
| **safety_integration_status** | string | "" | The safety provider integration status for this assignee |
| **is_assigning_enabled** | boolean | false | True when the assignee can be put on a route |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is last updated |

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

##### Assignee Vechile Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | string | "" | The assignee id if the vehicle is assigned |
| **account_buid** | string | The account ID | The account ID that this vehicle is in |
| **capacity** | int32 | 0 | The capacity of the vehicle, usually used to denote the number of packages |
| **saddress** | string | "" | The starting address of the vehicle |
| **sformatted_address** | string | "" | The starting address of the vehicle after being formatted |
| **sposition** | LatLng | {} | The geocoded LatLng of the starting address |
| **eaddress** | string | "" | The ending address of the vehicle |
| **eformatted_address** | string | "" | The ending address of the vehicle after being formatted |
| **eposition** | LatLng | {} | The ending position of the vehicle |
| **start_anywhere** | boolean | false | True if the vehicle can start from anywhere on route planning |
| **start_anytime** | boolean | false | True if the vehicle can start anytime on route planning |
| **end_anywhere** | boolean | false | True if the vehicle can end anywhere on route planning |
| **flavors** | string | "" | Comma separated to describe the capabilities of the vehicles, which must be matched for items during Route planning |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this assignee is last updated |
| **country_iso3** | string | "" | The ISO3 country code of the addresses |
| **dimensions** | Dimensions object | {} | This to denote capacity on various dimensions for Route planning |

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

##### Route What-if Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **item** | Array of Item | Empty Array | The list of items to compute |
| **list_route_ids** | Array of string | [] | The list of route IDs to compute |
| **route_size_limit** | int32 | 0 | The max number of stops for a route to be eligible. 0 means no limits |
| **must_have_assignee** | boolean | 0 | The epoch millis indicating the starting of the route |
| **request_id** | string | "" | Idempotent request ID  |
| **asynchronous** | boolean | false | True if the request was submitted to be executed asynchronously |
| **use_warehouse_as_terminal** | boolean | false | True to use warehouse as terminal stops |
| **ignore_time_constrains** | boolean | false | True to ignore the time constraints |
| **cost_limit** | Cost Limit object | {} | Only returns routes whose costs are within the limit |
| **include_multi_day_window_stops** | boolean | false | Whether the time window across multiple days are to be supported |
| **assignee_position_freshness_minutes** | int32 | 0 | Include assignees whose locations are fresher than this setting. 0 means no limits |
| **include_open_stops_outside_current_date** | boolean | false | True to include stops outside of today's date |
| **ignore_source_sequence** | boolean | false | True if the source sequence on stops were to be ignored |
| **logs** | Array of string | [] | The list of logs appended during processing |
| **status** | string | "" | The status of the request |
| **account_buid** | string | Account ID | The account identifier |
| **include_negative_delta_cost** | boolean | false | True if negative costs are allowed |
| **heuristics** | Heuristics Filter object | {} | A set of filters |
| **allow_unknown_assignee_location** | boolean | false | True to allow assignees with unknown locations |
| **pair_stops_for_flex_time_window** | boolean | false | True if the stops needs to be paired |
| **internal_ref** | string | "" | Internal reference for this request |
| **start_time_epoch** | int64 | 0 | The epoch when the request was started |
| **end_time_epoch** | int64 | 0 | The epoch when the request was completed |
| **result** | Route Delta Cost Object | {} | The result of the What if analysis |
| **completed** | boolean | false | Whether the request completed |
| **message** | string | "" | The processing message, if any |


##### Heuristics Filter object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **distance_M** | double | 0.0 | Include routes whose delta distance is less than M meters |
| **time_S** | double | 0.0 | Include routes whose delta time is less than S seconds |


##### Cost Limit object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **include_with_num_stops_N** | int32 | 0 | If route has N or less stops, it will always be included for computation |
| **proximity_to_new_stops_M** | double | 0.0 | Only include routes containing a stop that is within M meters, crows fly distance, of any one of the new stops |
| **include_all_stops** | boolean | false | True if all the stops are considered for proximity computations |


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

#### Driver Start Callback Example
```json
{
    "type": "DRIVER_START",
    "action": "CREATE",
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "object": {
        "list_assignee_id": "ca8d-0a3889d0-a756",
        "list_route_id": "e4630dbb-44f9-447c-8c5d-ba0aee0a6b82",
        "start_epoch_millis": "1670813033227"
    },
    "watermark": "1670813035543"
}

```

##### Driver Start Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | string | "" | The unique id of the assignee that starts the route |
| **list_route_id** | string | "" | The route ID that was started|
| **start_epoch_millis** | int64 | 0 | The epoch millis indicating the starting of the route |

#### Missing Info on Packages Add Example

This callback is triggered when a scanned barcode does not have sufficient amount of information for the system to resolve it to a list item.

   - a driver scans a barcode or a label
   - the system, given the barcode or a label, could not find any matching list item
   - the system would create this callback **and wait for the response**
   - the system would attempt to process the content received from the callback response
      - "list" of items
      - or a single item
   - if the item(s) received are valid, they would be created or updated
      - which itself would generate a Item callback if enabled, **asynchronously**
      - if the system could not safely handled the response, then, the callback response would be logged, and the system would return with failed label error
   - return the response to the driver scan
   
In other words, this callback would be blocking on the driver scans to await the information from the receiver of the callback.

```json
{
  "type": "BARCODE_MISSING_INFO",
  "action": "CREATE",
  "account_buid": "aCUYkl5jtq8-BrBTr3pTdzmnVQyb8Im5ODarcMg-ucyDFHSJ3D9bvdxlnbFyeoikFo2BKlATE0PPgah7IXvKqFe7TdcD_uCZdUgiMLVGqbyy6JGxPta73ZdaPjBARsfIuq65qQ",
  "object": {
    "list_assignee_id": "4heosxdisgn6dmybh2k8hm",
    "list_route_id": "19f86a7ab09036e682f2bdeeb8bde70c",
    "timestamp_millis": 1675959159679,
    "barcode": "C123456",
    "response": ""
  },
  "watermark": 1675959159679
}
```

##### Missing Info on Packages Add Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | string | "" | The unique id of the assignee that starts the route |
| **list_route_id** | string | "" | The route ID that was started|
| **timestamp_millis** | int64 | 0 | The epoch millis when the system receives the scan request |
| **barcode** | string | "" | The barcode that the system could not find information on |
| **response** | string | "" | **System** use only |