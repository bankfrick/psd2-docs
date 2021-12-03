# Utility

General services that indicate availability of the psd2 interface and backend services.


## GET /utility/healthcheck

`GET /utility/healthcheck`

> Request

```shell--sandbox
GET /utility/healthcheck
Content-Type: */*

                
...
```

```shell--production
GET /utility/healthcheck
Content-Type: */*

                
...
```

> Response

```shell
HTTP/1.1 204 No Content
```

Low cost service to check if the ASPSP backend services are available.


**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 204 | Indicates general availability. |
| 500 | Internal server error occurred. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |


## GET /utility/system-messages

`GET /utility/system-messages`

> Request

```shell--sandbox
GET /utility/system-messages
Content-Type: */*
Accept: application/json
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-User-Agent: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /utility/system-messages
Content-Type: */*
Accept: application/json
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-User-Agent: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "systemMessages" : [ {
    "topic" : "Maintenance Information",
    "message" : "Due to maintenance work, online banking will not be available between 05:00 to 06:00.",
    "lastChange" : "..."
  }, {
    "topic" : "...",
    "message" : "...",
    "lastChange" : "..."
  } ]
}
```

Returns general available system messages as published by the ASPSP that can be shown to the psu.

Not supported by all ASPSPs.


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[SystemMessageResponse] (JSON) |


## GET /utility/version

`GET /utility/version`

> Request

```shell--sandbox
GET /utility/version
Content-Type: */*
Accept: application/json
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /utility/version
Content-Type: */*
Accept: application/json
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "version" : "1.3.6"
}
```

Read the application version of the interface.


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| X-Request-ID | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | The version of the currently deployed psd2 interface. |
| 500 | Internal server error occurred. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[ApplicationVersionResponse] (JSON) |