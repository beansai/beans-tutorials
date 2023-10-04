

<img src="../../assets/images/beans-128x128.png" align="right" />

# Stops Management



For details of a stop (Item)  please see https://www.beansroute.ai/route-api-v1.php#item-list-object


## Table of contents
- [Create Stops](#create-stops)
- [Update Stop](#update-stop)
- [Get Stop List](#get-stop-list)
- [Get Stops By Route ID](#get-stops-by-route-id)
- [Get Stop](#get-stop)
- [Delete Stop](#delete-stop)
- [Get all item IDs from a Route that have documentations](#get-all-item-ids-from-a-route-that-have-documentations)
- [Get Item Documentation](#get-item-documentation)
- [Search Archived Items](#search-archived-items)
- [Objects](#objects)
  - [Array of List Item Object](#array-of-list-item-object)
  - [List Item Object](#list-item-object)
  - [Dimensions Object](#dimensions-object)
  - [Dimension Object](#dimension-object)

## Create Stops

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/items
```

**Body**
- list_item_id - ID of listItem, it is unique within the account.
- address - The address of the item.
- type - Either of DROPOFF of PICKUP
- deliver_from_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- deliver_to_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- placement - we can use this to denote the stop which size is varchar(64)

```json
{
  "item": [
    {
      "list_item_id": "d3f6-a801b3605afbd726df743cc66",
      "address": "3365 Deer Valley Rd, Antioch, CA 94531",
      "route": {
        "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
      },
      "type":"PICKUP",
      "deliver_from_str":"2033-01-01 13:00",
      "deliver_by_str":"2033-01-01 18:00",
      "placement":"T:R"
    },
    {
      "list_item_id": "d3f6-8eca53fefb635f19958ab0cbf",
      "address": "4320 E Summer Lake Dr, Oakley, CA 94561",
      "route": {
        "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
      },
      "type":"DROPOFF",
      "deliver_from_str":"2033-01-01 07:00",
      "deliver_by_str":"2033-01-01 11:00",
      "placement":"T:R"
    }
  ]
}

```

**Response Example**

```json
{
    "item": [
        {
            "listItemId": "d3f6-a801b3605afbd726df743cc66",
            "address": "3365 Deer Valley Rd, Antioch, CA 94531",
            "formattedAddress": "3365 Deer Valley Rd, Antioch, CA",
            "status": "NEW",
            "updatedAt": 1644400351640,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 6,
            "type": "PICKUP",
            "position": {
                "latitude": 37.98784,
                "longitude": -121.78451
            },
            "displayPosition": {
                "latitude": 37.98784,
                "longitude": -121.78445
            },
            "deliverFromStr": "2033-01-01 13:00",
            "deliverByStr": "2033-01-01 18:00",
            "addressComponents": {
                "zipcode": "94531",
                "countryIso3": "USA"
            },
            "placement":"T:R"
        }
    ],
    "route": [
        {
            "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "createdAt": 1643267000000,
            "updatedAt": 1644400352000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "14840 CA-4, Discovery Bay, CA 94505",
                "formattedAddress": "14840 CA-4, Discovery Bay, CA",
                "createdAt": 1643183316000,
                "updatedAt": 1644388049000,
                "position": {
                    "latitude": 37.88946,
                    "longitude": -121.6215
                },
                "name": "Tutorial Warehouse 2"
            },
            "routePathMd5": "ea1cee82a254c506a74b6c5ec889168c",
            "dateStr": "2023-01-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE"
        }
    ]
}
```

## Update Stop

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Body**
- list_item_id - ID of listItem, it is unique within the account.
- address - The address of the item.
- type - Either of DROPOFF of PICKUP
- deliver_from_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- deliver_to_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- placement - we can use this to denote the stop which size is varchar(64)

  <b>VERY IMPORTANT</b> This performs a whole object replacements, and thus, if you wish to maintain existing values, they need to be passed in as well to maintain their value. Otherwise, type default would be used.

```json
{
    "address": "3365 Deer Valley Rd, Antioch, CA 94532",
    "route": {
    "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
    },
    "type":"DROPOFF",
    "deliver_from_str":"2033-01-01 13:00",
    "deliver_by_str":"2033-01-01 18:00",
    "placement":"T:R"
}
```

**Response Example**

```json
{
    "item": [
        {
            "listItemId": "d3f6-a801b3605afbd726df743cc66",
            "address": "3365 Deer Valley Rd, Antioch, CA 94532",
            "formattedAddress": "3365 Deer Valley Rd, Antioch, CA",
            "status": "NEW",
            "updatedAt": 1644400495083,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 6,
            "type": "DROPOFF",
            "position": {
                "latitude": 37.98784,
                "longitude": -121.78451
            },
            "displayPosition": {
                "latitude": 37.98784,
                "longitude": -121.78445
            },
            "deliverFromStr": "2033-01-01 13:00",
            "deliverByStr": "2033-01-01 18:00",
            "addressComponents": {
                "zipcode": "94531",
                "countryIso3": "USA"
            },
            "placement":"T:R"
        }
    ]
}
```

## Get Stop List

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/items
```

**Response**

```json
{
    "item": [
        {
            "listItemId": "d3f6-b4d913523baaee8f2ba5e1a25",
            "address": "1923 Delta Rd, Knightsen, CA 94548",
            "formattedAddress": "1923 Delta Rd, Knightsen, CA",
            "status": "NEW",
            "updatedAt": 1644400352000,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 4,
            "type": "DROPOFF",
            "position": {
                "latitude": 37.96883,
                "longitude": -121.6603
            },
            "displayPosition": {
                "latitude": 37.96792,
                "longitude": -121.6603
            },
            "deliverFromStr": "2033-01-01 07:00",
            "deliverByStr": "2033-01-01 11:00",
            "addressComponents": {
                "zipcode": "94548",
                "countryIso3": "USA"
            }
        }
    ]
}
```

## Get Stops By Route ID
To get non-deleted items by route id.

**Request**
```
GET {{baseURL}}/enterprise/v1/lists/routes/{{list-route-id}}/items
```

**Response Example**
```json
{
    "item": [
        {
            "listItemId": "a3cc1ed-4",
            "address": "9404 Central Ave, Montclair, CA 91763, United States",
            "formattedAddress": "9404 Central Ave, Montclair, CA",
            "status": "NEW",
            "updatedAt": 1655347418000,
            "statusUpdatedAt": 1655346404000,
            "route": {
                "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
            },
            "type": "DROPOFF",
            "parentListItemId": "e20c85d1b155327a973e5fa41f0bd08d",
            "position": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "displayPosition": {
                "latitude": 34.082443,
                "longitude": -117.690918
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
        {
            "listItemId": "e20c85d1b155327a973e5fa41f0bd08d",
            "address": "9404 Central Ave, Montclair, CA",
            "notes": "Autogenerated by optimizer",
            "formattedAddress": "9404 Central Ave, Montclair, CA",
            "status": "NEW",
            "updatedAt": 1655347418000,
            "statusUpdatedAt": 1655347418000,
            "route": {
                "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
            },
            "routePriority": -1,
            "trackingId": "NA, NA, NA, NA",
            "numPackages": 4,
            "type": "DROPOFF",
            "children": [
                {
                    "listItemId": "a3cc1ed-4",
                    "address": "9404 Central Ave, Montclair, CA 91763, United States",
                    "formattedAddress": "9404 Central Ave, Montclair, CA",
                    "status": "NEW",
                    "updatedAt": 1655347418000,
                    "statusUpdatedAt": 1655346404000,
                    "route": {
                        "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
                    },
                    "type": "DROPOFF",
                    "parentListItemId": "e20c85d1b155327a973e5fa41f0bd08d",
                    "position": {
                        "latitude": 34.082443,
                        "longitude": -117.690918
                    },
                    "displayPosition": {
                        "latitude": 34.082443,
                        "longitude": -117.690918
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
            ],
            "position": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "displayPosition": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "addressComponents": {
                "city": "Montclair",
                "state": "CA",
                "zipcode": "91763",
                "street": "9404 Central Ave",
                "countryIso3": "USA"
            },
            "sourceSeq": -1,
            "countryIso3": "USA"
        }
    ]
}
```

## Get Stop

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Response Example**

```json
{
    "listItemId": "d3f6-b4d913523baaee8f2ba5e1a25",
    "address": "1923 Delta Rd, Knightsen, CA 94548",
    "formattedAddress": "1923 Delta Rd, Knightsen, CA",
    "status": "NEW",
    "updatedAt": 1644400352000,
    "statusUpdatedAt": 1643267011000,
    "route": {
        "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
    },
    "routePriority": 4,
    "type": "DROPOFF",
    "position": {
        "latitude": 37.96883,
        "longitude": -121.6603
    },
    "displayPosition": {
        "latitude": 37.96792,
        "longitude": -121.6603
    },
    "deliverFromStr": "2033-01-01 07:00",
    "deliverByStr": "2033-01-01 11:00",
    "addressComponents": {
        "zipcode": "94548",
        "countryIso3": "USA"
    }
}
```

## Delete Stop
This will perform a soft-delete action, and the stop will still be return in the get item by listItemId response 
with status "DELETED".

**Request Example**
```
DELETE {{baseURL}}/enterprise/v1/lists/items/{{list-item-id}}
```
**Response Example**
```
{
    "listItemId": "a3cc1ed-3",
    "address": "9404 Central Ave, Montclair, CA 91763, United States",
    "formattedAddress": "9404 Central Ave, Montclair, CA",
    "status": "DELETED",
    "updatedAt": 1655347418000,
    "statusUpdatedAt": 1655346404000,
    "route": {
        "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
    },
    "type": "DROPOFF",
    "parentListItemId": "e20c85d1b155327a973e5fa41f0bd08d",
    "position": {
        "latitude": 34.082443,
        "longitude": -117.690918
    },
    "displayPosition": {
        "latitude": 34.082443,
        "longitude": -117.690918
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
```


## Get all item IDs from a Route that have documentations
An item is deemed to have documentation when there is a non-trivial (so, non empty) note, and a non-trivial image url.

**Request Example**
```
{{baseURL}}/enterprise/v1/lists/itemidswithdocumentation_byroute/{{route-id}}
```

**Response Example**
```json
{
    "listItemIds": [
        "ca8d-fae5d3b6b9c9f2f1a14c43b0a1"
    ]
}
```

## Get Item Documentation

Item document introduces the basic idea of contextual documentation that often 
accompany a pice of work or task. Since a piece of work/task in our ecosystem 
is currently modeled as a List Item, we are terming it Item Documentation.

For example, when a package is dropped of, the driver could ask the recipient of 
the package for signatures AND encode status of the package as part of the documentation.

**Request Example**
```
GET {{baseURL}}/enterprise/v1/lists/itemsdocumentation/{{list-item-id}}
```

**Response Example**
- image type
  - proof
  - signature
  - exception

```json
{
    "listItemId": "ca8d-fae5d3b6b9c9f2f1a14c43b0a1",
    "listRouteId": "ca8daa7f-0625-4ebe-9b57-6314e6746fef",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "timestampEpochSecond": 1646264551,
    "notes": [
        "014-DroppedOfAtCustomer"
    ],
    "images": [
        {
            "url": "https://storage.googleapis.com/beans-images/testing/original/2022-03-02/2022-03-02_b695d615-4d32-4222-ba34-f34a68f1cee4.png",
            "type": "proof",
            "position": {
                "latitude": 20.2,
                "longitude": -30.2
            }
        }
    ],
    "eventCode": {
        "code": "014",
        "name": "DroppedOfAtCustomer"
    },
    "tags": [
        {
            "key": "/FEDEX/package_size",
            "value": "large"
        }
    ]
}
```


## Search Archived Items
**Request Example**
```
GET {{baseURL}}/enterprise/v1/lists/items/do/search?date_from=2021-01-01&date_to=2022-07-01
```
Available filters for query
- date_from - in yyyy-MM-dd format(required)
- date_to - in yyyy-MM-dd format(required)
- route_name - optional
- address - optional
- package_number - optional
- assignee_name - optional

**Response Example**
```json
{
    "item": [
        {
            "listItemId": "april-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808-01",
            "address": "112 N GAGE AVE.,LOS ANGELES",
            "formattedAddress": "112 N Gage Ave, Los Angeles, CA",
            "status": "NEW",
            "updatedAt": 1652077858000,
            "statusUpdatedAt": 1649832929000,
            "route": {
                "listRouteId": "april-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "name": "Route April",
                "status": "CLOSED",
                "createdAt": 1649832900000,
                "updatedAt": 1652077858000,
                "warehouse": {
                    "listWarehouseId": "6f4f7bf9-b878-4eda-b01d-17dfcfcdadc3",
                    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                    "address": "3790 Wilshire Blvd, Los Angeles, CA 90010, United States",
                    "formattedAddress": "3790 Wilshire Blvd, Los Angeles, CA",
                    "createdAt": 1649284672000,
                    "updatedAt": 1649284672000,
                    "position": {
                        "latitude": 34.06169,
                        "longitude": -118.30861
                    },
                    "name": "Thermopylae"
                },
                "routePathMd5": "1981e263541a90c2e7244d73ccc740ee",
                "dateStr": "2022-06-13",
                "startMode": "WAREHOUSE",
                "endMode": "WAREHOUSE"
            },
            "routePriority": 1,
            "type": "DROPOFF",
            "position": {
                "latitude": 34.03642,
                "longitude": -118.18464
            },
            "displayPosition": {
                "latitude": 34.03643,
                "longitude": -118.18443
            },
            "deliverFromStr": "2022-04-13 08:00",
            "deliverByStr": "2022-04-13 09:00",
            "addressComponents": {
                "city": "Los Angeles",
                "state": "CA",
                "zipcode": "90063-2306",
                "street": "112 N Gage Ave",
                "countryIso3": "USA"
            },
            "sourceSeq": 1,
            "countryIso3": "USA"
        }
    ]
}

```

## Objects

### Array of List Item Object
| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **item** | Array of List Item object | [] | A list of List Item Object |

### List Item Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **listItemId** | string | The item ID | The unique id of the item |
| **accountBuid** | string | The account ID | The account ID that this item is in |
| **address** | string | "" | The original address for this item |
| **unit** | string | "" | The original unit for this item, or secondary address line |
| **notes** | string | "" | The notes associated with this item, this is free form text |
| **formattedAddress** | string | "" | Formatted address for this item, often is generated and cleaned during geocoding process if geocoder is enabled |
| **deliverFromStr** | string | "" | The start of the time window that this item could be done by |
| **deliverByStr** | string | "" | The end of the time window that this item should be done by |
| **trackingId** | string | "" | The tracking ID of the stop |
| **numPackages** | int32 | 0 | The number of packages associated with this stop |
| **type** | string | Enum | One of PICKUP, DROPOFF |
| **customerName** | string | "" | The name of the customer associated with this item |
| **customerPhone** | string | "" | The phone number of the customer associated with this item |
| **status** | string | Enum | One of NEW, IN_PROCESS, FINISHED, FAILED< MISLOAD, NOLOCATION, DELETED |
| **statusUpdatedAt** | int64 | 0 | The epoch-millis when the status of the stop was updated |
| **route** | **Dimmunitive Route object** | {} | The Route that this stop is in. This is **dimmunitive** because only the list_route_id would be populated to non-default value if there is any association with other route values set to default. Otherwise, an empty object would be returned. |
| **routePriority** | int32 | 0 | The ordering of ths stop in the route |
| **masterAddress** | string | "" | The leasing office address or community address, if associative |
| **parentListItemId** | string | "" | The ID of the parent item if this list is in a group |
| **createdAt** | int64 | 0L | The timestamp, in epoch-millis, when this item is created |
| **updatedAt** | int64 | 0L | The timestamp, in epoch-millis, when this item is last updated |
| **position** | LatLng | {} | Usually the navigate location of the address |
| **displayPosition** | LatLng | {} | Usually the rooftop location of the address |
| **isExternal** | boolean | false | Whether or not the geocoders are external to Beans |
| **origination** | string | "" | The origin of the item, set when the item is created |
| **provider** | string | "" | The provider of the item, set when the item is created |
| **signatureRequired** | boolean | false | True when signature is required to close out the item |
| **url** | string | "" | Associated URL of the item |
| **sourceSeq** | int32 | 0 | The sequence of the item, may not be correlated in a route |
| **transfer** | string | "" | Note on whether or not this item is transferred out or tranferred in |
| **placement** | string | "" | Free form string, usually denote the placement of the item in a truck |
| **countryIso3** | string | "" | The ISO3 country code of the address |
| **customerEmail** | string | "" | The email of the customer associated with this item |
| **flavors** | string | "" | Comma separated associated constrains, this is used for route planning, and is used to match, exactly, to trucks that contain all the flavors. For example, if a item has flavors "a,b", then, only trucks that has both "a", and "b" flavors can be used for this item |
| **stopTimeSeconds** | int32 | 0 | The stop time, in seconds, that this item should carry |
| **transferredIn** | boolean | false | True when this item was transferred in from another stop or route |
| **transferredOut** | boolean | false | True when this item was transferred out into another route |
| **dimensions** | Dimensions object | {} | This to denote constrains on various dimensions for Route planning |
| **thirdPartyReferenceId** | string | "" | Third party reference ID for this stop |
| **thirdPartyStatus** | string | "" | Third party reference status for this stop |

### Dimensions Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **dims** | Array of Dimension object | [] | An Array of dimension |

### Dimension Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **t** | string | Enum | Type of the dimension. One of WEIGHT, VOLUME, COUNT |
| **v** | string | "" | respective value of the dimension. As long as the unit is aligned with the vehicle's, a numeric is sufficient |

