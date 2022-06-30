

<img src="../../assets/images/beans-128x128.png" align="right" />

# Warehouses Managements



For details of a warehouse's shape please see https://www.beansroute.ai/route-api-v1.php#warehouse-list-object


## Table of contents
- [Create Warehouses](#create-warehouses)
- [Update Warehouse](#update-warehouse)
- [Get Warehouse list](#get-warehouse-list)
- [Get Warehouse](#get-warehouse)
- [Delete Warehouse](#delete-warehouse)

### Create warehouses

**Request example**

```
POST https://isp.beans.ai/enterprise/v1/lists/warehouses
```

**Body**

```json
{
    "warehouse":
    [
        {
            "name": "Tutorial Warehouse",
            "domicile": "",
            "address": "14840 CA-4, Discovery Bay, CA 94505",
            "list_warehouse_id": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f"
        }
    ]
}
```

**Response Example**

```json
{
    "warehouse": [
        {
            "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "address": "14840 CA-4, Discovery Bay, CA 94505",
            "formattedAddress": "14840 CA-4, Discovery Bay, CA",
            "createdAt": 1643183316000,
            "updatedAt": 1643183316000,
            "position": {
                "latitude": 37.88946,
                "longitude": -121.6215
            },
            "name": "Tutorial Warehouse"
        }
    ]
}
```

### Update warehouse

**Request example**

```
POST https://isp.beans.ai/enterprise/v1/lists/warehouses/{{list-warehouse-id}}
```

**Body**

```json
{
    "name": "Tutorial Warehouse",
    "domicile": "",
    "address": "14840 CA-4, Discovery Bay, CA 94505"
}
```

**Response Example**

```json
{
    "warehouse": [
        {
            "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "address": "14840 CA-4, Discovery Bay, CA 94505",
            "formattedAddress": "14840 CA-4, Discovery Bay, CA",
            "createdAt": 1643183316000,
            "updatedAt": 1643183316000,
            "position": {
                "latitude": 37.88946,
                "longitude": -121.6215
            },
            "name": "Tutorial Warehouse"
        }
    ]
}
```

### Get Warehouse List

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/warehouses
```

**Response Example**

```json
{
    "warehouse": [
        {
            "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "address": "14840 CA-4, Discovery Bay, CA 94505",
            "formattedAddress": "14840 CA-4, Discovery Bay, CA",
            "createdAt": 1643183316000,
            "updatedAt": 1643183316000,
            "position": {
                "latitude": 37.88946,
                "longitude": -121.6215
            },
            "name": "Tutorial Warehouse"
        }
    ]
}
```

### Get Warehouse

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/warehouses/{{list-warehouse-id}}
```

**Response Example**

```json
{
    "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f2",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "address": "14840 CA-4, Discovery Bay, CA 94505",
    "formattedAddress": "14840 CA-4, Discovery Bay, CA",
    "createdAt": 1644384027000,
    "updatedAt": 1644384739000,
    "position": {
        "latitude": 37.88946,
        "longitude": -121.6215
    },
    "name": "Tutorial Warehouse2"
}
```


### Delete Warehouse
This will perform a soft-delete action, and still will still be return in get warehouse by id response.

**Request**
```
DELETE {{baseURL}}/enterprise/v1/lists/warehouse/{{list-warehouse-id}}
```

**Response**
```json
{
    "listWarehouseId": "6f4f7bf9-b878-4eda-b01d-17dfcfcdadc3e",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "address": "3790 Wilshire Blvd, Los Angeles, CA 90010, United States",
    "formattedAddress": "3790 Wilshire Blvd, Los Angeles, CA",
    "createdAt": 1656546041000,
    "updatedAt": 1656546065377,
    "position": {
        "latitude": 34.061512,
        "longitude": -118.308624
    },
    "name": "Thermopylaee"
}
```
