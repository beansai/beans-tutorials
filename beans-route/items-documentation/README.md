

<img src="../../assets/images/beans-128x128.png" align="right" />

# Items Documentation

Describe any documentation on list item
e.g. proof of delivery, signature, or any other documentation

## Table of contents

- [Items Documentation](#items-documentation)
  - [Get Documentation](#get-documentation)
  - [Post Documentation](#post-documentation)

## Get Documentation

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
            "type": "signatures",
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
            "type": "signatures",
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
            "type": "signatures",
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


