

<img src="../../assets/images/beans-128x128.png" align="right" />

# Items Documentation

Item Documentation introduces the basic idea of contextual documentation that often accompany a piece of work or task. Since a piece of work/task in our ecosystem is currently modeled as a List Item, we are terming this set of API's Item Documentation.

For example, when a package is dropped of, the driver could ask the recipient of the package for signatures AND encode status of the package as part of the documentation.

## Table of contents

- [Items Documentation](#items-documentation)
  - [Get Item Documentation](#get-item-documentation)
  - [Search Item Documentation By Tracking ID](#search-item-documentation-by-tracking-id)
  - [Post Item Documentation](#post-item-documentation)
  - [Objects](#objects)
    - [Item Documentation Object](#item-documentation-object)
    - [Event Code Object](#event-code-object)
    - [Image Info Object](#image-info-object)
  - [Notes](#notes)

## Get Item Documentation

**Request Example**

```
GET {{baseURL}}/enterprise/v1/lists/itemsdocumentation/{list-item-id}
```

**Response Example**

```json
{
    "listItemId": "47e56245-0a78-4cb9-a268-83fa2f247d91-01",
    "listRouteId": "47e56245-0a78-4cb9-a268-83fa2f247d91",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "timestampEpochSecond": 1669118402,
    "notes": [
        "note 1",
        "note 2"
    ],
    "images": [
        {
            "url": "https://storage.googleapis.com/beans-images/testing/small/2022-11-22/2022-11-22_b27d61c6-21d8-4188-a0e2-f184360907d2.png",
            "type": "signature",
            "position": {
                "latitude": 38.003654,
                "longitude": -121.783137
            }
        }
    ],
    "eventCode": {
        "code": "101",
        "name": "received"
    },
    "tags": [
        {
            "key": "is_in_time",
            "value": "true"
        }
    ]
}
```

## Search Item Documentation by Tracking ID

**Request Example**

```
GET {{baseURL}}/enterprise/v1/lists/itemsdocumentation?tracking_id=08342343
```

**Response Example**

```json
{
  "pod": [
    {
      "listItemId": "372a629f-a0ed-4b01-91fe-238009c1567b",
      "listRouteId": "6022e66f-fd73-4497-bb04-0f946591e376",
      "accountBuid": "902592b7-6888-4599-9f21-ae112fe09c09",
      "timestampEpochSecond": 1697832840,
      "eventCode": {
        "code": "DELIVERED",
        "name": "delivered"
      },
      "generatedFrom": "APP",
      "generatedBy": "driver@example.com",
      "podTimestampEpoch": 1697832838,
      "listAssigneeId": "0f07d2d1-8de6-4409-a21d-aa670782ca5d",
      "tags": [
        {
          "key": "/FEDEX/package_size",
          "value": "regular"
        }
      ],
      "ts": 1697822840000
    }
  ]
}
```

## Post Item Documentation

**Request Example**

```
POST {{baseURL}}/enterprise/v1/lists/itemsdocumentation
```

**Body**

```json
{
    "account_buid": "4022a1aada0e4c4684e61e3f73290a68",
    "list_route_id": "47e56245-0a78-4cb9-a268-83fa2f247d91",
    "list_item_id": "47e56245-0a78-4cb9-a268-83fa2f247d91-01",
    "timestamp_epochSecond": 1669118402,
    "notes": [
        "note 1",
        "note 2"
    ],
    "images": [
        {
            "url": "https://storage.googleapis.com/beans-images/testing/small/2022-11-22/2022-11-22_b27d61c6-21d8-4188-a0e2-f184360907d2.png",
            "type": "signature",
            "position": {
                "lat": "38.003654",
                "lng": "-121.783137"
            }
        }
    ],
    "event_code": {
        "code": "101",
        "name": "received"
    },
    "tags": [
        {
            "key": "is_in_time",
            "value": "true"
        }
    ]
}
```



**Response Example**
```json
{
    "listItemId": "47e56245-0a78-4cb9-a268-83fa2f247d91-01",
    "listRouteId": "47e56245-0a78-4cb9-a268-83fa2f247d91",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "timestampEpochSecond": 1669118402,
    "notes": [
        "note 1",
        "note 2"
    ],
    "images": [
        {
            "url": "https://storage.googleapis.com/beans-images/testing/small/2022-11-22/2022-11-22_b27d61c6-21d8-4188-a0e2-f184360907d2.png",
            "type": "signature",
            "position": {
                "latitude": 38.003654,
                "longitude": -121.783137
            }
        }
    ],
    "eventCode": {
        "code": "101",
        "name": "received"
    },
    "tags": [
        {
            "key": "is_in_time",
            "value": "true"
        }
    ]
}
```

## Objects
### Item Documentation Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **listItemId** | string | The id of the list item | The ID of the list item (stop) that this documentation is for |
| **listRouteId** | string | "" | The ID of the route that the item is currently on |
| **accountBuid** | string | "" | The ID of the account that the item is in |
| **timestampEpochSecond** | int64 | 0 | The timestamp in epoch when this documentation were entered into the system |
| **notes** | Array of string | [] | Notes that were put down either by agents or by system |
| **images** | Array of Image Info Object | [] | An array of images that are associated with this documentation |
| **eventCode** | Event code object | {} | The chosen event code by an agent to be associated with this documentation  |
| **tags** | Array of Tag | Empty Array | A list of route tags. These are route preferences |
| **pod_timestamp_epoch** | Timestamp epoch | 0 | The timestamp of which the documentation is recorded |
| **labels** | Array of Label | Empty Array | A list of label objects that are associated with the Item Documentation |
| **consignee_name** | Array of Label | Empty Array | A list of label objects that are associated with the Item Documentation |

### Event Code Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **code** | string | "" | The short code for the event |
| **name** | string | "" | The name for the event |

### Image Info Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **url** | string | "" | The URL of the image where it may be downloaded |
| **type** | string | "" | The type of an image. "proof" usually denotes the proof of delivery, "signature" usually denotes the signature blocks. New types may be added in the future  |
| **position** | LatLng | {} | The lat/lng associated with the image |

### Label Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **barcode** | string | "" | The barcode string |

## Notes

A documentation is always in context of a list item
- There could be multiple images
- There could be multiple notes
- Tags are used for domain specific considerations (e.g package size, dimension) that is not sufficiently general
- Image type can really be anything, though the common ones are:
  - proof
  - signature
  - exception
