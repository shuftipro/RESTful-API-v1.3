# Status Codes

Shufti Pro Verification API uses conventional HTTP response codes to indicate the success or failure of an API request. Every response is generated in JSON with a specific HTTP code. 

## HTTP Codes

Following is a list of HTTP codes which are generated in responses by Shufti Pro Verification API.

HTTP code     | HTTP message         | Message        |                                   
--------------|----------------------| -------------- |
200           | OK                 | success                                    
400           | Bad Request          | bad request: one or more parameter is invalid or missing
401           | Unauthorized         | unauthorized: invalid signature key provided in the request
402           | Request Failed       | invalid request data: missing required parameters
403           | Forbidden            | forbidden: service not allowed
404           | Not Found            | resource not found
409           | Conflict             | conflicting data: already exists
500           | Server Error         | internal server error


## Events

Events are sent in responses which show the status of request. These events are sent in both HTTP and callback responses.


Event               | description     | HTTP Response | Callback Response
------------------------|-----------------|---------------|------------------
request.pending         | Request parameters are valid and verification url is generated in case of on-site verification.|Yes|Yes
request.invalid         | Request parameters provided in request are invalid.|Yes|Yes
verification.cancelled  | Request is cancelled by the user. This event occurs when end-user disagrees to terms and conditions before starting verifications.|Yes|Yes
request.timeout         | Request has timed out after a specific period of time.|No|Yes
request.unauthorized    | Request is unauthorized. The information provided in authorization header is invalid.|Yes|No
verification.accepted   | Request was valid and accepted after verification.|Yes|Yes
verification.declined   | Request was valid and declined after verification.|Yes|Yes
verification.status.changed   | Request status has been updated.|No|Yes
request.deleted   | Request has been deleted.|Yes|Yes

<aside class="notice">
  In case of off-site verification, <b>verification.accepted</b> or <b>verification.declined</b> is returned in event when request is valid after verification. In case of <b>verification.status.changed</b> a callback is sent to notify a client that the verification status has been updated.
</aside>

**Following are some sample events responses**  

> request.pending

```json
{
  "reference": "17374217",
  "event": "request.pending",
  "error": "",
  "verification_url": "https://shuftipro.com/api/verify/474f51710fb60fdf9688f44ea0345eda28a9f55212a83266fb5d237babff2"
}
```

> request.invalid

```json
{
  "reference": "17374217",
  "event": "request.invalid",
  "error": {
    "service": "document",
    "key": "dob",
    "message": "The dob does not match the format Y-m-d."
  },
  "verification_url": ""
}
```

> request.cancelled

```json
{
  "reference": "17374217",
  "event": "request.cancelled",
  "error": "",
  "verification_url": ""
}
```

> request.timeout

```json
{
  "reference": "17374217",
  "event": "request.timeout",
  "error": "",
  "verification_url": ""
}
```

> request.unauthorized

```json
{
  "reference": "",
  "event": "request.unauthorized",
  "error": {
    "service": "",
    "key": "",
    "message": "Authorization keys are missing/invalid."
  },
  "token": "",
  "verification_url": ""
}
```

> verification.accepted

```json
{
  "reference": "17374217",
  "event": "verification.accepted",
  "error": "",
  "verification_url": "",
  "verification_result": {
    "document": {
      "name": 1,
      "dob": 1,
      "expiry_date": 1,
      "issue_date": 1,
      "document_number": 1,
      "document": 1
    },
    "address": {
      "name": 1,
      "full_address": 1
    }
  },
  "verification_data": {
    "document": {
      "name": {
        "first_name": "John",
        "middle_name": "Carter",
        "last_name": "Doe"
      },
      "dob": "1978-03-13",
      "issue_date": "2015-10-10",
      "expiry_date": "2025-12-31",
      "document_number": "1456-0989-5567-0909",
      "selected_type": [
        "id_card"
      ],
      "supported_types": [
        "id_card",
        "driving_license",
        "passport"
      ]
    },
    "address": {
      "name": {
        "first_name": "John",
        "middle_name": "Carter",
        "last_name": "Doe"
      },
      "full_address": "3339 Maryland Avenue, Largo, Florida",
      "selected_type": [
        "id_card"
      ],
      "supported_types": [
        "id_card",
        "bank_statement"
      ]
    }
  }
}
```

> verification.declined

```json
{
  "reference": "95156124",
  "event": "verification.declined",
  "error": "",
  "verification_url": "",
  "verification_result": {
    "document": {
      "name": 0,
      "dob": 1,
      "expiry_date": 1,
      "issue_date": 1,
      "document_number": 1,
      "document": null
    },
    "address": {
      "name": null,
      "full_address": null
    }
  },
  "verification_data": {
    "document": {
      "name": {
        "first_name": "John",
        "middle_name": "Carter",
        "last_name": "Doe"
      },
      "dob": "1978-03-13",
      "issue_date": "2015-10-10",
      "expiry_date": "2025-12-31",
      "document_number": "1456-0989-5567-0909",
      "selected_type": [
        "id_card"
      ],
      "supported_types": [
        "id_card",
        "driving_license",
        "passport"
      ]
    },
    "address": {
      "name": {
        "first_name": "John",
        "middle_name": "Carter",
        "last_name": "Doe"
      },
      "full_address": "3339 Maryland Avenue, Largo, Florida",
      "selected_type": [
        "id_card"
      ],
      "supported_types": [
        "id_card",
        "bank_statement"
      ]
    }
  }
}
```

> verification.status.changed

```json
{
  "reference": "17374217",
  "event": "verification.status.changed"
}
```

> request.deleted

```json
{
    "reference": "17374217",
    "event": "request.deleted"
}
```