

<img src="../assets/images/beans-128x128.png" align="right" />

# Route Report


## Table of contents
- [Route Report](#route-report)
 - [Get Route Report](#get-route-report)

## Get Route Report

**Request Example**

```
GET {{baseURL}}/enterprise/v1/lists/route_reports/{{list-route-id}}
```

**Response Example**

We support reports in csv, pdf, xls file types.

```json
{
    "reports": [
        {
            "csvUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Zamboni 7e95ff31-7e95ff31-2d79-4405-82b2-3a9f8ea89c34.csv",
            "pdfUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Zamboni 7e95ff31-7e95ff31-2d79-4405-82b2-3a9f8ea89c34.pdf",
            "xlsUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Via Zamboni 7e95ff31-7e95ff31-2d79-4405-82b2-3a9f8ea89c34.xls"
        }
    ]
}
```