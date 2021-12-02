# Account Information Service (AIS)

The Account Information Service (AIS) offers the following services

  * Transaction reports for a given account or card account including balances if applicable.
  * Balances of a given account or card account,
  * A list of available accounts or card account,
  * Account details of a given account or card account or of the list of all accessible accounts or card account relative to a granted consent

## GET Accounts

`GET /accounts`

> Request

```shell--sandbox
GET /accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...  
```

```shell--production
GET /accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...   
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "accounts" : [ {
    "resourceId" : "...",
    "name" : "...",
    "product" : "...",
    "cashAccountType" : "SACC",
    "status" : "blocked",
    "bic" : "...",
    "linkedAccounts" : "...",
    "usage" : "PRIV",
    "details" : "...",
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "closingBooked",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "forwardAvailable",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    },
    "displayName" : "...",
    "ownerName" : "...",
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  }, {
    "resourceId" : "...",
    "name" : "...",
    "product" : "...",
    "cashAccountType" : "CISH",
    "status" : "blocked",
    "bic" : "...",
    "linkedAccounts" : "...",
    "usage" : "PRIV",
    "details" : "...",
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "authorised",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "forwardAvailable",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    },
    "displayName" : "...",
    "ownerName" : "...",
    "iban" : "...",
    "bban" : "...",
    "pan" : "...",
    "maskedPan" : "...",
    "msisdn" : "...",
    "currency" : "..."
  } ]
}
```

Read the identifiers of the available payment account together with booking balance information, depending on the consent granted.

It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed list of accounts depends then on the PSU ID and the stored consent addressed by consentId, respectively the OAuth2 access token.

Returns all identifiers of the accounts, to which an account access has been granted to through the /consents endpoint by the PSU. In addition, relevant information about the accounts and hyperlinks to corresponding account information resources are provided if a related consent has been already granted.

Remark: Note that the /consents endpoint optionally offers to grant an access on all available payment accounts of a PSU. In this case, this endpoint will deliver the information about all available payment accounts of the PSU at this ASPSP.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	| header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	| header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | 	regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$
| PSU-Http-Method	| header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP ddress field between PSU and TPP. |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	| header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| withBalance | query | If contained, this function reads the list of accessible payment accounts including the booking balance, if granted by the PSU in the related consent and available by the ASPSP. This parameter might be ignored by the ASPSP. | boolean |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |


**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [AccountList] (JSON) |


## GET /accounts/{account-id}

`GET /accounts/{account-id}`

> Request

```shell--sandbox
GET /accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "account" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  }
}
```

Reads details about an account, with balances where required. It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed details of this account depends then on the stored consent addressed by consentId, respectively the OAuth2 access token.

**NOTE:** The account-id can represent a multicurrency account. In this case the currency code is set to "XXX".

Give detailed information about the addressed account.

Give detailed information about the addressed account together with balance information

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID	 | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. | 
| PSU-Accept | header |	The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	| header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	| header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |
| withBalance | query | If contained, this function reads the list of accessible payment accounts including the booking balance, if granted by the PSU in the related consent and available by the ASPSP. This parameter might be ignored by the ASPSP. | boolean |

**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [AccountDetailsResponse] (JSON) |


## GET /accounts/{account-id}/balances

`GET /accounts/{account-id}/balances`


> Request

```shell--sandbox
GET /accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "balances" : [ {
    "balanceAmount" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balanceType" : "nonInvoiced",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  }, {
    "balanceAmount" : {
      "amount" : 12345.0,
      "currency" : "..."
    },
    "balanceType" : "interimBooked",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  } ],
  "account" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  }
}
```

Reads account data from a given account addressed by "account-id".

**Remark:** This account-id can be a tokenised identification due to data protection reason since the path information might be logged on intermediary servers within the ASPSP sphere. This account-id then can be retrieved by the "Get account list" call.

The account-id is constant at least throughout the lifecycle of a given consent.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id	 | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [AccountBalanceResponse] (JSON) |

## GET /accounts/{account-id}/transactions

`GET /accounts/{account-id}/transactions`

> Request

```shell--sandbox
GET /accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "account" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "transactions" : {
    "booked" : [ {
      "transactionId" : "...",
      "entryReference" : "...",
      "endToEndId" : "...",
      "mandateId" : "...",
      "checkId" : "...",
      "creditorId" : "...",
      "bookingDate" : "...",
      "valueDate" : "...",
      "transactionAmount" : { },
      "creditorName" : "Creditor Name",
      "creditorAccount" : { },
      "creditorAgent" : "...",
      "ultimateCreditor" : "Ultimate Creditor",
      "debtorName" : "Debtor Name",
      "debtorAccount" : { },
      "debtorAgent" : "...",
      "ultimateDebtor" : "Ultimate Debtor",
      "remittanceInformationUnstructured" : "Ref Number Merchant",
      "remittanceInformationUnstructuredArray" : [ "...", "..." ],
      "remittanceInformationStructured" : "...",
      "remittanceInformationStructuredArray" : [ "...", "..." ],
      "additionalInformation" : "...",
      "additionalInformationStructured" : { },
      "purposeCode" : "TAXR",
      "bankTransactionCode" : "...",
      "proprietaryBankTransactionCode" : "...",
      "balanceAfterTransaction" : { },
      "_links" : [ { }, { } ]
    }, {
      "transactionId" : "...",
      "entryReference" : "...",
      "endToEndId" : "...",
      "mandateId" : "...",
      "checkId" : "...",
      "creditorId" : "...",
      "bookingDate" : "...",
      "valueDate" : "...",
      "transactionAmount" : { },
      "creditorName" : "Creditor Name",
      "creditorAccount" : { },
      "creditorAgent" : "...",
      "ultimateCreditor" : "Ultimate Creditor",
      "debtorName" : "Debtor Name",
      "debtorAccount" : { },
      "debtorAgent" : "...",
      "ultimateDebtor" : "Ultimate Debtor",
      "remittanceInformationUnstructured" : "Ref Number Merchant",
      "remittanceInformationUnstructuredArray" : [ "...", "..." ],
      "remittanceInformationStructured" : "...",
      "remittanceInformationStructuredArray" : [ "...", "..." ],
      "additionalInformation" : "...",
      "additionalInformationStructured" : { },
      "purposeCode" : "LCOL",
      "bankTransactionCode" : "...",
      "proprietaryBankTransactionCode" : "...",
      "balanceAfterTransaction" : { },
      "_links" : [ { }, { } ]
    } ],
    "pending" : [ {
      "transactionId" : "...",
      "entryReference" : "...",
      "endToEndId" : "...",
      "mandateId" : "...",
      "checkId" : "...",
      "creditorId" : "...",
      "bookingDate" : "...",
      "valueDate" : "...",
      "transactionAmount" : { },
      "creditorName" : "Creditor Name",
      "creditorAccount" : { },
      "creditorAgent" : "...",
      "ultimateCreditor" : "Ultimate Creditor",
      "debtorName" : "Debtor Name",
      "debtorAccount" : { },
      "debtorAgent" : "...",
      "ultimateDebtor" : "Ultimate Debtor",
      "remittanceInformationUnstructured" : "Ref Number Merchant",
      "remittanceInformationUnstructuredArray" : [ "...", "..." ],
      "remittanceInformationStructured" : "...",
      "remittanceInformationStructuredArray" : [ "...", "..." ],
      "additionalInformation" : "...",
      "additionalInformationStructured" : { },
      "purposeCode" : "SLPI",
      "bankTransactionCode" : "...",
      "proprietaryBankTransactionCode" : "...",
      "balanceAfterTransaction" : { },
      "_links" : [ { }, { } ]
    }, {
      "transactionId" : "...",
      "entryReference" : "...",
      "endToEndId" : "...",
      "mandateId" : "...",
      "checkId" : "...",
      "creditorId" : "...",
      "bookingDate" : "...",
      "valueDate" : "...",
      "transactionAmount" : { },
      "creditorName" : "Creditor Name",
      "creditorAccount" : { },
      "creditorAgent" : "...",
      "ultimateCreditor" : "Ultimate Creditor",
      "debtorName" : "Debtor Name",
      "debtorAccount" : { },
      "debtorAgent" : "...",
      "ultimateDebtor" : "Ultimate Debtor",
      "remittanceInformationUnstructured" : "Ref Number Merchant",
      "remittanceInformationUnstructuredArray" : [ "...", "..." ],
      "remittanceInformationStructured" : "...",
      "remittanceInformationStructuredArray" : [ "...", "..." ],
      "additionalInformation" : "...",
      "additionalInformationStructured" : { },
      "purposeCode" : "ELEC",
      "bankTransactionCode" : "...",
      "proprietaryBankTransactionCode" : "...",
      "balanceAfterTransaction" : { },
      "_links" : [ { }, { } ]
    } ],
    "_links" : {
      "account" : { },
      "first" : { },
      "next" : { },
      "previous" : { },
      "last" : { }
    }
  },
  "balances" : [ {
    "balanceAmount" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balanceType" : "expected",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  }, {
    "balanceAmount" : {
      "amount" : 12345.0,
      "currency" : "..."
    },
    "balanceType" : "expected",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  } ],
  "_links" : [ {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  }, {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  } ]
}
```

