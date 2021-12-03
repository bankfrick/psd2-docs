# Payment Initiation Service (PIS)

The Description for Payment Initiation Service (PIS) offers the following services:

  * Initiation and update of a payment request
  * Status information of a payment


## POST /{payment-service}/{payment-product}

`POST /{payment-service}/{payment-product}`

> Request

```shell--sandbox
POST /{payment-service}/{payment-product}
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

                
...
```

```shell--production
POST /{payment-service}/{payment-product}
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

                
...
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
  "transactionStatus" : "ACSC",
  "paymentId" : "...",
  "transactionFees" : {
    "amount" : 5877.78,
    "currency" : "EUR"
  },
  "currencyConversionFee" : {
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
  "transactionFeeIndicator" : true,
  "scaMethods" : [ {
    "authenticationType" : "SMS_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  }, {
    "authenticationType" : "SMTP_OTP",
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
    "otpFormat" : "characters",
    "additionalInformation" : "..."
  },
  "_links" : {
    "scaRedirect" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "scaOAuth" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisation" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuIdentification" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithEncryptedPsuAuthentication" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "startAuthorisationWithTransactionAuthorisation" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "self" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "status" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "scaStatus" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    },
    "confirmation" : {
      "href" : "/v1/payments/sepa-credit-transfers/1234-wertiq-983"
    }
  },
  "psuMessage" : "...",
  "tppMessages" : [ {
    "category" : "ERROR",
    "text" : "...",
    "path" : "...",
    "code" : { }
  }, {
    "category" : "ERROR",
    "text" : "...",
    "path" : "...",
    "code" : { }
  } ]
}
```

This method is used to initiate a payment at the ASPSP.

**Variants of Payment Initiation Requests**

This method to initiate a payment initiation at the ASPSP can be sent with either a `JSON` body or an `pain.001` body depending on the payment product in the path.

There are the following payment products:

  * Payment products with payment information in JSON format:
   - sepa-credit-transfers
   - instant-sepa-credit-transfers
   - target-2-payments
   - cross-border-credit-transfers
  * Payment products with payment information in pain.001 XML format:
   - pain.001-sepa-credit-transfers
   - pain.001-instant-sepa-credit-transfers
   - pain.001-target-2-payments
   - pain.001-cross-border-credit-transfers

Furthermore the request body depends on the payment-service

  * **payments:** A single payment initiation request.
  * **bulk-payments:** A collection of several payment iniatiation requests.
     In case of a pain.001 message there are more than one payments contained in the *pain.001 message.
     In case of a JSON there are several JSON payment blocks contained in a joining list.
  * **periodic-payments:** Create a standing order initiation resource for recurrent i.e. periodic payments addressable under {paymentId} with all data relevant for the corresponding payment product and the execution of the standing order contained in a JSON body.

This is the first step in the API to initiate the related recurring/periodic payment.

**Single and multilevel SCA Processes**

The Payment Initiation Requests are independent from the need of one ore multilevel SCA processing, i.e. independent from the number of authorisations needed for the execution of payments.

But the response messages are specific to either one SCA processing or multilevel SCA processing.

