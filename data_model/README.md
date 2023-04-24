

<img src="../../assets/images/beans-128x128.png" align="right" />

# Data Models

Here are the object definitions for various important data types in the ecosystem. A few common behaviors
- Fields with default value are not returned with the object. For example, if notes is empty, then, by default, the field notes would not be returned. It is safe to assume default values.
- The system accept native and camel casing as POST, and may return camel casing or native casing based on the header
- New fields may be added to support new use cases, and thus, it would be safer to ignore fields that you do not recognize

For example, default return of callback configuration is
```json
{
  "accountBuid": "e7c15b96-f782-4bea-807e-83ad0ebf8b9a",
  "route": true,
  "globalUrl": "https://callback.beans.ai/enterprise/v1/lists/_callback",
  "includeDefaultValues": true
}
```

With header **"X-Beansai-Format: native"**, the return of the same callback configuration is
```json
{
    "account_buid": "e7c15b96-f782-4bea-807e-83ad0ebf8b9a",
    "route": true,
    "global_url": "https://callback.beans.ai/enterprise/v1/lists/_callback",
    "include_default_values": true
}
```



## Table of contents
- [Route Object](#route-object)
- [List Item Object](#list-item-object)
- [Warehouse Object](#warehouse-object)

### Route Object

| Native | Camel | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **list_route_id** | listRouteId | string | The Route ID | The unique id of the route |
| **account_buid** | accountBuid | string | The account ID | The account ID that this route is in |
| **name** | name | string | "" | The name of the route |
| **date_str** | dateStr | string | "" | The date str (yyyy-mm-dd) and should be in route operator's local time zone |
| **status** | status | string | "" | One of OPEN, CLOSED  |
| **manifest_name** | manifestName | string | "" | The name of the manifest that was loaded to create this route |
| **assignee** | assignee | Assignee Object | {} | The Assignee object associated with this route |
| **warehouse** | warehouse | Warehouse Object | {} | The warehouse object associated with this route |
| **route_path_md5** | routePathMd5 | string | "" | The md5 hash of the path last computed for this route |
| **created_at** | createdAt | int64 | 0L | The timestamp, in epoch-millis, when this route is created |
| **updated_at** | updatedAt | int64 | 0L | The timestamp, in epoch-millis, when this route is last updated |
| **providers** | providers | Array of string | Empty array | 0 or more providers that are associated with this route |
| **assignee_secondarys** | assigneeSecondarys | Array of string | Empty array | A list of assignee IDs acting as secondary assignees to this route |
| **route_type** | routeType | string | "" | One of DEFAULT, SORTING_RECEIVED, TRAILER, WAREHOUSE_RECEIVED, STORAGE, OMBUDSMAN or an empty string to indicate the type of the route |
| **tags** | tags | Array of Tag | Empty Array | A list of route tags. These are route preferences |
| **start_mode** |startMode | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the start location of the route |
| **end_mode** | endMode | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the end location of the route |

### Tag object
| Native | Camel | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **key** | key | string | "" | The key of the tag |
| **value** | value | string | "" | TThe value of the tag |


### List Item Object

| Native | Camel | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **list_item_id** | listItemId | string | The item ID | The unique id of the item |
| **account_buid** | accountBuid | string | The account ID | The account ID that this item is in |
| **address** | address | string | "" | The original address for this item |
| **unit** | unit | string | "" | The original unit for this item, or secondary address line |
| **notes** | notes | string | "" | The notes associated with this item, this is free form text |
| **formatted_address** | formattedAddress | string | "" | Formatted address for this item, often is generated and cleaned during geocoding process if geocoder is enabled |
| **deliver_from_str** | deliverFromStr | string | "" | The start of the time window that this item could be done by |
| **deliver_by_str** | deliverByStr | string | "" | The end of the time window that this item should be done by |
| **tracking_id** | trackingId | string | "" | The tracking ID of the stop |
| **num_packages** | numPackages | int32 | 0 | The number of packages associated with this stop |
| **type** | type | string | Enum | One of PICKUP, DROPOFF |
| **customer_name** | customerName | string | "" | The name of the customer associated with this item |
| **customer_phone** | customerPhone | string | "" | The phone number of the customer associated with this item |
| **status** | status | string | Enum | One of NEW, IN_PROCESS, FINISHED, FAILED, MISLOAD, NOLOCATION, DELETED |
| **status_updated_at** | statusUpdatedAt | int64 | 0 | The epoch-millis when the status of the stop was updated |
| **route** | route | **Dimmunitive Route object** | {} | The Route that this stop is in. This is **dimmunitive** because only the list_route_id would be populated to non-default value if there is any association with other route values set to default. Otherwise, an empty object would be returned. |
| **route_priority** | routePriority | int32 | 0 | The ordering of ths stop in the route |
| **master_address** | masterAddress | string | "" | The leasing office address or community address, if associative |
| **parent_list_item_id** | parentListItemId | string | "" | The ID of the parent item if this list is in a group |
| **created_at** | createdAt | int64 | 0L | The timestamp, in epoch-millis, when this item is created |
| **updated_at** | updatedAt | int64 | 0L | The timestamp, in epoch-millis, when this item is last updated |
| **position** | position | LatLng | {} | Usually the navigate location of the address |
| **display_position** | displayPosition | LatLng | {} | Usually the rooftop location of the address |
| **is_external** | isExternal | boolean | false | Whether or not the geocoders are external to Beans |
| **origination** | origination | string | "NOT_SPECIFIED" | The origin of the item, set when the item is created. MANIFEST_AMEND, MANIFEST_SYNC, MANIFEST_UPLOAD, SCANNED, CALLBACK, DISPATCH, SYSTEM, NOT_SPECIFIED |
| **provider** | provider | string | "" | The provider of the item, set when the item is created |
| **signature_required** | signatureRequired | boolean | false | True when signature is required to close out the item |
| **url** | url | string | "" | Associated URL of the item |
| **source_seq** | sourceSeq | int32 | 0 | The sequence of the item, may not be correlated in a route |
| **transfer** | transfer | string | "" | Note on whether or not this item is transferred out or tranferred in |
| **placement** | placement | string | "" | Free form string, usually denote the placement of the item in a truck |
| **country_iso3** | countryIso3 | string | "" | The ISO3 country code of the address |
| **customer_email** | customerEmail | string | "" | The email of the customer associated with this item |
| **flavors** | flavors | string | "" | Comma separated associated constrains, this is used for route planning, and is used to match, exactly, to trucks that contain all the flavors. For example, if a item has flavors "a,b", then, only trucks that has both "a", and "b" flavors can be used for this item |
| **stop_time_seconds** | stopTimeSeconds | int32 | 0 | The stop time, in seconds, that this item should carry |
| **transferred_in** | transferredIn | boolean | false | True when this item was transferred in from another stop or route |
| **transferred_out** | transferredOut |  boolean | false | True when this item was transferred out into another route |
| **dimensions** | dimensions | Dimensions object | {} | This to denote constrains on various dimensions for Route planning |
| **third_party_reference_id** | thirdPartyReferenceId | string | "" | Third party reference ID for this stop |
| **third_party_status** | thirdPartyStatus | string | "" | Third party reference status for this stop |
| **secondary_status** | secondaryStatus | string | "" | Secondary status for this stop |

### Dimensions Object

| Native | Camel |  Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **dims** | dims | Array of Dimension object | [] | An Array of dimension |


### Dimension Object

| Native | Camel |  Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **t** | t | string | Enum | Type of the dimension. One of WEIGHT, VOLUME, COUNT |
| **v** | v | string | "" | respective value of the dimension. As long as the unit is aligned with the vehicle dimensions, a numeric is sufficient |


### Warehouse Object

| Native | Camel | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **list_warehouse_id** | listWarehouseId | string | The warehouse ID | The unique id of the warehouse |
| **account_buid** | accountBuid | string | The account ID | The account ID that this warehouse is in |
| **address** | address | string | "" | The address of the warehouse |
| **formatted_address** | formatted_address | string | "" | The formatted address |
| **country_iso3** | countryIso3 | string | "" | The country ISO3 code of the warehouse |
| **name** | name | string | "" | The name of the warehouse |
| **domicile** | domicile | string | "" | The domicile code of the warehouse |
| **created_at** | createdAt | int64 | 0L | The timestamp, in epoch-millis, when this warehouse is created |
| **updated_at** | updatedAt | int64 | 0L | The timestamp, in epoch-millis, when this warehouse is last updated |
| **deleted** | deleted | boolean | false | Whether or not the warehouse is deleted |
| **partner_warehouse_uuid** | partnerWarehouseUuid | string | "" | An associated warehouse reference to a partner |
| **position** | position | LatLng | {} | The Lat/Lng of the warehouse |
| **tags** | tags | Array of Tag | Empty Array | A list of warehouse tags. These are warehouse preferences |

### LatLng Object

| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **latitude** | double | 0.0 | The latitude |
| **longitude** | double | 0.0 | The longitude |


### Assignee Object

| Native | Camel | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| **list_assignee_id** | listAssigneeId | string | The assignee ID | The unique id of the assignee |
| **account_buid** | accountBuid | string | The account ID | The account ID that this assignee is in |
| **name** | name | string | "" | The name of the assignee |
| **email** | email | string | "" | The email of the assignee |
| **phone** | phone | string | "" | The phone of the assignee |
| **name** | name | string | "" | The name of the warehouse |
| **code** | code | string | "" | The short code of the assignee |
| **created_at** | createdAt | int64 | 0L | The timestamp, in epoch-millis, when this assignee is created |
| **updated_at** | updatedAt | int64 | 0L | The timestamp, in epoch-millis, when this assignee is last updated |
| **latitude** | latitude | double | 0.0 | The last known latitude of the assignee |
| **longitude** | longitude | double | 0.0 | The last known longitude of the assignee |
| **state** | state | string | "" | ACTIVE or DISABLED |
| **role** | role | string | "" | The role of the assignee, DRIVER, MANAGER, DISPATCHER, ADMIN |
| **employee_id | employeeId | string | "" | The employee id of the assignee or a reference id |