Read transaction reports or transaction lists of a given account dressed by "account-id", depending on the steering parameter "bookingStatus" together with balances.

For a given account, additional parameters are e.g. the attributes "dateFrom" and "dateTo". The ASPSP might add balance information, if transaction lists without balances are not supported.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Accept | header | The TPP can indicate the formats of account reports supported together with a priorisation following the HTTP header definition. The formats supported by this specification are
  * xml
  * JSON
  * text
Remark: Content types might be extended in the next version of the specification. This shall enable the TPP to address different camt.05x versions or different MT94x versions in a corporate context. The TPP then could e.g. say: "I prefer MT942, but take MT940 if MT942 is not available." |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id	 | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |
| bookingStatus | query | Permitted codes are "booked", "pending", "both" and "information".

"booked" shall be supported by the ASPSP.

To support the "pending" and "both" feature is optional for the ASPSP, Error code if not supported in the online banking frontend. If supported, "both" means to request transaction reports of transaction of bookingStatus either "pending" or "booked".

To support the "information" feature is optional for the ASPSP. Currently the booking status "information" only covers standing orders. Error code if not supported. | required
| dateFrom | query | Conditional: Starting date (inclusive the date dateFrom) of the transaction list, mandated if no delta access is required.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. |
| dateTo | query | End date (inclusive the data dateTo) of the transaction list, default is "now" if not given.

Might be ignored if a delta function is used.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. |
| deltaList | query | This data attribute is indicating that the AISP is in favor to get all transactions after the last report access for this PSU on the addressed account. This is another implementation of a delta access-report. This delta indicator might be rejected by the ASPSP if this function is not supported. Optional if supported by API provider. | boolean |
| entryReferenceFrom | query | This data attribute is indicating that the AISP is in favor to get all transactions after the transaction with identification entryReferenceFrom alternatively to the above defined period. This is a implementation of a delta access. If this data element is contained, the entries "dateFrom" and "dateTo" might be ignored by the ASPSP if a delta report is supported.

Optional if supported by API provider. |
| withBalance | query | If contained, this function reads the list of accessible payment accounts including the booking balance, if granted by the PSU in the related consent and available by the ASPSP. This parameter might be ignored by the ASPSP. | boolean


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [AccountTransactionsResponse] (JSON) |
| application/xml | object |
| text/plain | object |

## GET /accounts/{account-id}/transactions/{transactionId}

`GET /accounts/{account-id}/transactions/{transactionId}`

> Request

```shell--sandbox
GET /accounts/{account-id}/transactions/{transactionId}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /accounts/{account-id}/transactions/{transactionId}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "transactionId" : "...",
  "entryReference" : "...",
  "endToEndId" : "...",
  "mandateId" : "...",
  "checkId" : "...",
  "creditorId" : "...",
  "bookingDate" : "...",
  "valueDate" : "...",
  "transactionAmount" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "creditorName" : "Creditor Name",
  "creditorAccount" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "creditorAgent" : "...",
  "ultimateCreditor" : "Ultimate Creditor",
  "debtorName" : "Debtor Name",
  "debtorAccount" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "debtorAgent" : "...",
  "ultimateDebtor" : "Ultimate Debtor",
  "remittanceInformationUnstructured" : "Ref Number Merchant",
  "remittanceInformationUnstructuredArray" : [ "...", "..." ],
  "remittanceInformationStructured" : "...",
  "remittanceInformationStructuredArray" : [ "...", "..." ],
  "additionalInformation" : "...",
  "additionalInformationStructured" : {
    "standingOrderDetails" : {
      "startDate" : "...",
      "frequencyCode" : "MonthlyVariable",
      "endDate" : "...",
      "executionRule" : "preceding",
      "withinAMonthFlag" : true,
      "monthsOfExecution" : [ { }, { } ],
      "multiplicator" : 12345,
      "dayOfExecution" : "13",
      "LimitAamount" : { },
      "limitAamount" : { }
    }
  },
  "purposeCode" : "IPEA",
  "bankTransactionCode" : "...",
  "proprietaryBankTransactionCode" : "...",
  "balanceAfterTransaction" : {
    "balanceAmount" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balanceType" : "interimBooked",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  },
  "_links" : [ {
    "transactionDetails" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  }, {
    "transactionDetails" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  } ]
}
```

Reads transaction details from a given transaction addressed by “transactionId” on a given account addressed by "account-id". This call is only available on transactions as reported in a JSON format

Remark: Please note that the PATH might be already given in detail by the corresponding entry of the response of the "Read Transaction List" call within the _links subfield.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id	 | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |
| transactionId | path | This identification is given by the attribute transactionId of the corresponding entry of a transaction list. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [TransactionDetails] (JSON) |

## GET /card-accounts

`GET /card-accounts`

> Request