For payment initiation with multilevel SCA, this specification requires an explicit start of the authorisation, i.e. links directly associated with SCA processing like 'scaRedirect' or 'scaOAuth' cannot be contained in the response message of a Payment Initation Request for a payment, where multiple authorisations are needed. Also if any data is needed for the next action, like selecting an SCA method is not supported in the response, since all starts of the multiple authorisations are fully equal. In these cases, first an authorisation sub-resource has to be generated following the 'startAuthorisation' link.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Corporate-ID | header | Might be mandated in the ASPSP's documentation. Only used in a corporate context. |
| PSU-Corporate-ID-Type	| header | Might be mandated in the ASPSP's documentation. Only used in a corporate context. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-ID | header | Client ID of the PSU in the ASPSP client interface. Might be mandated in the ASPSP's documentation. Is not contained if an OAuth2 based authentication was performed in a pre-step or an OAuth2 based SCA was performed in an preceeding AIS service in the same session. | required |
| PSU-ID-Type	| header | Type of the PSU-ID, needed in scenarios where PSUs have several PSU-IDs as access possibility. |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Brand-Logging-Information | header | This header might be used by TPPs to inform the ASPSP about the brand used by the TPP towards the PSU. This information is meant for logging entries to enhance communication between ASPSP and PSU or ASPSP and TPP. This header might be ignored by the ASPSP. |
| TPP-Explicit-Authorisation-Preferred | header | If it equals "true", the TPP prefers to start the authorisation process separately, e.g. because of the usage of a signing basket. This preference might be ignored by the ASPSP, if a signing basket is not supported as functionality. If it equals "false" or if the parameter is not used, there is no preference of the TPP. This especially indicates that the TPP assumes a direct authorisation of the transaction in the next step, without using a signing basket. | boolean |
| TPP-Nok-Redirect-URI | header | If this URI is contained, the TPP is asking to redirect the transaction flow to this address instead of the TPP-Redirect-URI in case of a negative result of the redirect SCA method. This might be ignored by the ASPSP. |
| TPP-Notification-Content-Preferred | header | The string has the form status=X1, ..., Xn where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the of following semantics: SCA: A notification on every change of the scaStatus attribute for all related authorisation processes is preferred by the TPP. PROCESS: A notification on all changes of consentStatus or transactionStatus attributes is preferred by the TPP. LAST: Only a notification on the last consentStatus or transactionStatus as available in the XS2A interface is preferred by the TPP. This header field may be ignored, if the ASPSP does not support resource notification services for the related TPP. |
| TPP-Notification-URI | header | URI for the Endpoint of the TPP-API to which the status of the payment initiation should be sent. This header field may by ignored by the ASPSP. For security reasons, it shall be ensured that the TPP-Notification-URI as introduced above is secured by the TPP eIDAS QWAC used for identification of the TPP. The following applies: URIs which are provided by TPPs in TPP-Notification-URI shall comply with the domain secured by the eIDAS QWAC certificate of the TPP in the field CN or SubjectAltName of the certificate. Please note that in case of example-TPP.com as certificate entry TPP- Notification-URI like www.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications or notifications.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications would be compliant. Wildcard definitions shall be taken into account for compliance checks by the ASPSP. ASPSPs may respond with ASPSP-Notification-Support set to false, if the provided URIs do not comply. |
| TPP-Redirect-Preferred | header | If it equals "true", the TPP prefers a redirect over an embedded SCA approach. If it equals "false", the TPP prefers not to be redirected for SCA. The ASPSP will then choose between the Embedded or the Decoupled SCA approach, depending on the choice of the SCA procedure by the TPP/PSU. If the parameter is not used, the ASPSP will choose the SCA approach to be applied depending on the SCA method chosen by the TPP/PSU. | boolean |
| TPP-Redirect-URI | header | URI of the TPP, where the transaction flow shall be redirected to after a Redirect. Mandated for the Redirect SCA Approach, specifically when TPP-Redirect-Preferred equals "true". It is recommended to always use this header field. **Remark for Future:** This field might be changed to mandatory in the next version of the specification. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| TPP-Rejection-NoFunds-Preferred	| path | If it equals "true" then the TPP prefers a rejection of the payment initiation in case the ASPSP is providing an integrated confirmation of funds request an the result of this is that not sufficient funds are available. If it equals "false" then the TPP prefers that the ASPSP is dealing with the payment initiation like in the ASPSPs online channel, potentially waiting for a certain time period for funds to arrive to initiate the payment. This parameter might be ignored by the ASPSP. | boolean |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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

**Request Body**

| media type | data type |
| ---------- | --------- |
| application/json | string (JSON) |
| application/xml | object |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | [PaymentInitiationResponse] (JSON) |

**Response Headers**

