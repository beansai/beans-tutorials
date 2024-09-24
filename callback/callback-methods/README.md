

<img src="../../assets/images/beans-128x128.png" align="right" />

# Callback Methods


## Table of contents
- [Callback Methods](#callback-methods)
  - [Get Callbacks](#get-callbacks)
  - [Get Callback by id](#get-callback-by-id)
  - [Rerun Callback](#rerun-callback)

## Get Callbacks

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/callbacks?startMillisInclusive={{millisecond}}}&endMillisExclusive={{millisecond}}
```

**Response Example**

```json
{
    "logs": [
        {
            "uuid": "df6476e10e654fa6bb9f2569eaa35166",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "log": "{\"type\":\"ASSIGNEE_VEHICLE\",\"action\":\"UPDATE\",\"account_buid\":\"4022a1aada0e4c4684e61e3f73290a68\",\"object\":{\"list_assignee_id\":\"ca8d-0a3889d0-a756\",\"capacity\":16,\"updated_at\":\"1646313322186\",\"dimensions\":{}},\"watermark\":\"1646313322186\"}",
            "config": {
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "account": true,
                "route": true,
                "item": true,
                "assignee": true,
                "warehouse": true,
                "assigneeVehicle": true,
                "globalUrl": "https://b3d4-36-237-95-112.ngrok.io",
                "routeWhatifAsync": true
            },
            "watermark": 1646313322186,
            "type": "ASSIGNEE_VEHICLE",
            "tsMillis": 1646313322000
        },
        {
            "uuid": "32f034f26a50442b8db6a13114b39065",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "log": "{\"type\":\"ITEM\",\"action\":\"CREATE\",\"account_buid\":\"4022a1aada0e4c4684e61e3f73290a68\",\"object\":{\"list_item_id\":\"p9xs-8eca53fefb635f19958ab0cbf4\",\"address\":\"600 Driscoll Rd, Fremont, CA 94539, United States\",\"formatted_address\":\"600 Driscoll Rd, Fremont, CA\",\"status\":\"NEW\",\"updated_at\":\"1646313991048\",\"status_updated_at\":\"1646313991896\",\"route\":{\"list_route_id\":\"ca8daa7f-0625-4ebe-9b57-6314e6746fef\"},\"route_priority\":6,\"type\":\"PICKUP\",\"position\":{\"lat\":0.01,\"lng\":179.99},\"display_position\":{\"lat\":0.01,\"lng\":179.99},\"address_components\":{\"city\":\"Fremont\",\"state\":\"CA\",\"zipcode\":\"94539\",\"country\":\"USA\",\"street\":\"600 Driscoll Rd\"},\"is_external\":true,\"url\":\"#_beans-status\",\"dimensions\":{}},\"watermark\":\"1646313991048\"}",
            "config": {
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "account": true,
                "route": true,
                "item": true,
                "assignee": true,
                "warehouse": true,
                "assigneeVehicle": true,
                "globalUrl": "https://b3d4-36-237-95-112.ngrok.io",
                "routeWhatifAsync": true
            },
            "watermark": 1646313991048,
            "type": "ITEM",
            "tsMillis": 1646313993000
        }
    ]
}
```
| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **uuid** | string | The Callback ID | The unique id of the callback |
| **accountBuid** | string | The Account ID | The Account id that this callback is in |
| **log** | string | The Callback Envelope | The envelope of callback, please see [Callback Examples](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#callback-examples) |
| **config** | string | The Callback Config | The config of callback, please see [Callback Configs](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#callback-configs) |
| **type** | enum | The Callback Type | Types of callback, please see [Callback Enumerations](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#enumerations) |
| **watermark** | long | 0 | The watermark of the callback. The system ensures that the value of the watermark is strictly increasing. In other words, if the receiver of the callback receives a message on the same object with earlier watermark, the receiver can safely assume that payload represented an earlier version of the object. |
| **tsMillis** | long | 0 | The timestamp, in epoch-millis, when this callback log is created |


## Get Callback by id

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/callbacks/{{callback-id}}
```

**Response Example**

```json
{
    "uuid": "df6476e10e654fa6bb9f2569eaa35166",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "log": "{\"type\":\"ASSIGNEE_VEHICLE\",\"action\":\"UPDATE\",\"account_buid\":\"4022a1aada0e4c4684e61e3f73290a68\",\"object\":{\"list_assignee_id\":\"ca8d-0a3889d0-a756\",\"capacity\":16,\"updated_at\":\"1646313322186\",\"dimensions\":{}},\"watermark\":\"1646313322186\"}",
    "config": {
        "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
        "account": true,
        "route": true,
        "item": true,
        "assignee": true,
        "warehouse": true,
        "assigneeVehicle": true,
        "globalUrl": "https://b3d4-36-237-95-112.ngrok.io",
        "routeWhatifAsync": true
    },
    "watermark": 1646313322186,
    "type": "ASSIGNEE_VEHICLE",
    "tsMillis": 1646313322000
}
```

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **uuid** | string | The Callback ID | The unique id of the callback |
| **accountBuid** | string | The Account ID | The Account id that this callback is in |
| **log** | string | The Callback Envelope | The envelope of callback, please see [Callback Examples](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#callback-examples) |
| **config** | string | The Callback Config | The config of callback, please see [Callback Configs](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#callback-configs) |
| **type** | enum | The Callback Type | Types of callback, please see [Callback Enumerations](https://github.com/beansai/beans-tutorials/tree/main/callback/callback-configs#enumerations) |
| **watermark** | long | 0 | The watermark of the callback. The system ensures that the value of the watermark is strictly increasing. In other words, if the receiver of the callback receives a message on the same object with earlier watermark, the receiver can safely assume that payload represented an earlier version of the object. |
| **tsMillis** | long | 0 | The timestamp, in epoch-millis, when this callback log is created |

## Rerun Callback

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/callbacks_rerun
```

**Body**
```json
{
    "startMillisInclusive":"1646313000000",
    "endMillisExclusive":"1646320000000"
}
```
| Field | Type | Description |
| --- | --- | --- |
| **startMillisInclusive** | long | The start epoch milli-second of the time window, inclusive |
| **endMillisExclusive** | long | The end epoch milli-second of the time window, exclusive |
| **type** | string | The type of the Callback object, and if not specified, all of them. |

**Response Example**
```json
{
    "logs": [
        {
            "uuid": "df6476e10e654fa6bb9f2569eaa35166",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "log": "{\"type\":\"ASSIGNEE_VEHICLE\",\"action\":\"UPDATE\",\"account_buid\":\"4022a1aada0e4c4684e61e3f73290a68\",\"object\":{\"list_assignee_id\":\"ca8d-0a3889d0-a756\",\"capacity\":16,\"updated_at\":\"1646313322186\",\"dimensions\":{}},\"watermark\":\"1646313322186\"}",
            "config": {
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "account": true,
                "route": true,
                "item": true,
                "assignee": true,
                "warehouse": true,
                "assigneeVehicle": true,
                "globalUrl": "https://b3d4-36-237-95-112.ngrok.io",
                "routeWhatifAsync": true
            },
            "watermark": 1646313322186,
            "type": "ASSIGNEE_VEHICLE",
            "tsMillis": 1646313322000,
            "responseStatus": 502,
            "response": "\n<!doctype html5>\n<html>\n    <head>\n        <style type=\"text/css\">\n         \n        strong { font-weight: bold; }\n        hr { -moz-box-sizing: content-box; box-sizing: content-box; height: 0; }\n        html { font-family: sans-serif;   -ms-text-size-adjust: 100%;   -webkit-text-size-adjust: 100%;   } body { margin: 0; }\n        a { background-color: transparent; }\n        a:active, a:hover { outline: 0; }\n        </style>\n\n        <style type=\"text/css\">\n            body { background-color: #f5f5f5; }\n            .container { width: 500px; margin: auto; color: #444; padding: 5px; }\n            a, strong { color: purple; text-decoration: none; }\n            a:hover { text-decoration: underline; }\n            h2 { text-align: center; color: #000; }\n            p { line-height: 20px; }\n        </style>\n    </head>\n    <body>\n        <div class=\"container\">\n            \n            \n<h2>Failed to complete tunnel connection</h2>\n<hr />\n<p>\n    The connection to <strong><a href=\"http://29eb-101-9-39-166.ngrok.io\">http://29eb-101-9-39-166.ngrok.io</a></strong>\n    was successfully tunneled to your ngrok client,\n    but the client failed to establish a connection to\n    the local address <strong><a href=\"http://localhost:8080\">localhost:8080</a></strong>.\n</p>\n<p>\n    Make sure that a web service is running on\n    <strong><a href=\"http://localhost:8080\">localhost:8080</a></strong> and that it is a valid address.\n</p>\n<p>\n    The error encountered was: <strong style=\"color: #9E2929\">dial tcp [::1]:8080: connect: connection refused</strong>\n</p>\n\n            \n        </div>\n    </body>\n</html>\n"
        },
        {
            "uuid": "32f034f26a50442b8db6a13114b39065",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "log": "{\"type\":\"ITEM\",\"action\":\"CREATE\",\"account_buid\":\"4022a1aada0e4c4684e61e3f73290a68\",\"object\":{\"list_item_id\":\"p9xs-8eca53fefb635f19958ab0cbf4\",\"address\":\"600 Driscoll Rd, Fremont, CA 94539, United States\",\"formatted_address\":\"600 Driscoll Rd, Fremont, CA\",\"status\":\"NEW\",\"updated_at\":\"1646313991048\",\"status_updated_at\":\"1646313991896\",\"route\":{\"list_route_id\":\"ca8daa7f-0625-4ebe-9b57-6314e6746fef\"},\"route_priority\":6,\"type\":\"PICKUP\",\"position\":{\"lat\":0.01,\"lng\":179.99},\"display_position\":{\"lat\":0.01,\"lng\":179.99},\"address_components\":{\"city\":\"Fremont\",\"state\":\"CA\",\"zipcode\":\"94539\",\"country\":\"USA\",\"street\":\"600 Driscoll Rd\"},\"is_external\":true,\"url\":\"#_beans-status\",\"dimensions\":{}},\"watermark\":\"1646313991048\"}",
            "config": {
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "account": true,
                "route": true,
                "item": true,
                "assignee": true,
                "warehouse": true,
                "assigneeVehicle": true,
                "globalUrl": "https://b3d4-36-237-95-112.ngrok.io",
                "routeWhatifAsync": true
            },
            "watermark": 1646313991048,
            "type": "ITEM",
            "tsMillis": 1646313993000,
            "responseStatus": 502,
            "response": "\n<!doctype html5>\n<html>\n    <head>\n        <style type=\"text/css\">\n         \n        strong { font-weight: bold; }\n        hr { -moz-box-sizing: content-box; box-sizing: content-box; height: 0; }\n        html { font-family: sans-serif;   -ms-text-size-adjust: 100%;   -webkit-text-size-adjust: 100%;   } body { margin: 0; }\n        a { background-color: transparent; }\n        a:active, a:hover { outline: 0; }\n        </style>\n\n        <style type=\"text/css\">\n            body { background-color: #f5f5f5; }\n            .container { width: 500px; margin: auto; color: #444; padding: 5px; }\n            a, strong { color: purple; text-decoration: none; }\n            a:hover { text-decoration: underline; }\n            h2 { text-align: center; color: #000; }\n            p { line-height: 20px; }\n        </style>\n    </head>\n    <body>\n        <div class=\"container\">\n            \n            \n<h2>Failed to complete tunnel connection</h2>\n<hr />\n<p>\n    The connection to <strong><a href=\"http://29eb-101-9-39-166.ngrok.io\">http://29eb-101-9-39-166.ngrok.io</a></strong>\n    was successfully tunneled to your ngrok client,\n    but the client failed to establish a connection to\n    the local address <strong><a href=\"http://localhost:8080\">localhost:8080</a></strong>.\n</p>\n<p>\n    Make sure that a web service is running on\n    <strong><a href=\"http://localhost:8080\">localhost:8080</a></strong> and that it is a valid address.\n</p>\n<p>\n    The error encountered was: <strong style=\"color: #9E2929\">dial tcp [::1]:8080: connect: connection refused</strong>\n</p>\n\n            \n        </div>\n    </body>\n</html>\n"
        }
    ]
}
```