```shell--sandbox
GET /card-accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /card-accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "cardAccounts" : [ {
    "resourceId" : "...",
    "maskedPan" : "123456xxxxxx1234",
    "currency" : "EUR",
    "ownerName" : "John Doe",
    "name" : "...",
    "displayName" : "...",
    "product" : "...",
    "status" : "deleted",
    "usage" : "ORGA",
    "details" : "...",
    "creditLimit" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "closingBooked",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "interimBooked",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    }
  }, {
    "resourceId" : "...",
    "maskedPan" : "...",
    "currency" : "...",
    "ownerName" : "...",
    "name" : "...",
    "displayName" : "...",
    "product" : "...",
    "status" : "blocked",
    "usage" : "PRIV",
    "details" : "...",
    "creditLimit" : {
      "amount" : 12345.0,
      "currency" : "..."
    },
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "forwardAvailable",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "nonInvoiced",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    }
  } ]
}
```

Reads a list of card accounts with additional information, e.g. balance information. It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed list of card accounts depends then on the PSU ID and the stored consent addressed by consentId, respectively the OAuth2 access token.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CardAccountList] (JSON) |

## GET /card-accounts/{account-id}

`GET /card-accounts/{account-id}`

> Request

```shell--sandbox
GET /card-accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /card-accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "cardAccount" : {
    "resourceId" : "...",
    "maskedPan" : "123456xxxxxx1234",
    "currency" : "EUR",
    "ownerName" : "John Doe",
    "name" : "...",
    "displayName" : "...",
    "product" : "...",
    "status" : "deleted",
    "usage" : "ORGA",
    "details" : "...",
    "creditLimit" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "openingBooked",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "expected",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    }
  }
}
```

Reads details about a card account. It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed details of this account depends then on the stored consent addressed by consentId, respectively the OAuth2 access token.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CardAccountDetailsResponse] (JSON) |

## GET /card-accounts/{account-id}/balances

`GET /card-accounts/{account-id}/balances`

> Request

```shell--sandbox
GET /card-accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /card-accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "balances" : [ {
    "balanceAmount" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balanceType" : "openingBooked",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  }, {
    "balanceAmount" : {
      "amount" : 12345.0,
      "currency" : "..."
    },
    "balanceType" : "authorised",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  } ],
  "cardAccount" : {
    "resourceId" : "...",
    "maskedPan" : "123456xxxxxx1234",
    "currency" : "EUR",
    "ownerName" : "John Doe",
    "name" : "...",
    "displayName" : "...",
    "product" : "...",
    "status" : "deleted",
    "usage" : "ORGA",
    "details" : "...",
    "creditLimit" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balances" : [ {
      "balanceAmount" : { },
      "balanceType" : "openingBooked",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    }, {
      "balanceAmount" : { },
      "balanceType" : "nonInvoiced",
      "creditLimitIncluded" : true,
      "lastChangeDateTime" : 12345,
      "referenceDate" : "...",
      "lastCommittedTransaction" : "..."
    } ],
    "_links" : {
      "balances" : { },
      "transactions" : { }
    }
  }
}
```

Reads balance data from a given card account addressed by "account-id".

Remark: This account-id can be a tokenised identification due to data protection reason since the path information might be logged on intermediary servers within the ASPSP sphere. This account-id then can be retrieved by the "Get card account list" call.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CardAccountBalanceResponse] (JSON) |

## GET /card-accounts/{account-id}/transactions

`GET /card-accounts/{account-id}/transactions`

> Request

```shell--sandbox
GET /card-accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /card-accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "cardAccount" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "cardTransactions" : {
    "booked" : [ {
      "cardTransactionId" : "...",
      "terminalId" : "...",
      "transactionDate" : "...",
      "acceptorTransactionDateTime" : "...",
      "bookingDate" : "...",
      "transactionAmount" : { },
      "currencyExchange" : [ { }, { } ],
      "originalAmount" : { },
      "markupFee" : { },
      "markupFeePercentage" : "...",
      "cardAcceptorId" : "...",
      "cardAcceptorAddress" : { },
      "cardAcceptorPhone" : "...",
      "merchantCategoryCode" : "...",
      "maskedPAN" : "123456xxxxxx1234",
      "transactionDetails" : "...",
      "invoiced" : true,
      "proprietaryBankTransactionCode" : "..."
    }, {
      "cardTransactionId" : "...",
      "terminalId" : "...",
      "transactionDate" : "...",
      "acceptorTransactionDateTime" : "...",
      "bookingDate" : "...",
      "transactionAmount" : { },
      "currencyExchange" : [ { }, { } ],
      "originalAmount" : { },
      "markupFee" : { },
      "markupFeePercentage" : "...",
      "cardAcceptorId" : "...",
      "cardAcceptorAddress" : { },
      "cardAcceptorPhone" : "...",
      "merchantCategoryCode" : "...",
      "maskedPAN" : "...",
      "transactionDetails" : "...",
      "invoiced" : true,
      "proprietaryBankTransactionCode" : "..."
    } ],
    "pending" : [ {
      "cardTransactionId" : "...",
      "terminalId" : "...",
      "transactionDate" : "...",
      "acceptorTransactionDateTime" : "...",
      "bookingDate" : "...",
      "transactionAmount" : { },
      "currencyExchange" : [ { }, { } ],
      "originalAmount" : { },
      "markupFee" : { },
      "markupFeePercentage" : "...",
      "cardAcceptorId" : "...",
      "cardAcceptorAddress" : { },
      "cardAcceptorPhone" : "...",
      "merchantCategoryCode" : "...",
      "maskedPAN" : "123456xxxxxx1234",
      "transactionDetails" : "...",
      "invoiced" : true,
      "proprietaryBankTransactionCode" : "..."
    }, {
      "cardTransactionId" : "...",
      "terminalId" : "...",
      "transactionDate" : "...",
      "acceptorTransactionDateTime" : "...",
      "bookingDate" : "...",
      "transactionAmount" : { },
      "currencyExchange" : [ { }, { } ],
      "originalAmount" : { },
      "markupFee" : { },
      "markupFeePercentage" : "...",
      "cardAcceptorId" : "...",
      "cardAcceptorAddress" : { },
      "cardAcceptorPhone" : "...",
      "merchantCategoryCode" : "...",
      "maskedPAN" : "...",
      "transactionDetails" : "...",
      "invoiced" : true,
      "proprietaryBankTransactionCode" : "..."
    } ],
    "_links" : {
      "account" : { },
      "first" : { },
      "next" : { },
      "previous" : { },
      "last" : { }
    }
  },
  "balances" : [ {
    "balanceAmount" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "balanceType" : "authorised",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  }, {
    "balanceAmount" : {
      "amount" : 12345.0,
      "currency" : "..."
    },
    "balanceType" : "openingBooked",
    "creditLimitIncluded" : true,
    "lastChangeDateTime" : 12345,
    "referenceDate" : "...",
    "lastCommittedTransaction" : "..."
  } ],
  "_links" : [ {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  }, {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  } ]
}
```

Reads account data from a given card account addressed by "account-id".

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |
| bookingStatus | query | Permitted codes are "booked", "pending", "both" and "information".

"booked" shall be supported by the ASPSP.

