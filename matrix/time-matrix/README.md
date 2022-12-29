
<img src="../assets/images/beans-128x128.png" align="right" />

# Time Matrix

![Stops](assets/images/stops.png)

When you have many stops and want to determine the travel time among them at once,

Time Matrix would be helpful to you.

## Table of contents
- [Time Matrix](#time-matrix)
  - [Example of Specified sources and destinations](#example-of-specified-sources-and-destinations)
  - [Example of All Possibilities](#example-of-all-possibilities)
  - [Example of Additional stops](#example-of-additional-stops)
  - [Request Payloads](#request-payloads)
  - [Importance](#importance)

## Example of Specified sources and destinations
![Stops](assets/images/stops-part.png)
Let's say we have 6 stops which 3 are sources and 3 are destinations,
we will make a calculation request then get the result.

**Send Calculation Request**

```
POST {{baseURL}}/enterprise/v1/dro/time_matrix
```

**Body**
```json
{
    "requestId": "matrix-time-1",
    "points": [
        {
            "position":
            {
                "latitude": 37.996333094327554,
                "longitude": -121.70646459893086
            }
        },
        {
            "position":
            {
                "latitude": 37.96858164318102,
                "longitude": -121.6959508962403
            }
        },
        {
            "position":
            {
                "latitude": 37.8966488871678,
                "longitude": -121.69619540095405
            }
        },
        {
            "position":
            {
                "latitude": 37.925198993623624,
                "longitude": -121.77883799480549
            }
        },
        {
            "position":
            {
                "latitude": 37.966075787314864,
                "longitude": -121.78128304194283
            }
        },
        {
            "position":
            {
                "latitude": 38.011938673071406,
                "longitude": -121.80597801802993
            }
        }
    ],
    "sourcesIdx": [
        0,1,2
    ],
    "destinationsIdx": [
        3,4,5
    ],
    "asynchronous": true,
    "countryIso3": "USA"
}
```

**Get Calculation Result**
```
GET {{baseURL}}/enterprise/v1/dro/time_matrix/{{requestId}}
```

**Response**

```json
{
    "rows": [
        {
            "value": [
                933.1,
                804.9,
                567.9
            ]
        },
        {
            "value": [
                822.7,
                646.4,
                807.8
            ]
        },
        {
            "value": [
                692.8,
                783.2,
                924.2
            ]
        }
    ],
    "stat": {
        "uniqueSource": 3,
        "uniqueDestination": 3,
        "totalCells": 9
    },
    "requestId": "matrix-time-1",
    "startTimeEpoch": 1671675366,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "matrix-time-1",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318102,
                    "longitude": -121.6959508962403
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871678,
                    "longitude": -121.69619540095405
                }
            },
            {
                "position": {
                    "latitude": 37.925198993623624,
                    "longitude": -121.77883799480549
                }
            },
            {
                "position": {
                    "latitude": 37.966075787314864,
                    "longitude": -121.78128304194283
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802993
                }
            }
        ],
        "sourcesIdx": [
            2,
            1,
            0
        ],
        "destinationsIdx": [
            5,
            4,
            3
        ],
        "asynchronous": true,
        "countryIso3": "USA"
    }
}
```


Then, we got a 3x3 time(seconds) matrix from the rows in the response.
![Time-matrix-3-3](assets/images/matrix-time-3x3.png)


## Example of All Possibilities
![Stops](assets/images/stops.png)

In this case, we want to calculate travel time among the 6 stops.

**Send Calculation Request**

```
POST {{baseURL}}/enterprise/v1/dro/time_matrix
```

**Body**
```json
{
    "requestId": "matrix-time-2",
    "points": [
        {
            "position":
            {
                "latitude": 37.996333094327554,
                "longitude": -121.70646459893086
            }
        },
        {
            "position":
            {
                "latitude": 37.96858164318102,
                "longitude": -121.6959508962403
            }
        },
        {
            "position":
            {
                "latitude": 37.8966488871678,
                "longitude": -121.69619540095405
            }
        },
        {
            "position":
            {
                "latitude": 37.925198993623624,
                "longitude": -121.77883799480549
            }
        },
        {
            "position":
            {
                "latitude": 37.966075787314864,
                "longitude": -121.78128304194283
            }
        },
        {
            "position":
            {
                "latitude": 38.011938673071406,
                "longitude": -121.80597801802993
            }
        }
    ],
    "sourcesIdx": [
    ],
    "destinationsIdx": [
    ],
    "asynchronous": true,
    "countryIso3": "USA"
}
```

**Get Calculation Result**

```
GET {{baseURL}}/enterprise/v1/dro/time_matrix/{{requestId}}
```

**Response**

```json
{
    "rows": [
        {
            "value": [
                0.0,
                229.9,
                805.8,
                924.2,
                783.2,
                692.8
            ]
        },
        {
            "value": [
                229.9,
                0.0,
                575.9,
                807.8,
                646.4,
                822.7
            ]
        },
        {
            "value": [
                806.5,
                576.6,
                0.0,
                567.9,
                804.9,
                933.1
            ]
        },
        {
            "value": [
                940.9,
                808.8,
                553.9,
                0.0,
                507.0,
                917.4
            ]
        },
        {
            "value": [
                761.4,
                609.0,
                714.4,
                450.3,
                0.0,
                489.6
            ]
        },
        {
            "value": [
                704.3,
                877.7,
                975.2,
                936.9,
                486.6,
                0.0
            ]
        }
    ],
    "stat": {
        "uniqueSource": 6,
        "uniqueDestination": 6,
        "totalCells": 36
    },
    "requestId": "matrix-time-2",
    "startTimeEpoch": 1671675857,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "matrix-time-2",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318102,
                    "longitude": -121.6959508962403
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871678,
                    "longitude": -121.69619540095405
                }
            },
            {
                "position": {
                    "latitude": 37.925198993623624,
                    "longitude": -121.77883799480549
                }
            },
            {
                "position": {
                    "latitude": 37.966075787314864,
                    "longitude": -121.78128304194283
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802993
                }
            }
        ],
        "asynchronous": true,
        "countryIso3": "USA"
    }
}
```

Then, we got a 6x6 time(seconds) matrix from the rows in the response.
![Time-matrix-6-6](assets/images/matrix-time-6x6.png)

## Example of Additional Stops
```
POST {{baseURL}}/enterprise/v1/dro/time_matrix
```

To calculate with additional stops, we will use <b>referenceRequestId</b> which is the requestId of matrix we just created.

In this example, we added the 7th stop and a referenceRequestId to the request.

**Body**
```json
{
        "requestId": "matrix-time-101",
        "referenceRequestId":"matrix-time-2",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318102,
                    "longitude": -121.6959508962403
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871678,
                    "longitude": -121.69619540095405
                }
            },
            {
                "position": {
                    "latitude": 37.925198993623624,
                    "longitude": -121.77883799480549
                }
            },
            {
                "position": {
                    "latitude": 37.966075787314864,
                    "longitude": -121.78128304194283
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802993
                }
            },
            {
                "position": {
                    "latitude": 37.98937699198773,
                    "longitude": -121.75662231471074
                }
            }
        ],
        "asynchronous": true,
        "countryIso3": "USA"
    }
```

**Get Calculation Result**

```
GET {{baseURL}}/enterprise/v1/dro/time_matrix/{{requestId}}
```

Then we can get the 7x7 matrix with the requestId "matrix-time-101"

**Response**

```json
{
    "rows": [
        {
            "value": [
                0.0,
                229.9,
                805.8,
                924.2,
                783.2,
                692.8,
                874.3
            ]
        },
        {
            "value": [
                229.9,
                0.0,
                575.9,
                807.8,
                646.4,
                822.7,
                851.6
            ]
        },
        {
            "value": [
                806.5,
                576.6,
                0.0,
                567.9,
                804.9,
                933.1,
                1010.1
            ]
        },
        {
            "value": [
                940.9,
                808.8,
                553.9,
                0.0,
                507.0,
                917.4,
                943.9
            ]
        },
        {
            "value": [
                761.4,
                609.0,
                714.4,
                450.3,
                0.0,
                489.6,
                543.4
            ]
        },
        {
            "value": [
                704.3,
                877.7,
                975.2,
                936.9,
                486.6,
                0.0,
                662.8
            ]
        },
        {
            "value": [
                876.5,
                868.5,
                973.9,
                941.6,
                561.6,
                632.6,
                0.0
            ]
        }
    ],
    "stat": {
        "uniqueSource": 7,
        "uniqueDestination": 7,
        "totalCells": 49
    },
    "requestId": "reference-matrix-time-101",
    "startTimeEpoch": 1672273068,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "reference-matrix-time-101",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318102,
                    "longitude": -121.6959508962403
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871678,
                    "longitude": -121.69619540095405
                }
            },
            {
                "position": {
                    "latitude": 37.925198993623624,
                    "longitude": -121.77883799480549
                }
            },
            {
                "position": {
                    "latitude": 37.966075787314864,
                    "longitude": -121.78128304194283
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802993
                }
            },
            {
                "position": {
                    "latitude": 37.98937699198773,
                    "longitude": -121.75662231471074
                }
            }
        ],
        "asynchronous": true,
        "countryIso3": "USA",
        "referenceRequestId": "matrix-time-2"
    }
}
```


## Request Payloads
- points - [required] The stops we want to calculate for time.
- requestId - [optional] If not specified we will generate one, it is determinsitacally based on the points, sourcesIdx, destinationsIdx.
- referenceRequestId - [optional] The requestId of created matrix.
- sources_idx - [optional] All points would be sources if it is not specified.
- destinations_idx - [optional] All points would be destinations if it is not specified.
- country_iso3 - [optional] A random Point would be used to determine its most likely country of origin if it is not specified.

## Importance
The calculation result will be available for 7 days (the result may be archived after 7 days).