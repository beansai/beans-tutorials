

<img src="../assets/images/beans-128x128.png" align="right" />

# Timesheet Report


## Table of contents
- [Timesheet Report](#timesheet-report)
 - [Get Timesheet Report](#get-timesheet-report)

## Get Timesheet Report

**Request Example**

```
GET {{baseURL}}/enterprise/v1/timesheets/report/{{list-assignee-Ids}}?date_from={{date-from}}}&date_to={{date-to}}&auto_adjust=false
```
- list-assignee-Ids [array, required] 
  - You may get reports for several assignees at once by given a set of list-assignee-id separated by comma ","
  - e.g. "assignee-id-1,assignee-id-2,assignee-id-3"
- from_date [Date String, required] - in yyyy-MM-dd format (e.g. 2023-01-01)
- to_date [Date String, required] - in yyyy-MM-dd format (e.g. 2023-02-01)
- auto_adjust [boolean, optional] 
  - Auto adjust time based on default route length when start time or end time is empty
  - The time will display "ERR" if start_time/end_time is empty and auto_adjust is set to false.
  - default is set to false


**Response Example**

We support reports in csv, pdf, xls types.

```json
{
    "csvUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Timecard 2022-06-01 to 2022-12-31 - 90a68.csv",
    "pdfUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Timecard 2022-06-01 to 2022-12-31 - 90a68.pdf",
    "xlsUrl": "https://storage.googleapis.com/beans-lists-reports/testing/Timecard 2022-06-01 to 2022-12-31 - 90a68.xls",
    "url": [
        {
            "type": "STD",
            "url": "https://storage.googleapis.com/beans-lists-reports/testing/Timecard 2022-06-01 to 2022-12-31 - 90a68-stdformat.csv"
        }
    ]
}
```

### Reports Object

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **csvUrl** | String | "" | Url of the report in csv style |
| **pdfUrl** | String | "" | Url of the report in pdf style |
| **xlsUrl** | String | "" | Url of the report in xls style |
| **url** | Array of url object | empty array | Additional report types |

### Url object
| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **type** | String | "" | Type of Report |
| **url** | String | "" | URL of the report |