To support the "pending" and "both" feature is optional for the ASPSP, Error code if not supported in the online banking frontend. If supported, "both" means to request transaction reports of transaction of bookingStatus either "pending" or "booked".

To support the "information" feature is optional for the ASPSP. Currently the booking status "information" only covers standing orders. Error code if not supported. | required |
| dateFrom | query | Conditional: Starting date (inclusive the date dateFrom) of the transaction list, mandated if no delta access is required.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. |
| dateTo | query | End date (inclusive the data dateTo) of the transaction list, default is "now" if not given.

Might be ignored if a delta function is used.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. |
| deltaList | query | This data attribute is indicating that the AISP is in favor to get all transactions after the last report access for this PSU on the addressed account. This is another implementation of a delta access-report. This delta indicator might be rejected by the ASPSP if this function is not supported. Optional if supported by API provider. | boolean |
| entryReferenceFrom | query | This data attribute is indicating that the AISP is in favor to get all transactions after the transaction with identification entryReferenceFrom alternatively to the above defined period. This is a implementation of a delta access. If this data element is contained, the entries "dateFrom" and "dateTo" might be ignored by the ASPSP if a delta report is supported.

Optional if supported by API provider. |
| withBalance | query | If contained, this function reads the list of accessible payment accounts including the booking balance, if granted by the PSU in the related consent and available by the ASPSP. This parameter might be ignored by the ASPSP. | boolean |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CardAccountTransactionsResponse] (JSON) |

## POST /consents

`POST /consents`

> Request

```shell--sandbox
POST /consents
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Corporate-ID: ...
PSU-Corporate-ID-Type: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-ID: ...
PSU-ID-Type: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Brand-Logging-Information: ...
TPP-Explicit-Authorisation-Preferred: ...
TPP-Nok-Redirect-URI: ...
TPP-Notification-Content-Preferred: ...
TPP-Notification-URI: ...
TPP-Redirect-Preferred: ...
TPP-Redirect-URI: ...
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "combinedServiceIndicator" : true,
  "access" : {
    "accounts" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "balances" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "transactions" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "additionalInformation" : {
      "ownerName" : [ { }, { } ],
      "trustedBeneficiaries" : [ { }, { } ]
    },
    "availableAccounts" : "allAccountsWithOwnerName",
    "availableAccountsWithBalance" : "allAccountsWithOwnerName",
    "allPsd2" : "allAccounts",
    "restrictedTo" : [ "CACC", "ONDP" ],
    "instruments" : "both"
  },
  "recurringIndicator" : true,
  "validUntil" : "...",
  "frequencyPerDay" : 12345
}
```