| name | description |
| ---- | ----------- |
| ASPSP-Notification-Support | true if the ASPSP supports resource status notification services. False if the ASPSP supports resource status notification in general, but not for the current request. Not used, if resource status notification services are generally not supported by the ASPSP. Shall be supported if the ASPSP supports resource status notification services. |
| X-Request-ID | ID of the request, unique to the call, as determined by the initiating party. |
| Trading-Hours	| In case the order is made outside of the regular trading hours, this field contains information about the ASPSP trading hours. |
| ASPSP-SCA-Approach | This data element must be contained, if the SCA Approach is already fixed. Possible values are EMBEDDED, DECOUPLED, REDIRECT. The OAuth SCA approach will be subsumed by REDIRECT. |
| ASPSP-Notification-Content | The string has the form status=X1, …, Xn where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the following semantics: SCA - Notification on every change of the scaStatus attribute for all related authorisation processes is provided by the ASPSP for the related resource. PROCESS - Notification on all changes of consentStatus or transactionStatus attributes is provided by the ASPSP for the related resource. LAST: - Notification on the last consentStatus or transactionStatus as available in the XS2A interface is provided by the ASPSP for the related resource. This field must be provided if the ASPSP-Notification-Support=true. The ASPSP might consider the notification content as preferred by the TPP, but can also respond independently of the preferred request. |
| MiFID-Confirmation-Required | In case the order requires mifid confirmation, the header contains a list of customer depots that require MiFID confirmation for the order within the start authorization process. The string has the form {bban}=(RISK_CLASSIFICATION/KNOWLEDGE) comma separated for each custody account. The constants have the following semantics: RISK_CLASSIFICATION - Verification of the risk profile of the customer compared to the instrument risk of the securities. KNOWLEDGE - Verification of the product knowledge of the customer. The confirmation must be given when the marketorder is being authorised. |
| Location | Location of the created resource. |

## DELETE /{payment-service}/{payment-product}/{paymentId}

`DELETE /{payment-service}/{payment-product}/{paymentId}`

> Request

```shell--sandbox
DELETE /{payment-service}/{payment-product}/{paymentId}
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
DELETE /{payment-service}/{payment-product}/{paymentId}
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

                
...
```

This method initiates the cancellation of a payment. Depending on the payment-service, the payment-product and the ASPSP's implementation, this TPP call might be sufficient to cancel a payment. If an authorisation of the payment cancellation is mandated by the ASPSP, a corresponding hyperlink will be contained in the response message.

Cancels the addressed payment with resource identification paymentId if applicable to the payment-service, payment-product and received in product related timelines (e.g. before end of business day for scheduled payments of the last business day before the scheduled execution day).

The response to this DELETE command will tell the TPP whether the

  * access method was rejected,
  * access method was successful, or
  * access method is generally applicable, but further authorisation processes are needed.


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | object (JSON) |


## GET /{payment-service}/{payment-product}/{paymentId}

`GET /{payment-service}/{payment-product}/{paymentId}`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}
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
GET /{payment-service}/{payment-product}/{paymentId}
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

                
...
```

Returns the content of a payment object.


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | object (JSON) | Depending on the payment service and payment product, one of pain 001 xml message, one of pain 001 xml message, [PaymentInitiationWithStatusResponse], [BulkPaymentInitiationWithStatusResponse] or [PeriodicPaymentInitiationWithStatusResponse].
| application/xml | object |

## GET /{payment-service}/{payment-product}/{paymentId}/authorisations

`GET /{payment-service}/{payment-product}/{paymentId}/authorisations`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/authorisations
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
GET /{payment-service}/{payment-product}/{paymentId}/authorisations
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

Read a list of all authorisation subresources IDs which have been created. This function returns an array of hyperlinks to all generated authorisation sub-resources.


**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers` `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | 	[Authorisations] (JSON) |

## POST /{payment-service}/{payment-product}/{paymentId}/authorisations

`POST /{payment-service}/{payment-product}/{paymentId}/authorisations`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/authorisations
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
GET /{payment-service}/{payment-product}/{paymentId}/authorisations
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

Create an authorisation sub-resource and start the authorisation process. The message might in addition transmit authentication and authorisation related data.

This method is iterated n times for a n times SCA authorisation in a corporate context, each creating an own authorisation sub-endpoint for the corresponding PSU authorising the transaction.

The ASPSP might make the usage of this access method unnecessary in case of only one SCA process needed, since the related authorisation resource might be automatically created by the ASPSP after the submission of the payment data with the first POST payments/{payment-product} call.

The start authorisation process is a process which is needed for creating a new authorisation or cancellation sub-resource.

This applies in the following scenarios:

  * The ASPSP has indicated with an 'startAuthorisation' hyperlink in the preceding Payment Initiation Response that an explicit start of the authorisation process is needed by the TPP. The 'startAuthorisation' hyperlink can transport more information about data which needs to be uploaded by using the extended forms.
   - 'startAuthorisationWithPsuIdentfication',
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
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Nok-Redirect-URI | header |  If this URI is contained, the TPP is asking to redirect the transaction flow to this address instead of the TPP-Redirect-URI in case of a negative result of the redirect SCA method. This might be ignored by the ASPSP. |
| TPP-Notification-Content-Preferred | header | The string has the form status=X1, ..., Xn where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the of following semantics: SCA: A notification on every change of the scaStatus attribute for all related authorisation processes is preferred by the TPP. PROCESS: A notification on all changes of consentStatus or transactionStatus attributes is preferred by the TPP. LAST: Only a notification on the last consentStatus or transactionStatus as available in the XS2A interface is preferred by the TPP. This header field may be ignored, if the ASPSP does not support resource notification services for the related TPP. |
| TPP-Notification-URI | header | URI for the Endpoint of the TPP-API to which the status of the payment initiation should be sent. This header field may by ignored by the ASPSP. For security reasons, it shall be ensured that the TPP-Notification-URI as introduced above is secured by the TPP eIDAS QWAC used for identification of the TPP. The following applies: URIs which are provided by TPPs in TPP-Notification-URI shall comply with the domain secured by the eIDAS QWAC certificate of the TPP in the field CN or SubjectAltName of the certificate. Please note that in case of example-TPP.com as certificate entry TPP- Notification-URI like www.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications or notifications.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications would be compliant. Wildcard definitions shall be taken into account for compliance checks by the ASPSP. ASPSPs may respond with ASPSP-Notification-Support set to false, if the provided URIs do not comply. |
| TPP-Redirect-Preferred | header | If it equals "true", the TPP prefers a redirect over an embedded SCA approach. If it equals "false", the TPP prefers not to be redirected for SCA. The ASPSP will then choose between the Embedded or the Decoupled SCA approach, depending on the choice of the SCA procedure by the TPP/PSU. If the parameter is not used, the ASPSP will choose the SCA approach to be applied depending on the SCA method chosen by the TPP/PSU. | boolean |
| TPP-Redirect-URI | header | URI of the TPP, where the transaction flow shall be redirected to after a Redirect. Mandated for the Redirect SCA Approach, specifically when TPP-Redirect-Preferred equals "true". It is recommended to always use this header field. **Remark for Future:** This field might be changed to mandatory in the next version of the specification. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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


**Request Body**

| media type | data type |
| ---------- | --------- |
| application/json | 	[AuthorisationUpdate] (JSON)

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[StartScaprocessResponse] (JSON) |

**Response Headers**

| name | description |
| ---- | ----------- |
| X-Request-ID | ID of the request, unique to the call, as determined by the initiating party. |
| ASPSP-SCA-Approach | This data element must be contained, if the SCA Approach is already fixed. Possible values are EMBEDDED, DECOUPLED, REDIRECT. The OAuth SCA approach will be subsumed by REDIRECT. |

## GET /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}

`GET /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}
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
GET /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}
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
  "scaStatus" : "received",
  "trustedBeneficiaryFlag" : true
}
```

This method returns the SCA status of a payment initiation's authorisation sub-resource.

For DECOUPLED SCA approach, calling this method will check if the PSU has approved or rejected the transaction and updates the status accordingly.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationID | path | Resource identification of the related SCA. | required |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | 	[ScaStatusResponse] (JSON) |


## PUT /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}

`PUT /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}`

> Request

```shell--sandbox
PUT /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}
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
PUT /{payment-service}/{payment-product}/{paymentId}/authorisations/{authorisationId}
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
  "scaStatus" : "psuAuthenticated",
  "scaMethods" : [ {
    "authenticationType" : "SMS_OTP",
    "authenticationVersion" : "...",
    "authenticationMethodId" : "...",
    "name" : "SMS OTP on phone +49160 xxxxx 28",
    "explanation" : "..."
  }, {
    "authenticationType" : "SMTP_OTP",
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
  "challengeData" : {
    "image" : "...",
    "data" : [ "...", "..." ],
    "imageLink" : "...",
    "otpMaxLength" : 12345,
    "otpFormat" : "characters",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

This methods updates PSU data on the authorisation resource if needed. It may authorise a payment within the Embedded SCA Approach where needed.

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

  * Update PSU Identification
  * Update PSU Authentication
  * Select PSU Autorization Method WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.
  * Transaction Authorisation WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-ID | header | Client ID of the PSU in the ASPSP client interface. Might be mandated in the ASPSP's documentation. Is not contained if an OAuth2 based authentication was performed in a pre-step or an OAuth2 based SCA was performed in an preceeding AIS service in the same session. |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationID | path | Resource identification of the related SCA. | required |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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

**Request Body**

| media type | data type |
| ---------- | --------- |
| application/json | 	[AuthorisationUpdate] (JSON) |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[UpdatePsuDataResponse] (JSON) |

## GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations

`GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations
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
GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations
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

Retrieve a list of all created cancellation authorisation sub-resources.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`, `pain.001-instant-sepa-credit-transfers`, `pain.001-target-2-payments`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | 	[Authorisations] (JSON) |


## POST /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations

`POST /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations`

> Request

```shell--sandbox
POST /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations
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
POST /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations
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
X-Request-ID: ...
ASPSP-SCA-Approach: ...

                
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
  "scaStatus" : "exempted",
  "scaMethods" : [ {
    "authenticationType" : "SMS_OTP",
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
    "authenticationType" : "SMTP_OTP",
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
    "otpFormat" : "characters",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

Create an authorisation sub-resource and start the authorisation process. The message might in addition transmit authentication and authorisation related data.

This method is iterated n times for a n times SCA authorisation in a corporate context, each creating an own authorisation sub-endpoint for the corresponding PSU authorising the transaction.

The ASPSP might make the usage of this access method unnecessary in case of only one SCA process needed, since the related authorisation resource might be automatically created by the ASPSP after the submission of the payment data with the first POST payments/{payment-product} call.

The start authorisation process is a process which is needed for creating a new authorisation or cancellation sub-resource.

This applies in the following scenarios:

  * The ASPSP has indicated with an 'startAuthorisation' hyperlink in the preceding Payment Initiation Response that an explicit start of the authorisation process is needed by the TPP. The 'startAuthorisation' hyperlink can transport more information about data which needs to be uploaded by using the extended forms.
   - 'startAuthorisationWithPsuIdentfication',
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
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Nok-Redirect-URI | header |  If this URI is contained, the TPP is asking to redirect the transaction flow to this address instead of the TPP-Redirect-URI in case of a negative result of the redirect SCA method. This might be ignored by the ASPSP. |
| TPP-Notification-Content-Preferred | header | The string has the form status=X1, ..., Xn where Xi is one of the constants SCA, PROCESS, LAST and where constants are not repeated. The usage of the constants supports the of following semantics: SCA: A notification on every change of the scaStatus attribute for all related authorisation processes is preferred by the TPP. PROCESS: A notification on all changes of consentStatus or transactionStatus attributes is preferred by the TPP. LAST: Only a notification on the last consentStatus or transactionStatus as available in the XS2A interface is preferred by the TPP. This header field may be ignored, if the ASPSP does not support resource notification services for the related TPP. |
| TPP-Notification-URI | header | URI for the Endpoint of the TPP-API to which the status of the payment initiation should be sent. This header field may by ignored by the ASPSP. For security reasons, it shall be ensured that the TPP-Notification-URI as introduced above is secured by the TPP eIDAS QWAC used for identification of the TPP. The following applies: URIs which are provided by TPPs in TPP-Notification-URI shall comply with the domain secured by the eIDAS QWAC certificate of the TPP in the field CN or SubjectAltName of the certificate. Please note that in case of example-TPP.com as certificate entry TPP- Notification-URI like www.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications or notifications.example-TPP.com/xs2a-client/v1/ASPSPidentifcation/mytransaction- id/notifications would be compliant. Wildcard definitions shall be taken into account for compliance checks by the ASPSP. ASPSPs may respond with ASPSP-Notification-Support set to false, if the provided URIs do not comply. |
| TPP-Redirect-Preferred | header | If it equals "true", the TPP prefers a redirect over an embedded SCA approach. If it equals "false", the TPP prefers not to be redirected for SCA. The ASPSP will then choose between the Embedded or the Decoupled SCA approach, depending on the choice of the SCA procedure by the TPP/PSU. If the parameter is not used, the ASPSP will choose the SCA approach to be applied depending on the SCA method chosen by the TPP/PSU. | boolean |
| TPP-Redirect-URI | header | URI of the TPP, where the transaction flow shall be redirected to after a Redirect. Mandated for the Redirect SCA Approach, specifically when TPP-Redirect-Preferred equals "true". It is recommended to always use this header field. Remark for Future: This field might be changed to mandatory in the next version of the specification. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`. `pain.001-instant-sepa-credit-transfers`. `pain.001-target-2-payment`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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


**Request Body**

| media type | data type |
| ---------- | --------- |
| application/json | 	[AuthorisationUpdate] (JSON)

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[StartScaprocessResponse] (JSON) |

**Response Headers**

| name | description |
| ---- | ----------- |
| X-Request-ID | ID of the request, unique to the call, as determined by the initiating party. |
| ASPSP-SCA-Approach | This data element must be contained, if the SCA Approach is already fixed. Possible values are EMBEDDED, DECOUPLED, REDIRECT. The OAuth SCA approach will be subsumed by REDIRECT. |

## GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}

`GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}
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
GET /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}
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
  "scaStatus" : "received",
  "trustedBeneficiaryFlag" : true
}
```

This method returns the SCA status of a payment initiation's authorisation sub-resource.

For DECOUPLED SCA approach, calling this method will check if the PSU has approved or rejected the transaction and updates the status accordingly.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationId | path | Resource identification of the related SCA. | required |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`. `pain.001-instant-sepa-credit-transfers`. `pain.001-target-2-payment`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | 	[ScaStatusResponse] (JSON) |

## PUT /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}

`PUT /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}`

> Request

```shell--sandbox
PUT /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}
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
PUT /{payment-service}/{payment-product}/{paymentId}/cancellation-authorisations/{authorisationId}
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
  "scaStatus" : "psuIdentified",
  "scaMethods" : [ {
    "authenticationType" : "SMTP_OTP",
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
    "authenticationType" : "PHOTO_OTP",
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
    "otpFormat" : "characters",
    "additionalInformation" : "..."
  },
  "psuMessage" : "..."
}
```

This method updates PSU data on the cancellation authorisation resource if needed. It may authorise a cancellation of the payment within the Embedded SCA Approach where needed.

Independently from the SCA Approach it supports e.g. the selection of the authentication method and a non-SCA PSU authentication.

This methods updates PSU data on the cancellation authorisation resource if needed.

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

  * Update PSU Identification
  * Update PSU Authentication
  * Select PSU Autorization Method WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.
  * Transaction Authorisation WARNING: This method need a reduced header, therefore many optional elements are not present. Maybe in a later version the access path will change.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-ID | header | Client ID of the PSU in the ASPSP client interface. Might be mandated in the ASPSP's documentation. Is not contained if an OAuth2 based authentication was performed in a pre-step or an OAuth2 based SCA was performed in an preceeding AIS service in the same session. |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| authorisationID | path | Resource identification of the related SCA. | required |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`. `pain.001-instant-sepa-credit-transfers`. `pain.001-target-2-payment`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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

**Request Body**

| media type | data type |
| ---------- | --------- |
| application/json | 	[AuthorisationUpdate] (JSON) |

**Response Body**

| media type | data type | description |
| ---------- | --------- | ----------- |
| application/json | 	[UpdatePsuDataResponse] (JSON) |

## GET /{payment-service}/{payment-product}/{paymentId}/status

`GET /{payment-service}/{payment-product}/{paymentId}/status`

> Request

```shell--sandbox
GET /{payment-service}/{payment-product}/{paymentId}/status
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
GET /{payment-service}/{payment-product}/{paymentId}/status
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

                
...
```

Check the transaction status of a payment initiation.

**Request Parameters**

| name | type | description | constraints |
| ---- | ---- | ----------- | ----------- |
| Accept | header | The TPP can indicate the formats of status reports supported together with a prioritisation following the HTTP header definition. The formats supported by this specification are `xml` and `JSON`. If only one format is supported by the TPP, which is not supported by the ASPSP this can lead to a rejection of the request. |
| Digest | header | Is contained if and only if the "Signature" element is contained in the header of the request. |
| PSU-Accept | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Charset | header	| The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Encoding | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Accept-Language | header | The forwarded IP Accept header fields consist of the corresponding HTTP request Accept header fields between PSU and TPP, if available. |
| PSU-Device-ID | header | UUID (Universally Unique Identifier) for a device, which is used by the PSU, if available. UUID identifies either a device or a device dependant application installation. In case of an installation identification this ID need to be unaltered until removal from device. | regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| PSU-Geo-Location | header | The forwarded Geo Location of the corresponding http request between PSU and TPP if available. | regex: ^GEO:([-+]?)([\d]{1,2})(((\.)(\d+)(,)))(\s*)(([-+]?)([\d]{1,3})((\.)(\d+))?)$ |
| PSU-Http-Method | header | HTTP method used at the PSU ? TPP interface, if available. Valid values are: GET, POST, PUT, PATCH, DELETE | regex: ^(GET/POST/PUT/PATCH/DELETE)$ |
| PSU-IP-Address | header | The forwarded IP Address header field consists of the corresponding http request IP Address field between PSU and TPP. If not available, the TPP shall use the IP Address used by the TPP when submitting this request. | required |
| PSU-IP-Port	| header | The forwarded IP Port header field consists of the corresponding HTTP request IP Port field between PSU and TPP, if available. |
| PSU-User-Agent | header | The forwarded Agent header field of the HTTP request between PSU and TPP, if available. |
| Signature | header | A signature of the request by the TPP on application level. This might be mandated by ASPSP. |
| TPP-Signature-Certificate	| header | The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained. |
| X-Request-ID	| header | ID of the request, unique to the call, as determined by the initiating party. | required, regex: ^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$ |
| payment-product | path | The addressed payment product endpoint, e.g. for SEPA Credit Transfers (SCT). The ASPSP will publish which of the payment products/endpoints will be supported. Possible values are depending on the support of the ASPSP: `sepa-credit-transfers`, `instant-sepa-credit-transfers`, `target-2-payments`, `cross-border-credit-transfers`, `pain.001-sepa-credit-transfers`. `pain.001-instant-sepa-credit-transfers`. `pain.001-target-2-payment`, `pain.001-cross-border-credit-transfers` **Remark:** For all SEPA Credit Transfer based endpoints which accept XML encoding, the XML pain.001 schemes provided by EPC are supported by the ASPSP as a minimum for the body content. Further XML schemes might be supported by some communities. **Remark:** For cross-border and TARGET-2 payments only community wide pain.001 schemes do exist. There are plenty of country specific scheme variants. |
| payment-service | path | Payment Service Possible values are depending on the support of the ASPSP: `payments`, `bulk-payments`, `periodic-payments` |
| paymentId | path | Resource identification of the generated payment initiation resource. | required |

**Response Codes**

| code | condition | type |
| ---- | --------- | ---- |
| 200 | PUT, GET Response Codes. This return code is permitted if a request was repeated due to a time-out. The response in that might be either a 200 or 201 code depending on the ASPSP implementation. The POST for a Funds request will also return 200 since it does not create a new resource. DELETE Response Code where a payment resource has been cancelled successfully and no further cancellation authorisation is required.
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
| application/json | 	object (JSON) |
| application/xml | object |