
<img src="../assets/images/beans-128x128.png" align="right" />

# Distance Matrix

![Stops](assets/images/stops.png)

When you have many stops and want to determine the distances among them at once,

Distance Matrix would be helpful to you.

## Table of contents
- [Distance Matrix](#distance-matrix)
  - [Example of Specified Sources and Destinations](#example-of-specified-sources-and-destinations)
  - [Example of All Possibilities](#example-of-all-possibilities)
  - [Example of Additional stops](#example-of-additional-stops)
  - [Request Payloads](#request-payloads)
  - [Importance](#importance)

## Example of Specified Sources and Destinations
![Stops](assets/images/stops-part.png)
Let's say we have 6 stops which 3 are sources and 3 are destinations,
we will make a calculation request then get the result.

**Send Calculation Request**

```
POST {{baseURL}}/enterprise/v1/dro/distance_matrix
```

**Body**
```json
{
    "requestId": "distance-matrix-2001A",
    "points": [
        {
            "position":
            {
                "latitude": 37.996333094327555,
                "longitude": -121.70646459893087
            }
        },
        {
            "position":
            {
                "latitude": 37.96858164318103,
                "longitude": -121.6959508962404
            }
        },
        {
            "position":
            {
                "latitude": 37.8966488871679,
                "longitude": -121.69619540095406
            }
        },
        {
            "position":
            {
                "latitude": 37.925198993623625,
                "longitude": -121.77883799480548
            }
        },
        {
            "position":
            {
                "latitude": 37.966075787314863,
                "longitude": -121.78128304194284
            }
        },
        {
            "position":
            {
                "latitude": 38.011938673071405,
                "longitude": -121.80597801802994
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
GET {{baseURL}}/enterprise/v1/dro/distance_matrix/{{requestId}}
```

**Response**
```json
{
    "rows": [
        {
            "value": [
                15634.5,
                11453.8,
                10171.6
            ]
        },
        {
            "value": [
                11789.2,
                8791.8,
                13635.7
            ]
        },
        {
            "value": [
                9607.4,
                13785.9,
                19478.6
            ]
        }
    ],
    "stat": {
        "uniqueSource": 3,
        "uniqueDestination": 3,
        "totalCells": 9
    },
    "requestId": "distance-matrix-100A",
    "startTimeEpoch": 1672296284,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "distance-matrix-100A",
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
            0,
            1,
            2
        ],
        "destinationsIdx": [
            3,
            4,
            5
        ],
        "asynchronous": true,
        "countryIso3": "USA"
    }
}
```

Then, we got a 3x3 distance(meters) matrix from the rows in the response.

![Distance-matrix-3-3](assets/images/calculation-result-3-3.png)


## Example of All Possibilities
![Stops](assets/images/stops.png)

This time, we want to calculate all distances between 6 stops.

**Send Calculation Request**

```
POST {{baseURL}}/enterprise/v1/dro/distance_matrix
```

**Body**
```json
{
    "requestId": "distance-matrix-2001B",
    "points": [
        {
            "position":
            {
                "latitude": 37.996333094327555,
                "longitude": -121.70646459893087
            }
        },
        {
            "position":
            {
                "latitude": 37.96858164318103,
                "longitude": -121.6959508962404
            }
        },
        {
            "position":
            {
                "latitude": 37.8966488871679,
                "longitude": -121.69619540095406
            }
        },
        {
            "position":
            {
                "latitude": 37.925198993623625,
                "longitude": -121.77883799480548
            }
        },
        {
            "position":
            {
                "latitude": 37.966075787314863,
                "longitude": -121.78128304194284
            }
        },
        {
            "position":
            {
                "latitude": 38.011938673071405,
                "longitude": -121.80597801802994
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
GET {{baseURL}}/enterprise/v1/dro/distance_matrix/{{requestId}}
```

**Response**
```json
{
    "rows": [
        {
            "value": [
                0.0,
                3504.5,
                11752.2,
                15634.5,
                11453.8,
                10171.6
            ]
        },
        {
            "value": [
                3504.5,
                0.0,
                8247.7,
                11789.2,
                8791.8,
                13635.7
            ]
        },
        {
            "value": [
                11767.8,
                8263.2,
                0.0,
                9607.4,
                13785.9,
                19478.6
            ]
        },
        {
            "value": [
                15936.0,
                11808.5,
                9548.4,
                0.0,
                5445.9,
                11319.4
            ]
        },
        {
            "value": [
                10665.6,
                8343.9,
                12954.5,
                4974.5,
                0.0,
                6521.4
            ]
        },
        {
            "value": [
                10179.2,
                14186.8,
                19699.8,
                11453.0,
                6478.4,
                0.0
            ]
        }
    ],
    "stat": {
        "uniqueSource": 6,
        "uniqueDestination": 6,
        "totalCells": 36
    },
    "requestId": "distance-matrix-2001B",
    "startTimeEpoch": 1672296453,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "distance-matrix-2001B",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318103,
                    "longitude": -121.6959508962404
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871679,
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
                    "longitude": -121.78128304194284
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802995
                }
            }
        ],
        "asynchronous": true,
        "countryIso3": "USA"
    }
}
```

Then, we got a 6x6 distance(meters) matrix from the rows in the response.

![Distance-matrix-6-6](assets/images/calculation-result-6-6.png)


## Example of Additional Stops

To calculate with additional stops, we will use <b>referenceRequestId</b> which is the requestId of matrix we just created.

In this example, we added another 3 stops with a referenceRequestId to the request.

**Send Calculation Request**

```
POST {{baseURL}}/enterprise/v1/dro/distance_matrix
```

**Body**
```json
{
    "requestId": "distance-matrix-A2001",
    "referenceRequestId":"distance-matrix-2001B",
    "points": [
        {
            "position":
            {
                "latitude": 37.996333094327555,
                "longitude": -121.70646459893087
            }
        },
        {
            "position":
            {
                "latitude": 37.96858164318103,
                "longitude": -121.6959508962404
            }
        },
        {
            "position":
            {
                "latitude": 37.8966488871679,
                "longitude": -121.69619540095406
            }
        },
        {
            "position":
            {
                "latitude": 37.925198993623625,
                "longitude": -121.77883799480548
            }
        },
        {
            "position":
            {
                "latitude": 37.966075787314863,
                "longitude": -121.78128304194284
            }
        },
        {
            "position":
            {
                "latitude": 38.011938673071405,
                "longitude": -121.80597801802994
            }
        },
        {
            "position":
            {
                "latitude": 37.988837389014364,
                "longitude": -121.76569457567187
            }
        },
        {
            "position":
            {
                "latitude": 37.983100261654,
                "longitude": -121.75899537913271
            }
        },
        {
            "position":
            {
                "latitude": 37.98395140229323,
                "longitude": -121.75187623295975
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

Then, we will get a 9x9 matrix with the requestId "distance-matrix-A2001" with a <b>referencedCells</b> in "stat" field.

```
GET {{baseURL}}/enterprise/v1/dro/distance_matrix/{{requestId}}
```

**Response**
```json
{
    "rows": [
        {
            "value": [
                0.0,
                3504.5,
                11752.2,
                15634.5,
                11453.8,
                10171.6,
                7713.8,
                6536.6,
                7213.3
            ]
        },
        {
            "value": [
                3504.5,
                0.0,
                8247.7,
                11789.2,
                8791.8,
                13635.7,
                9789.6,
                9692.8,
                10265.0
            ]
        },
        {
            "value": [
                11767.8,
                8263.2,
                0.0,
                9607.4,
                13785.9,
                19478.6,
                14783.7,
                14686.9,
                15259.1
            ]
        },
        {
            "value": [
                15936.0,
                11808.5,
                9548.4,
                0.0,
                5445.9,
                11319.4,
                9525.5,
                9428.7,
                10000.9
            ]
        },
        {
            "value": [
                10665.6,
                8343.9,
                12954.5,
                4974.5,
                0.0,
                6521.4,
                4704.4,
                4607.6,
                5179.9
            ]
        },
        {
            "value": [
                10179.2,
                14186.8,
                19699.8,
                11453.0,
                6478.4,
                0.0,
                6820.0,
                6723.2,
                7295.5
            ]
        },
        {
            "value": [
                12219.5,
                9825.0,
                14435.6,
                9538.3,
                4891.1,
                6823.6,
                0.0,
                1199.9,
                1772.1
            ]
        },
        {
            "value": [
                6557.6,
                9745.0,
                14355.6,
                9458.3,
                4811.0,
                6743.6,
                1190.5,
                0.0,
                690.1
            ]
        },
        {
            "value": [
                7234.3,
                10317.2,
                14927.8,
                10030.5,
                5383.2,
                7315.8,
                1762.8,
                690.1,
                0.0
            ]
        }
    ],
    "stat": {
        "uniqueSource": 9,
        "uniqueDestination": 9,
        "totalCells": 81,
        "referencedCells": 36
    },
    "requestId": "distance-matrix-A2001",
    "startTimeEpoch": 1672296699,
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "request": {
        "requestId": "distance-matrix-A2001",
        "points": [
            {
                "position": {
                    "latitude": 37.996333094327554,
                    "longitude": -121.70646459893086
                }
            },
            {
                "position": {
                    "latitude": 37.96858164318103,
                    "longitude": -121.6959508962404
                }
            },
            {
                "position": {
                    "latitude": 37.8966488871679,
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
                    "longitude": -121.78128304194284
                }
            },
            {
                "position": {
                    "latitude": 38.011938673071406,
                    "longitude": -121.80597801802995
                }
            },
            {
                "position": {
                    "latitude": 37.988837389014364,
                    "longitude": -121.76569457567187
                }
            },
            {
                "position": {
                    "latitude": 37.983100261654,
                    "longitude": -121.75899537913271
                }
            },
            {
                "position": {
                    "latitude": 37.98395140229323,
                    "longitude": -121.75187623295975
                }
            }
        ],
        "asynchronous": true,
        "countryIso3": "USA",
        "referenceRequestId": "distance-matrix-2001B"
    }
}
```


# Request Payloads
- points - [required] The stops we want to calculate for distances.
- requestId - [optional] If not specified we will generate one, it is determinsitacally based on the points, sourcesIdx, destinationsIdx.
- referenceRequestId - [optional] The requestId of created matrix.
- sources_idx - [optional] All points would be sources if it is not specified.
- destinations_idx - [optional] All points would be destinations if it is not specified.
- country_iso3 - [optional] A random Point would be used to determine its most likely country of origin if it is not specified.

# Importance
The calculation result will be available for 7 days (the result may be archived after 7 days).