```shell--production
POST /consents
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Corporate-ID: ...
PSU-Corporate-ID-Type: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-ID: ...
PSU-ID-Type: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Brand-Logging-Information: ...
TPP-Explicit-Authorisation-Preferred: ...
TPP-Nok-Redirect-URI: ...
TPP-Notification-Content-Preferred: ...
TPP-Notification-URI: ...
TPP-Redirect-Preferred: ...
TPP-Redirect-URI: ...
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "combinedServiceIndicator" : true,
  "access" : {
    "accounts" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "balances" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "transactions" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "additionalInformation" : {
      "ownerName" : [ { }, { } ],
      "trustedBeneficiaries" : [ { }, { } ]
    },
    "availableAccounts" : "allAccountsWithOwnerName",
    "availableAccountsWithBalance" : "allAccountsWithOwnerName",
    "allPsd2" : "allAccounts",
    "restrictedTo" : [ "CACC", "ONDP" ],
    "instruments" : "both"
  },
  "recurringIndicator" : true,
  "validUntil" : "...",
  "frequencyPerDay" : 12345
}
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
ASPSP-Notification-Support: ...
X-Request-ID: ...
ASPSP-SCA-Approach: ...
ASPSP-Notification-Content: ...
Location: ...

                
{
  "consentStatus" : "valid",
  "consentId" : "...",
  "scaMethods" : [ {
    "authenticationType" : "SMTP_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  }, {
    "authenticationType" : "CHIP_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "...",
    "explanation" : "..."
  } ],
  "chosenScaMethod" : {
    "authenticationType" : "PHOTO_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  },
  "_links" : {
    "scaRedirect" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "scaOAuth" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuIdentification" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updatePsuIdentification" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updatePsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithEncryptedPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "selectAuthenticationMethod" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "authoriseTransaction" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "status" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "self" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "confirmation" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  },
  "challengeData" : {
    "image" : "...",
    "data" : [ "...", "..." ],
    "imageLink" : "...",
    "otpMaxLength" : 12345,
    "otpFormat" : "integer",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

This method create a consent resource, defining access rights to dedicated accounts of a given PSU-ID. These accounts are addressed explicitly in the method as parameters as a core function.

Side Effects When this Consent Request is a request where the "recurringIndicator" equals "true", and if it exists already a former consent for recurring access on account information for the addressed PSU, then the former consent automatically expires as soon as the new consent request is authorized by the PSU.

Optional Extension: As an option, an ASPSP might optionally accept a specific access right on the access on all psd2 related services for all available accounts.

As another option an ASPSP might optionally also accept a command, where only access rights are inserted without mentioning the addressed account. The relation to accounts is then handled afterwards between PSU and ASPSP. This option is not supported for the Embedded SCA Approach. As a last option, an ASPSP might in addition accept a command with access rights

  * to see the list of available payment accounts or
  * to see the list of available payment accounts with balances.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Corporate-ID	| header | Might be mandated in the ASPSP's documentation. Only used in a corporate context. |
| PSU-Corporate-ID-Type	| header | Might be mandated in the ASPSP's documentation. Only used in a corporate context. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-ID | header | Client ID of the PSU in the ASPSP client interface. Might be mandated in the ASPSP's documentation. Is not contained if an OAuth2 based authentication was performed in a pre-step or an OAuth2 based SCA was performed in an preceeding AIS service in the same session. | required |
| PSU-ID-Type	| header | Type of the PSU-ID, needed in scenarios where PSUs have several PSU-IDs as access possibility. |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| TPP-Brand-Logging-Information	| header | This header might be used by TPPs to inform the ASPSP about the brand used by the TPP towards the PSU.
This information is meant for logging entries to enhance communication between ASPSP and PSU or ASPSP and TPP. This header might be ignored by the ASPSP. |
| TPP-Explicit-Authorisation-Preferred	| header | If it equals "true", the TPP prefers to start the authorisation process separately, e.g. because of the usage of a signing basket. This preference might be ignored by the ASPSP, if a signing basket is not supported as functionality.
If it equals "false" or if the parameter is not used, there is no preference of the TPP. This especially indicates that the TPP assumes a direct authorisation of the transaction in the next step, without using a signing basket. | boolean |
| TPP-Nok-Redirect-URI	| header | If this URI is contained, the TPP is asking to redirect the transaction flow to this address instead of the TPP-Redirect-URI in case of a negative result of the redirect SCA method. This might be ignored by the ASPSP. |
| TPP-Notification-Content-Preferred	| header | The string has the form
status=X1, ..., Xn

where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the of following semantics:

SCA: A notification on every change of the scaStatus attribute for all related authorisation processes is preferred by the TPP.

PROCESS: A notification on all changes of consentStatus or transactionStatus attributes is preferred by the TPP.

LAST: Only a notification on the last consentStatus or transactionStatus as available in the XS2A interface is preferred by the TPP.

This header field may be ignored, if the ASPSP does not support resource notification services for the related TPP. |
| TPP-Notification-URI	| header | URI for the Endpoint of the TPP-API to which the status of the payment initiation should be sent. This header field may by ignored by the ASPSP.
For security reasons, it shall be ensured that the TPP-Notification-URI as introduced above is secured by the TPP eIDAS QWAC used for identification of the TPP. The following applies:

URIs which are provided by TPPs in TPP-Notification-URI shall comply with the domain secured by the eIDAS QWAC certificate of the TPP in the field CN or SubjectAltName of the certificate. Please note that in case of example-TPP.com as certificate entry TPP- Notification-URI like www.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications or notifications.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications would be compliant.

Wildcard definitions shall be taken into account for compliance checks by the ASPSP. ASPSPs may respond with ASPSP-Notification-Support set to false, if the provided URIs do not comply. |
| TPP-Redirect-Preferred	| header | If it equals "true", the TPP prefers a redirect over an embedded SCA approach. If it equals "false", the TPP prefers not to be redirected for SCA. The ASPSP will then choose between the Embedded or the Decoupled SCA approach, depending on the choice of the SCA procedure by the TPP/PSU. If the parameter is not used, the ASPSP will choose the SCA approach to be applied depending on the SCA method chosen by the TPP/PSU. | boolean |
|TPP-Redirect-URI	| header | URI of the TPP, where the transaction flow shall be redirected to after a Redirect.
Mandated for the Redirect SCA Approach, specifically when TPP-Redirect-Preferred equals "true". It is recommended to always use this header field.

**Remark for Future:** This field might be changed to mandatory in the next version of the specification. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [ConsentCreationResult] (JSON) |

**Response Headers**

| name | description |
| ---- | ----------- |
| ASPSP-Notification-Support	| true if the ASPSP supports resource status notification services.

false if the ASPSP supports resource status notification in general, but not for the current request.

Not used, if resource status notification services are generally not supported by the ASPSP.

Shall be supported if the ASPSP supports resource status notification services. |
| X-Request-ID	| ID of the request, unique to the call, as determined by the initiating party. |
| ASPSP-SCA-Approach | Selected SCA-Approach in case if it is already fixed. |
| ASPSP-Notification-Content | The string has the form
status=X1, ..., Xn
where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated.
The usage of the constants supports the following semantics
SCA - Notification on every change of the scaStatus attribute for all related authorisation processes is provided by the ASPSP for the related resource.
PROCESS - Notification on all changes of consentStatus or transactionStatus attributes is provided by the ASPSP for the related resource
LAST - Notification on the last consentStatus or transactionStatus as available in the XS2A interface is provided by the ASPSP for the related resource.
This field must be provided if the ASPSP-Notification-Support=true. The ASPSP might consider the notification content as preferred by the TPP, but can also respond independently of the preferred request. |
| Location | Location of the created resource. |

## DELETE /consents/{consentId}

`DELETE /consents/{consentId}`

> Request

```shell--sandbox
DELETE /consents/{consentId}
Content-Type: */*
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
DELETE /consents/{consentId}
Content-Type: */*
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
```

The TPP can delete an account information consent object if needed.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

## GET /consents/{consentId}

`GET /consents/{consentId}`

> Request

```shell--sandbox
GET /consents/{consentId}
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /consents/{consentId}
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "consentStatus" : "valid",
  "lastActionDate" : "...",
  "_links" : {
    "account" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  },
  "access" : {
    "accounts" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "balances" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "transactions" : [ {
      "iban" : "DE27100777770209299700",
      "bban" : "BARC12345612345678",
      "pan" : "5409050000000000",
      "maskedPan" : "123456xxxxxx1234",
      "msisdn" : "+49 170 1234567",
      "currency" : "EUR"
    }, {
      "iban" : "...",
      "bban" : "...",
      "pan" : "...",
      "maskedPan" : "...",
      "msisdn" : "...",
      "currency" : "..."
    } ],
    "additionalInformation" : {
      "ownerName" : [ { }, { } ],
      "trustedBeneficiaries" : [ { }, { } ]
    },
    "availableAccounts" : "allAccounts",
    "availableAccountsWithBalance" : "allAccounts",
    "allPsd2" : "allAccounts",
    "restrictedTo" : [ "CHAR", "TAXE" ],
    "instruments" : "both"
  },
  "recurringIndicator" : true,
  "validUntil" : "...",
  "frequencyPerDay" : 12345
}
```

Returns the content of an account information consent object. This is returning the data for the TPP especially in cases, where the consent was directly managed between ASPSP and PSU e.g. in a re-direct SCA Approach.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [Consent] (JSON) |

## GET /consents/{consentId}/authorisations

`GET /consents/{consentId}/authorisations`

> Request

```shell--sandbox
GET /consents/{consentId}/authorisations
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /consents/{consentId}/authorisations
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "authorisationIds" : [ "...", "..." ]
}
```

Return a list of all authorisation subresources IDs which have been created. This function returns an array of hyperlinks to all generated authorisation sub-resources.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [Authorisations] (JSON) |

## POST /consents/{consentId}/authorisations

`POST /consents/{consentId}/authorisations`

> Request

```shell--sandbox
POST /consents/{consentId}/authorisations
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Nok-Redirect-URI: ...
TPP-Notification-Content-Preferred: ...
TPP-Notification-URI: ...
TPP-Redirect-Preferred: ...
TPP-Redirect-URI: ...
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "psuData" : {
    "password" : "...",
    "encryptedPassword" : "...",
    "additionalPassword" : "...",
    "additionalEncryptedPassword" : "..."
  },
  "authenticationMethodId" : "myAuthenticationID",
  "scaAuthenticationData" : "...",
  "confirmationCode" : "..."
}
```

```shell--production
POST /consents/{consentId}/authorisations
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Nok-Redirect-URI: ...
TPP-Notification-Content-Preferred: ...
TPP-Notification-URI: ...
TPP-Redirect-Preferred: ...
TPP-Redirect-URI: ...
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "psuData" : {
    "password" : "...",
    "encryptedPassword" : "...",
    "additionalPassword" : "...",
    "additionalEncryptedPassword" : "..."
  },
  "authenticationMethodId" : "myAuthenticationID",
  "scaAuthenticationData" : "...",
  "confirmationCode" : "..."
}
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "authorisationId" : "123auth456",
  "_links" : {
    "scaRedirect" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "scaOAuth" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuIdentification" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updatePsuIdentification" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updatePsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithEncryptedPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "selectAuthenticationMethod" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "authoriseTransaction" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "status" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "confirmation" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  },
  "scaStatus" : "received",
  "scaMethods" : [ {
    "authenticationType" : "SMS_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  }, {
    "authenticationType" : "PHOTO_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "...",
    "explanation" : "..."
  } ],
  "chosenScaMethod" : {
    "authenticationType" : "SMS_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  },
  "challengeData" : {
    "image" : "...",
    "data" : [ "...", "..." ],
    "imageLink" : "...",
    "otpMaxLength" : 12345,
    "otpFormat" : "integer",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

Create an authorisation sub-resource and start the authorisation process of a consent. The message might in addition transmit authentication and authorisation related data.

This method is iterated n times for a n times SCA authorisation in a corporate context, each creating an own authorisation sub-endpoint for the corresponding PSU authorising the consent.

The ASPSP might make the usage of this access method unnecessary, since the related authorisation resource will be automatically created by the ASPSP after the submission of the consent data with the first POST consents call.

The start authorisation process is a process which is needed for creating a new authorisation or cancellation sub-resource.

This applies in the following scenarios:

  * The ASPSP has indicated with an 'startAuthorisation' hyperlink in the preceding Payment Initiation Response that an explicit start of the authorisation process is needed by the TPP. The 'startAuthorisation' hyperlink can transport more information about data which needs to be uploaded by using the extended forms.
  - 'startAuthorisationWithPsuIdentfication'
  - 'startAuthorisationWithPsuAuthentication'
  - 'startAuthorisationWithEncryptedPsuAuthentication'
  - 'startAuthorisationWithAuthentciationMethodSelection'
  * The related payment initiation cannot yet be executed since a multilevel SCA is mandated.
  * The ASPSP has indicated with an 'startAuthorisation' hyperlink in the preceding Payment Cancellation Response that an explicit start of the authorisation process is needed by the TPP. The 'startAuthorisation' hyperlink can transport more information about data which needs to be uploaded by using the extended forms as indicated above.
  * The related payment cancellation request cannot be applied yet since a multilevel SCA is mandate for executing the cancellation.
  * The signing basket needs to be authorised yet.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Nok-Redirect-URI | header | If this URI is contained, the TPP is asking to redirect the transaction flow to this address instead of the TPP-Redirect-URI in case of a negative result of the redirect SCA method. This might be ignored by the ASPSP. |
| TPP-Notification-Content-Preferred	| header | The string has the form
status=X1, ..., Xn

where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the of following semantics:

SCA: A notification on every change of the scaStatus attribute for all related authorisation processes is preferred by the TPP.

PROCESS: A notification on all changes of consentStatus or transactionStatus attributes is preferred by the TPP.

LAST: Only a notification on the last consentStatus or transactionStatus as available in the XS2A interface is preferred by the TPP.

This header field may be ignored, if the ASPSP does not support resource notification services for the related TPP. |
| TPP-Notification-URI | header | URI for the Endpoint of the TPP-API to which the status of the payment initiation should be sent. This header field may by ignored by the ASPSP.
For security reasons, it shall be ensured that the TPP-Notification-URI as introduced above is secured by the TPP eIDAS QWAC used for identification of the TPP. The following applies:

URIs which are provided by TPPs in TPP-Notification-URI shall comply with the domain secured by the eIDAS QWAC certificate of the TPP in the field CN or SubjectAltName of the certificate. Please note that in case of example-TPP.com as certificate entry TPP- Notification-URI like www.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications or notifications.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications would be compliant.

Wildcard definitions shall be taken into account for compliance checks by the ASPSP. ASPSPs may respond with ASPSP-Notification-Support set to false, if the provided URIs do not comply. |
| TPP-Redirect-Preferred	| header | If it equals "true", the TPP prefers a redirect over an embedded SCA approach. If it equals "false", the TPP prefers not to be redirected for SCA. The ASPSP will then choose between the Embedded or the Decoupled SCA approach, depending on the choice of the SCA procedure by the TPP/PSU. If the parameter is not used, the ASPSP will choose the SCA approach to be applied depending on the SCA method chosen by the TPP/PSU. | boolean |
| TPP-Redirect-URI	| header | URI of the TPP, where the transaction flow shall be redirected to after a Redirect.
Mandated for the Redirect SCA Approach, specifically when TPP-Redirect-Preferred equals "true". It is recommended to always use this header field.

**Remark for Future:** This field might be changed to mandatory in the next version of the specification.
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [StartScaprocessResponse] (JSON) |

## GET /consents/{consentId}/authorisations/{authorisationId}

`GET /consents/{consentId}/authorisations/{authorisationId}`

> Request

```shell--sandbox
GET /consents/{consentId}/authorisations/{authorisationId}
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /consents/{consentId}/authorisations/{authorisationId}
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "scaStatus" : "finalised",
  "trustedBeneficiaryFlag" : true
}
```

This method returns the SCA status of a consent initiation's authorisation sub-resource. For DECOUPLED SCA approach, calling this method will check if the PSU has approved or rejected the consent and updates the consent status accordingly.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationId	| path | Resource identification of the related SCA. | required |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [ScaStatusResponse] (JSON) |

## PUT /consents/{consentId}/authorisations/{authorisationId}

`PUT /consents/{consentId}/authorisations/{authorisationId}`

> Request

```shell--sandbox
PUT /consents/{consentId}/authorisations/{authorisationId}
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-ID: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "psuData" : {
    "password" : "...",
    "encryptedPassword" : "...",
    "additionalPassword" : "...",
    "additionalEncryptedPassword" : "..."
  },
  "authenticationMethodId" : "myAuthenticationID",
  "scaAuthenticationData" : "...",
  "confirmationCode" : "..."
}
```

```shell--production
PUT /consents/{consentId}/authorisations/{authorisationId}
Content-Type: application/json
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-ID: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "psuData" : {
    "password" : "...",
    "encryptedPassword" : "...",
    "additionalPassword" : "...",
    "additionalEncryptedPassword" : "..."
  },
  "authenticationMethodId" : "myAuthenticationID",
  "scaAuthenticationData" : "...",
  "confirmationCode" : "..."
}
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "transactionFees" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "currencyConversionFees" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "estimatedTotalAmount" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "estimatedInterbankSettlementAmount" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "_links" : {
    "selectAuthenticationMethod" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "authoriseTransaction" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "scaStatus" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updateAdditionalPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "updateAdditionalEncryptedPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  },
  "scaStatus" : "received",
  "scaMethods" : [ {
    "authenticationType" : "PHOTO_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  }, {
    "authenticationType" : "SMS_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "...",
    "explanation" : "..."
  } ],
  "chosenScaMethod" : {
    "authenticationType" : "PUSH_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  },
  "challengeData" : {
    "image" : "...",
    "data" : [ "...", "..." ],
    "imageLink" : "...",
    "otpMaxLength" : 12345,
    "otpFormat" : "integer",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

This methods updates PSU data on the authorisation resource if needed. It may authorise a consent within the Embedded SCA Approach where needed.

Independently from the SCA Approach it supports e.g. the selection of the authentication method and a non-SCA PSU authentication.

There are several possible Update PSU Data requests in the context of payment initiation services needed, which depends on the SCA approach:

  * Redirect SCA Approach: A specific Update PSU Data Request is applicable for
   - the selection of authentication methods, before choosing the actual SCA approach.
  * Decoupled SCA Approach: A specific Update PSU Data Request is only applicable for
   - adding the PSU Identification, if not provided yet in the Payment Initiation Request or the Account Information Consent Request, or if no OAuth2 access token is used, or
   - the selection of authentication methods.
  * Embedded SCA Approach: The Update PSU Data Request might be used
   - to add credentials as a first factor authentication data of the PSU and
   - to select the authentication method and
   - transaction authorisation.

**Important:** The available SCA approaches are ASPSP and PSU specific and might differ from bank to bank.

The SCA Approach might depend on the chosen SCA method. For that reason, the following possible Update PSU Data request can apply to all SCA approaches:

  * Select an SCA method in case of several SCA methods are available for the customer.

There are the following request types on this access path:

*  Update PSU Identification
*  Update PSU Authentication
*  Select PSU Autorization Method WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.
*  Transaction Authorisation WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.*


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-ID | header | Client ID of the PSU in the ASPSP client interface. Might be mandated in the ASPSP's documentation. Is not contained if an OAuth2 based authentication was performed in a pre-step or an OAuth2 based SCA was performed in an preceeding AIS service in the same session. |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationId	| path | Resource identification of the related SCA. | required |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [AuthorisationUpdate] (JSON) |

## GET /consents/{consentId}/status

`GET /consents/{consentId}/status`

> Request

```shell--sandbox
GET /consents/{consentId}/status
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /consents/{consentId}/status
Content-Type: */*
Accept: application/json
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "consentStatus" : "terminatedByTpp",
  "psuMessage" : "..."
}
```

Read the status of an account information consent resource.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| consentId | path | ID of the corresponding consent object as returned by an Account Information Consent Request. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [ConsentStatusResponse] (JSON) |

## GET /custody-accounts

`GET /custody-accounts`

> Request

```shell--sandbox
GET /custody-accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /custody-accounts
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "custodyAccounts" : [ {
    "resourceId" : "...",
    "ownerName" : "John Doe",
    "name" : "...",
    "product" : "...",
    "status" : "blocked",
    "usage" : "ORGA",
    "details" : "...",
    "_links" : {
      "balances" : { },
      "transactions" : { }
    },
    "bban" : "BARC12345612345678"
  }, {
    "resourceId" : "...",
    "ownerName" : "...",
    "name" : "...",
    "product" : "...",
    "status" : "enabled",
    "usage" : "PRIV",
    "details" : "...",
    "_links" : {
      "balances" : { },
      "transactions" : { }
    },
    "bban" : "..."
  } ]
}
```

Reads a list of custody accounts with additional information, e.g. rating information. It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed list of custody accounts depends then on the PSU ID and the stored consent addressed by consentId, respectively the OAuth2 access token.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CustodyAccountList] (JSON) |

## GET /custody-accounts/{account-id}

`GET /custody-accounts/{account-id}`

> Request

```shell--sandbox
GET /custody-accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /custody-accounts/{account-id}
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "custodyAccount" : {
    "bban" : "BARC12345612345678"
  }
}
```

Reads details about a custody account. It is assumed that a consent of the PSU to this access is already given and stored on the ASPSP system. The addressed details of this account depends then on the stored consent addressed by consentId, respectively the OAuth2 access token.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CustodyAccountDetailsResponse] (JSON) |

## GET /custody-accounts/{account-id}/balances

`GET /custody-accounts/{account-id}/balances`

> Request

```shell--sandbox
GET /custody-accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /custody-accounts/{account-id}/balances
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "balances" : [ {
    "name" : "...",
    "valorCurrency" : "USD",
    "currency" : "CHF",
    "currentPrice" : 12345.0,
    "quantity" : 12345.0,
    "marketValutation" : 12345.0,
    "type" : "STRUCTURED_PRODUCTS",
    "category" : "250 - FONDS WERTPAPIERE",
    "courseDate" : "...",
    "acquirationPrice" : 12345.0,
    "averagePrice" : 12345.0,
    "winLoss" : 12345.0,
    "accuredInterest" : 12345.0,
    "multiplier" : 12345.0,
    "expireDate" : "...",
    "nsin" : "908440",
    "suffix" : "000",
    "isin" : "US0378331005"
  }, {
    "name" : "...",
    "valorCurrency" : "...",
    "currency" : "...",
    "currentPrice" : 12345.0,
    "quantity" : 12345.0,
    "marketValutation" : 12345.0,
    "type" : "STOCKS",
    "category" : "...",
    "courseDate" : "...",
    "acquirationPrice" : 12345.0,
    "averagePrice" : 12345.0,
    "winLoss" : 12345.0,
    "accuredInterest" : 12345.0,
    "multiplier" : 12345.0,
    "expireDate" : "...",
    "nsin" : "...",
    "suffix" : "...",
    "isin" : "..."
  } ],
  "custodyAccount" : {
    "bban" : "BARC12345612345678"
  }
}
```

Reads custody account positions data from a given custody account addressed by "account-id".

**Remark:** This account-id can be a tokenised identification due to data protection reason since the path information might be logged on intermediary servers within the ASPSP sphere. This account-id then can be retrieved by the "Get custody account list" call.

The account-id is constant at least throughout the lifecycle of a given consent.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CustodyAccountBalanceResponse] (JSON) |

## GET /custody-accounts/{account-id}/transactions

`GET /custody-accounts/{account-id}/transactions`

> Request

```shell--sandbox
GET /custody-accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /custody-accounts/{account-id}/transactions
Content-Type: */*
Accept: application/json
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "custodyAccount" : {
    "bban" : "BARC12345612345678"
  },
  "custodyAccountTransactions" : {
    "booked" : [ {
      "referenceId" : "...",
      "orderType" : "VCN - REDEMPTION",
      "tradingType" : "BUY",
      "name" : "Bitcoins USD",
      "quantity" : 12345.0,
      "rate" : 12345.0,
      "transactionDate" : "...",
      "courtage" : 12345.0,
      "transactionFees" : 12345.0,
      "exchange" : "...",
      "currency" : "...",
      "totalAmount" : 12345.0,
      "customerCurrency" : "...",
      "netAmountCustomerCurrency" : 12345.0,
      "nsin" : "908440",
      "suffix" : "000",
      "isin" : "US0378331005"
    }, {
      "referenceId" : "...",
      "orderType" : "...",
      "tradingType" : "SELL",
      "name" : "...",
      "quantity" : 12345.0,
      "rate" : 12345.0,
      "transactionDate" : "...",
      "courtage" : 12345.0,
      "transactionFees" : 12345.0,
      "exchange" : "...",
      "currency" : "...",
      "totalAmount" : 12345.0,
      "customerCurrency" : "...",
      "netAmountCustomerCurrency" : 12345.0,
      "nsin" : "...",
      "suffix" : "...",
      "isin" : "..."
    } ],
    "pending" : [ {
      "referenceId" : "...",
      "orderType" : "VCN - REDEMPTION",
      "tradingType" : "SELL",
      "name" : "Bitcoins USD",
      "quantity" : 12345.0,
      "rate" : 12345.0,
      "transactionDate" : "...",
      "courtage" : 12345.0,
      "transactionFees" : 12345.0,
      "exchange" : "...",
      "currency" : "...",
      "totalAmount" : 12345.0,
      "customerCurrency" : "...",
      "netAmountCustomerCurrency" : 12345.0,
      "nsin" : "908440",
      "suffix" : "000",
      "isin" : "US0378331005"
    }, {
      "referenceId" : "...",
      "orderType" : "...",
      "tradingType" : "SELL",
      "name" : "...",
      "quantity" : 12345.0,
      "rate" : 12345.0,
      "transactionDate" : "...",
      "courtage" : 12345.0,
      "transactionFees" : 12345.0,
      "exchange" : "...",
      "currency" : "...",
      "totalAmount" : 12345.0,
      "customerCurrency" : "...",
      "netAmountCustomerCurrency" : 12345.0,
      "nsin" : "...",
      "suffix" : "...",
      "isin" : "..."
    } ],
    "_links" : {
      "account" : { },
      "first" : { },
      "next" : { },
      "previous" : { },
      "last" : { }
    }
  },
  "_links" : [ {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  }, {
    "download" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  } ]
}
```

Reads account data from a given custody account addressed by "account-id".

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| account-id | path | This identification is denoting the addressed account. The account-id is retrieved by using a "Read Account List" call. The account-id is the "id" attribute of the account structure. Its value is constant at least throughout the lifecycle of a given consent. | required |
| bookingStatus | query | Permitted codes are "booked", "pending" and "both".

"booked" shall be supported by the ASPSP.

To support the "pending" and "both" feature is optional for the ASPSP, Error code if not supported in the online banking frontend. If supported, "both" means to request transaction reports of transaction of bookingStatus either "pending" or "booked". | required |
| dateFrom | query | Conditional: Starting date (inclusive the date dateFrom) of the transaction list, mandated if no delta access is required.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. | required |
| dateTo | query | End date (inclusive the data dateTo) of the transaction list, default is "now" if not given.

Might be ignored if a delta function is used.

For booked transactions, the relevant date is the booking date.

For pending transactions, the relevant date is the entry date, which may not be transparent neither in this API nor other channels of the ASPSP. |


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [CustodyAccountTransactionsResponse] (JSON) |


## GET /instruments

`GET /instruments`

> Request

```shell--sandbox
GET /instruments
Content-Type: */*
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

```shell--production
GET /instruments
Content-Type: */*
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
...
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "symbol" : "AAPL",
  "name" : "APPLE INC",
  "additionalName" : "APPLE INC",
  "currency" : "USD",
  "domicile" : "US",
  "denomination" : 12345.0,
  "type" : "CRYPTO_CURRENCIES",
  "canTrade" : true,
  "recentPrice" : {
    "dateTime" : "...",
    "price" : {
      "amount" : 5877.78,
      "currency" : "EUR"
    },
    "percentPrice" : false
  },
  "issuingDate" : "...",
  "expirationDate" : "...",
  "capitalization" : 12345.0,
  "interestRate" : 12345.0,
  "nominal" : 12345.0,
  "couponFrequency" : 12345,
  "nsin" : "908440",
  "suffix" : "000",
  "isin" : "US0378331005"
}
```

Lookup a financial instrument.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Authorization | header | This field might be used in case where a consent was agreed between ASPSP and PSU through an OAuth2 based protocol, facilitated by the TPP. |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| isin | query | The isin of the financial instrument | max size: 12, min size: 12 |
| suffix | query | In case the valoren number is not unique (e.g. securities exists for different currencies) the suffix must be given to identify the instrument correctly. Defaults to 000. | max size: 3, min size: 3 |
| valoren | query | The valoren number of the financial instrument. | max size: 12, min size: 0 |
| withRating | query | If contained, this function reads the current valutation of the financial instruments and returns it if available. | boolean


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [Instrument] (JSON) |


## POST /instruments/search

`POST /instruments/search`

> Request

```shell--sandbox
POST /instruments/search
Content-Type: application/json
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "input" : "Bitcoin",
  "type" : "CRYPTO_CURRENCIES"
}
```

```shell--production
POST /instruments/search
Content-Type: application/json
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
PSU-Accept: ...
PSU-Accept-Charset: ...
PSU-Accept-Encoding: ...
PSU-Accept-Language: ...
PSU-Device-ID: ...
PSU-Geo-Location: ...
PSU-Http-Method: ...
PSU-IP-Address: ...
PSU-IP-Port: ...
PSU-User-Agent: ...
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "input" : "Bitcoin",
  "type" : "CRYPTO_CURRENCIES"
}
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "instruments" : [ {
    "symbol" : "AAPL",
    "name" : "APPLE INC",
    "additionalName" : "APPLE INC",
    "currency" : "USD",
    "domicile" : "US",
    "denomination" : 12345.0,
    "type" : "STOCKS",
    "canTrade" : true,
    "recentPrice" : {
      "dateTime" : "...",
      "price" : { },
      "percentPrice" : false
    },
    "issuingDate" : "...",
    "expirationDate" : "...",
    "capitalization" : 12345.0,
    "interestRate" : 12345.0,
    "nominal" : 12345.0,
    "couponFrequency" : 12345,
    "nsin" : "908440",
    "suffix" : "000",
    "isin" : "US0378331005"
  }, {
    "symbol" : "...",
    "name" : "...",
    "additionalName" : "...",
    "currency" : "...",
    "domicile" : "...",
    "denomination" : 12345.0,
    "type" : "STOCKS",
    "canTrade" : true,
    "recentPrice" : {
      "dateTime" : "...",
      "price" : { },
      "percentPrice" : false
    },
    "issuingDate" : "...",
    "expirationDate" : "...",
    "capitalization" : 12345.0,
    "interestRate" : 12345.0,
    "nominal" : 12345.0,
    "couponFrequency" : 12345,
    "nsin" : "...",
    "suffix" : "...",
    "isin" : "..."
  } ]
}
```

Requires consent access to 'instruments'='searchInstruments' permission.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Authorization | header | This field might be used in case where a consent was agreed between ASPSP and PSU through an OAuth2 based protocol, facilitated by the TPP. |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. | required |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language	 | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID	 | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location	 | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method	 | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are:
  * GET
  * POST
  * PUT
  * PATCH
  * DELETE | regex: ^(GET|POST|PUT|PATCH|DELETE)$ |
| PSU-IP-Address	 | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. |
| PSU-IP-Port	 | header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent	 | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	 | header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	 | header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| withRating | query | If contained, this function reads the current valutation of the financial instruments and returns it if available. | boolean


**Response Codes**

| code | condition |
| ---- | --------- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required. |
| 201 | POST response code where Payment Initiation or Consent Request was correctly performed. |
| 202 | DELETE response code, where a payment resource can be cancelled in general, but where a cancellation authorisation is needed in addition. |
| 204 | DELETE response code where a consent resource was successfully deleted. The code indicates that the request was performed, but no content was returned. |
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [InstrumentsSearchRequest] (JSON) |