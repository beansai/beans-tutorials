

<img src="../assets/images/beans-128x128.png" align="right" />

# Routes Report


## Table of contents
- [Routes Report](#routes-report)
 - [Get Routes Report](#get-routes-report)

## Get Routes Report

**Request Example**

```
{{baseURL}}/enterprise/v1/lists/items/do/report?date_from={{from-date}}&date_to={{to-date}}
```

Query Parameter
- from_date [Date String, required] - in yyyy-MM-dd format (e.g. 2023-01-01)
- to_date [Date String, required] - in yyyy-MM-dd format (e.g. 2023-02-01)
- route_name [String, optional]
- address [String, optional]
- package_number [String, optional]
- assignee_name [String, optional]

Body Payload

- route [array, optional] - Could be used for multiple routes search

```json
{
    "route": [
        {
            "list_route_id": "e4630dbb-44f9-447c-8c5d-ba7482e0a6b82-k1"
        },
        {
            "list_route_id": "ecdd0458-7e63-44ad-b26d-b89fded637a2-k1"
        }
    ]
}
```


**Response Example**

We support reports in csv, pdf, xls file types.

```json
{
    "reports": [
        {
            "csvUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Spina e4630dbb-e4630dbb-44f9-447c-8c5d-ba0aee0a6b82.csv",
            "pdfUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Spina e4630dbb-e4630dbb-44f9-447c-8c5d-ba0aee0a6b82.pdf",
            "xlsUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Spina e4630dbb-e4630dbb-44f9-447c-8c5d-ba0aee0a6b82.xls"
        }
    ]
}
```