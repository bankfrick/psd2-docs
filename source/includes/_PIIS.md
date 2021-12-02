# Confirmation of Funds Service (PIIS)

Confirmation of Funds Service (PIIS) returns a confirmation of funds request at the ASPSP.


## POST /funds-confirmations

`POST /funds-confirmations`

> Request

```shell--sandbox
POST /funds-confirmations
Content-Type: application/json
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "cardNumber" : "...",
  "account" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "payee" : "...",
  "instructedAmount" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  }
} 
```

```shell--production
POST /funds-confirmations
Content-Type: application/json
Accept: application/json
Authorization: ...
Consent-ID: ...
Digest: SHA-256=hl1/Eps8BEQW58FJhDApwJXjGY4nr1ArGDHIT25vq6A=
Signature: keyId="SN=9FA1,CA=CN=D-TRUST%20CA%202-1%202015,O=D-Trust%20GmbH,C=DE",algorithm="rsa-sha256", headers="Digest X-Request-ID PSU-ID TPP-Redirect-URI Date", signature="Base64(RSA-SHA256(signing string))"
TPP-Signature-Certificate: ...
X-Request-ID: 99391c7e-ad88-49ec-a2ad-99ddcb1f7721

                
{
  "cardNumber" : "...",
  "account" : {
    "iban" : "DE27100777770209299700",
    "bban" : "BARC12345612345678",
    "pan" : "5409050000000000",
    "maskedPan" : "123456xxxxxx1234",
    "msisdn" : "+49 170 1234567",
    "currency" : "EUR"
  },
  "payee" : "...",
  "instructedAmount" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  }
}  
```

> Response

```shell
HTTP/1.1 200 OK
Content-Type: application/json

                
{
  "fundsAvailable" : true
}
```

Creates a confirmation of funds request at the ASPSP. Checks whether a specific amount is available at point of time of the request on an account linked to a given tuple card issuer(TPP)/card number, or addressed by IBAN and TPP respectively. If the related extended services are used a conditional Consent-ID is contained in the header. This field is contained but commented out in this specification.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Authorization | header | This field might be used in case where a consent was agreed between ASPSP and PSU through an OAuth2 based protocol, facilitated by the TPP. |
| Consent-ID | header | This then contains the consentId of the related AIS consent, which was performed prior to accessing this account. |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
| 400 | Validation error occurred. This code will cover malformed syntax in request or incorrect data in payload. |
| 401 | The TPP or the PSU is not correctly authorized to perform the request. Retry the request with correct authentication information. |
| 403 | Returned if the resource that was referenced in the path exists but cannot be accessed by the TPP or the PSU. This code should only be used for non-sensitive id references as it will reveal that the resource exists even though it cannot be accessed. |
| 404 | Returned if the resource or endpoint that was referenced in the path does not exist or cannot be referenced by the TPP or the PSU. When in doubt if a specific id in the path is sensitive or not, use the HTTP response code 404 instead of the HTTP response code 403. |
| 405 | This code is only sent when the HTTP method (PUT, POST, DELETE, GET etc.) is not supported on a specific endpoint. It has nothing to do with the consent, payment or account information data model. |
| 406 | The ASPSP cannot generate the content that the TPP specified in the Accept header. |
| 408 | The server is still working correctly, but an individual request has timed out. |
| 409 | Indicates that the request could not be processed because of conflict in the current state of the resource, such as an edit conflict between multiple simultaneous updates. |
| 415 | The TPP has supplied a media type which the ASPSP does not support. |
| 429 | The TPP has exceeded the number of requests allowed by the consent or by the RTS. |
| 500 | Internal server error occurred. |
| 501 | Indicates that the ASPSP does not support the requested resource. |
| 503 | The ASPSP server is currently unavailable. Generally, this is a temporary state. |


**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [FundsConfirmationResponse] (JSON) |