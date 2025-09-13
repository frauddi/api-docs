---
title: Frauddi API Reference
language_tabs:
  - shell: cURL
  - javascript: JavaScript  
  - python: Python
toc_footers:
  - <a href='https://frauddi.com'>Back to Frauddi</a>
  - <a href='mailto:elio@frauddi.com'>Support</a>
includes:
  - errors
search: true
code_clipboard: true
logo: logo.png
meta:
  - name: description
    content: Official API documentation for Frauddi
---

# Frauddi API

Welcome to the **Frauddi API**! Our API allows you to integrate advanced fraud detection and prevention capabilities into your applications.

We provide endpoints for fraud assessments, rule management, and comprehensive analytics to help protect your business from fraudulent activities.

Base URL: `https://api.frauddi.com`

## Authentication

> To authorize, use this code:

```shell
curl "https://api.frauddi.com/api/v0/endpoint" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

```javascript
const response = await fetch('https://api.frauddi.com/api/v0/endpoint', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    // request data
  })
});
const data = await response.json();
```

```python
import requests

headers = {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
}

data = {
    # request data
}

response = requests.post(
    'https://api.frauddi.com/api/v0/endpoint',
    headers=headers,
    json=data
)
result = response.json()
```

Frauddi uses API keys to authenticate requests. You can generate API keys from your Frauddi dashboard.

The API expects your key to be included in all requests in the Authorization header:

`Authorization: Bearer YOUR_API_KEY`

<aside class="notice">
Make sure to replace <code>YOUR_API_KEY</code> with your actual API key.
</aside>


<h1 id="fastapi">Frauddi API v1.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

# Authentication

- HTTP Authentication, scheme: bearer 

<h1 id="fastapi-default">Default</h1>

## Main

<a id="opIdmain__get"></a>

`GET /`

Main endpoint for the application.

> Example responses

> 200 Response

```json
{}
```

<h3 id="main-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|

<h3 id="main-responseschema">Response Schema</h3>

Status Code **200**

*Response Main  Get*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Pong

<a id="opIdpong_ping_get"></a>

`GET /ping`

Ping/Pong endpoint for the application.

> Example responses

> 200 Response

```json
{}
```

<h3 id="pong-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|

<h3 id="pong-responseschema">Response Schema</h3>

Status Code **200**

*Response Pong Ping Get*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="fastapi-assessments">assessments</h1>

## Assessment Charge

<a id="opIdassessment_charge_api_v0_assessments_charges_post"></a>

`POST /api/v0/assessments/charges`

Assessment charges.

> Body parameter

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}
```

<h3 id="assessment-charge-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="assessment-charge-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment charges|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="assessment-charge-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assessment Email

<a id="opIdassessment_email_api_v0_assessments_emails_post"></a>

`POST /api/v0/assessments/emails`

Assessment emails.

> Body parameter

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}
```

<h3 id="assessment-email-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="assessment-email-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment email|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="assessment-email-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assessment Rule

<a id="opIdassessment_rule_api_v0_assessments_rules_post"></a>

`POST /api/v0/assessments/rules`

Assessment rules.

> Body parameter

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}
```

<h3 id="assessment-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="assessment-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment rules|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="assessment-rule-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assessment Blacklist

<a id="opIdassessment_blacklist_api_v0_assessments_blacklists_post"></a>

`POST /api/v0/assessments/blacklists`

Assessment blacklists.

> Body parameter

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}
```

<h3 id="assessment-blacklist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="assessment-blacklist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment blacklists|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="assessment-blacklist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assessment Whitelist

<a id="opIdassessment_whitelist_api_v0_assessments_whitelists_post"></a>

`POST /api/v0/assessments/whitelists`

Assessment whitelists.

> Body parameter

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}
```

<h3 id="assessment-whitelist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="assessment-whitelist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment whitelists|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="assessment-whitelist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Assessment

<a id="opIdget_assessment_api_v0_assessments__assessment_id__get"></a>

`GET /api/v0/assessments/{assessment_id}`

Get an assessment by id.

<h3 id="get-assessment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|assessment_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-assessment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get assessment by id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-assessment-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Assessments By Type

<a id="opIdget_assessments_by_type_api_v0_assessments_type__assessment_type__get"></a>

`GET /api/v0/assessments/type/{assessment_type}`

Get assessments by type with pagination.

<h3 id="get-assessments-by-type-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|assessment_type|path|string|true|none|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-assessments-by-type-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get assessments by type|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-assessments-by-type-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-rules">rules</h1>

## Add Rule

<a id="opIdadd_rule_api_v0_rules__post"></a>

`POST /api/v0/rules/`

Add a rule based.

> Body parameter

```json
{
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="add-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RuleRequest](#schemarulerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="add-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Add a rule|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="add-rule-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Rules

<a id="opIdlist_rules_api_v0_rules__get"></a>

`GET /api/v0/rules/`

Fetch all rules based on the provided page and size.

<h3 id="list-rules-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-rules-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List rules|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-rules-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Rule

<a id="opIdupdate_rule_api_v0_rules__rule_id__put"></a>

`PUT /api/v0/rules/{rule_id}`

Update a rule.

> Body parameter

```json
{
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="update-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|
|body|body|[RuleRequest](#schemarulerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update a rule|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-rule-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Rule

<a id="opIddelete_rule_api_v0_rules__rule_id__delete"></a>

`DELETE /api/v0/rules/{rule_id}`

Delete a rule based on the provided user and rule ID.

<h3 id="delete-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a rule|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="delete-rule-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Rule

<a id="opIdget_rule_api_v0_rules__rule_id__get"></a>

`GET /api/v0/rules/{rule_id}`

Get a rule based on the provided user and rule ID.

<h3 id="get-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a rule|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-rule-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Simulate Rules

<a id="opIdsimulate_rules_api_v0_rules_simulate_post"></a>

`POST /api/v0/rules/simulate`

Simulate rules against historical charges data.

> Body parameter

```json
{
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "rules": [
    {
      "value": "string",
      "decision": "string",
      "expire_at": "2019-08-24T14:15:22Z"
    }
  ],
  "include_charge_ids": false
}
```

<h3 id="simulate-rules-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SimulationRequest](#schemasimulationrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="simulate-rules-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Simulate rules|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="simulate-rules-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-blacklists">blacklists</h1>

## Add Blacklist

<a id="opIdadd_blacklist_api_v0_blacklists__post"></a>

`POST /api/v0/blacklists/`

Add a blacklist.

> Body parameter

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="add-blacklist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BlacklistRequest](#schemablacklistrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="add-blacklist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Add a blacklist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="add-blacklist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Blacklists

<a id="opIdlist_blacklists_api_v0_blacklists__get"></a>

`GET /api/v0/blacklists/`

Fetch all blacklists with pagination.

<h3 id="list-blacklists-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-blacklists-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fetch blacklists|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-blacklists-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Blacklist

<a id="opIdupdate_blacklist_api_v0_blacklists__blacklist_id__put"></a>

`PUT /api/v0/blacklists/{blacklist_id}`

Update a blacklist.

> Body parameter

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="update-blacklist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|
|body|body|[BlacklistRequest](#schemablacklistrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-blacklist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update a blacklist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-blacklist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Blacklist

<a id="opIddelete_blacklist_api_v0_blacklists__blacklist_id__delete"></a>

`DELETE /api/v0/blacklists/{blacklist_id}`

Delete a blacklist.

<h3 id="delete-blacklist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-blacklist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a blacklist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="delete-blacklist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Blacklist

<a id="opIdget_blacklist_api_v0_blacklists__blacklist_id__get"></a>

`GET /api/v0/blacklists/{blacklist_id}`

Get a blacklist by id.

<h3 id="get-blacklist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-blacklist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a blacklist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-blacklist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-whitelists">whitelists</h1>

## Add Whitelist

<a id="opIdadd_whitelist_api_v0_whitelists__post"></a>

`POST /api/v0/whitelists/`

Add a whitelist.

> Body parameter

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="add-whitelist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[WhitelistRequest](#schemawhitelistrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="add-whitelist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Add a whitelist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="add-whitelist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Fetch Whitelists

<a id="opIdfetch_whitelists_api_v0_whitelists__get"></a>

`GET /api/v0/whitelists/`

Fetch all whitelists with pagination.

<h3 id="fetch-whitelists-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="fetch-whitelists-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fetch whitelists|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="fetch-whitelists-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Whitelist

<a id="opIdupdate_whitelist_api_v0_whitelists__whitelist_id__put"></a>

`PUT /api/v0/whitelists/{whitelist_id}`

Update a whitelist.

> Body parameter

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="update-whitelist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|
|body|body|[WhitelistRequest](#schemawhitelistrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-whitelist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update a whitelist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-whitelist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Whitelist

<a id="opIddelete_whitelist_api_v0_whitelists__whitelist_id__delete"></a>

`DELETE /api/v0/whitelists/{whitelist_id}`

Delete a whitelist.

<h3 id="delete-whitelist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-whitelist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a whitelist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="delete-whitelist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Whitelist

<a id="opIdget_whitelist_api_v0_whitelists__whitelist_id__get"></a>

`GET /api/v0/whitelists/{whitelist_id}`

Get a whitelist by id.

<h3 id="get-whitelist-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-whitelist-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a whitelist|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-whitelist-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-snapshots">snapshots</h1>

## Create Snapshot

<a id="opIdcreate_snapshot_api_v0_snapshots__post"></a>

`POST /api/v0/snapshots/`

Create a snapshot.

> Body parameter

```json
{
  "description": "",
  "collections": [
    "string"
  ],
  "drop_existing": false
}
```

<h3 id="create-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SnapshotRequest](#schemasnapshotrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="create-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Create a snapshot|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="create-snapshot-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Snapshots

<a id="opIdlist_snapshots_api_v0_snapshots__get"></a>

`GET /api/v0/snapshots/`

Fetch all rules based on the provided page and size.

<h3 id="list-snapshots-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-snapshots-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List snapshots.|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-snapshots-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Snapshot

<a id="opIdget_snapshot_api_v0_snapshots__snapshot_id__get"></a>

`GET /api/v0/snapshots/{snapshot_id}`

Get snapshot by snapshot id.

<h3 id="get-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get snapshot by snapshot id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-snapshot-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Snapshot

<a id="opIddelete_snapshot_api_v0_snapshots__snapshot_id__delete"></a>

`DELETE /api/v0/snapshots/{snapshot_id}`

Delete snapshot by snapshot id.

<h3 id="delete-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete snapshot by snapshot id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="delete-snapshot-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Snapshot Details

<a id="opIdget_snapshot_details_api_v0_snapshots__snapshot_id__metadata_get"></a>

`GET /api/v0/snapshots/{snapshot_id}/metadata`

Get snapshot metadata by snapshot id.

<h3 id="get-snapshot-details-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-snapshot-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get snapshot metadata by snapshot id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-snapshot-details-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Restore Snapshot

<a id="opIdrestore_snapshot_api_v0_snapshots__snapshot_id__restore_post"></a>

`POST /api/v0/snapshots/{snapshot_id}/restore`

Restore snapshot.

> Body parameter

```json
{
  "description": "",
  "collections": [
    "string"
  ],
  "drop_existing": false
}
```

<h3 id="restore-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|
|body|body|[SnapshotRequest](#schemasnapshotrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="restore-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Restore snapshot by snapshot id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="restore-snapshot-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Restore Snapshots

<a id="opIdlist_restore_snapshots_api_v0_snapshots__snapshot_id__restore_get"></a>

`GET /api/v0/snapshots/{snapshot_id}/restore`

Fetch all rules based on the provided page and size.

<h3 id="list-restore-snapshots-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-restore-snapshots-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List restore snapshots.|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-restore-snapshots-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Restore Snapshot

<a id="opIdget_restore_snapshot_api_v0_snapshots__snapshot_id__restore__snapshot_restore_id__get"></a>

`GET /api/v0/snapshots/{snapshot_id}/restore/{snapshot_restore_id}`

Get restore snapshot by restore snapshot id.

<h3 id="get-restore-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|
|snapshot_restore_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-restore-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get restore snapshot by restore snapshot id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-restore-snapshot-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Compare Snapshots

<a id="opIdcompare_snapshots_api_v0_snapshots_compare_post"></a>

`POST /api/v0/snapshots/compare`

Compare two snapshots and return the differences.

> Body parameter

```json
{
  "baseline_snapshot_id": "string",
  "current_snapshot_id": "string"
}
```

<h3 id="compare-snapshots-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SnapshotCompareRequest](#schemasnapshotcomparerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="compare-snapshots-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Compare two snapshots|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="compare-snapshots-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-aggregations">aggregations</h1>

## Add Aggregation

<a id="opIdadd_aggregation_api_v0_aggregations__post"></a>

`POST /api/v0/aggregations/`

Add a aggregation based.

> Body parameter

```json
{
  "name": "string",
  "value": "string",
  "periods": [
    0
  ]
}
```

<h3 id="add-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AggregationRequest](#schemaaggregationrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="add-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Add a aggregation|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="add-aggregation-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Aggregations

<a id="opIdlist_aggregations_api_v0_aggregations__get"></a>

`GET /api/v0/aggregations/`

Fetch all aggregations.

<h3 id="list-aggregations-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-aggregations-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List aggregations|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-aggregations-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Aggregation

<a id="opIdupdate_aggregation_api_v0_aggregations__aggregation_id__put"></a>

`PUT /api/v0/aggregations/{aggregation_id}`

Update a aggregation.

> Body parameter

```json
{
  "name": "string",
  "value": "string",
  "periods": [
    0
  ]
}
```

<h3 id="update-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|
|body|body|[AggregationRequest](#schemaaggregationrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update a aggregation|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-aggregation-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Aggregation

<a id="opIddelete_aggregation_api_v0_aggregations__aggregation_id__delete"></a>

`DELETE /api/v0/aggregations/{aggregation_id}`

Delete a aggregation.

<h3 id="delete-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Delete a aggregation|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="delete-aggregation-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Aggregation

<a id="opIdget_aggregation_api_v0_aggregations__aggregation_id__get"></a>

`GET /api/v0/aggregations/{aggregation_id}`

Get a aggregation.

<h3 id="get-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get a aggregation|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-aggregation-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Fields

<a id="opIdlist_fields_api_v0_aggregations_fields_get"></a>

`GET /api/v0/aggregations/fields`

Get list of aggregation fields.

> Example responses

> 200 Response

```json
null
```

<h3 id="list-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List aggregation fields|Inline|

<h3 id="list-fields-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Fields Description

<a id="opIdlist_fields_description_api_v0_aggregations_fields_description_get"></a>

`GET /api/v0/aggregations/fields/description`

Get list of aggregation fields description.

> Example responses

> 200 Response

```json
null
```

<h3 id="list-fields-description-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List aggregation fields description|Inline|

<h3 id="list-fields-description-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Aggregation Events

<a id="opIdget_aggregation_events_api_v0_aggregations_charges__charge_id__events_get"></a>

`GET /api/v0/aggregations/charges/{charge_id}/events`

Get a aggregation events by charge id.

<h3 id="get-aggregation-events-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-aggregation-events-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List aggregation events by charge id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-aggregation-events-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Aggregation Events Logs

<a id="opIdget_aggregation_events_logs_api_v0_aggregations_charges__charge_id__logs_get"></a>

`GET /api/v0/aggregations/charges/{charge_id}/logs`

Get a aggregation events by charge id.

<h3 id="get-aggregation-events-logs-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-aggregation-events-logs-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List aggregation events logs by charge id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-aggregation-events-logs-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-anomalies">anomalies</h1>

## Tree

<a id="opIdtree_api_v0_anomalies_tree_post"></a>

`POST /api/v0/anomalies/tree`

Detect and optimize anomalies in data based on the provided criteria.

This endpoint analyzes data from Elasticsearch using the anomaly detection algorithm
and then applies optimization techniques to identify the most relevant patterns and anomalies.

The optimization includes parameters for:
- Top N results: Limit the number of top results to consider
- Minimum value threshold: Filter out results below a certain value
- Minimum percentage threshold: Filter out results below a certain percentage

Args:
    company_id: Company ID from authentication
    deps: Application dependencies
    request: Optimized anomaly detection request with fields, filters and optimization parameters

Returns:
    Response with optimized anomaly analysis results including optimized tree structure

> Body parameter

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "top": 5,
  "min_value": 0,
  "min_percentage": 0
}
```

<h3 id="tree-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyOptimizedRequest](#schemaanomalyoptimizedrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="tree-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Detect optimized anomalies in data|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="tree-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Discover

<a id="opIddiscover_api_v0_anomalies_discover_post"></a>

`POST /api/v0/anomalies/discover`

Auto-discover concentration patterns in data using DataSpot discover method.

This endpoint automatically discovers the most important patterns in your data
without needing to specify fields in advance. It uses DataSpot's discover algorithm
to identify the most significant concentration patterns.

Args:
    request: Discovery parameters including max_fields, min_percentage, and limit
    company_id: Company ID for data filtering
    deps: Application dependencies

Returns:
    AnomalyDiscoverResponse with discovered patterns and field rankings

> Body parameter

```json
{
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "max_fields": 3,
  "min_percentage": 5,
  "limit": 20
}
```

<h3 id="discover-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyDiscoverRequest](#schemaanomalydiscoverrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="discover-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Auto-discover anomaly patterns using DataSpot|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="discover-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Find

<a id="opIdfind_api_v0_anomalies_find_post"></a>

`POST /api/v0/anomalies/find`

Find concentration patterns in specified fields using DataSpot find method.

This endpoint finds where your data concentrates across the specified fields.
You can control the analysis with various filtering options like minimum percentage,
maximum depth, and pattern content filtering.

Args:
    request: Find parameters including fields, filtering options, and limits
    company_id: Company ID for data filtering
    deps: Application dependencies

Returns:
    AnomalyFindResponse with found concentration patterns

> Body parameter

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "min_percentage": 5,
  "max_depth": 3,
  "contains": "string",
  "min_count": 1,
  "sort_by": "percentage",
  "limit": 50
}
```

<h3 id="find-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyFindRequest](#schemaanomalyfindrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="find-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Find concentration patterns using DataSpot|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="find-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Analyze

<a id="opIdanalyze_api_v0_anomalies_analyze_post"></a>

`POST /api/v0/anomalies/analyze`

Perform enhanced statistical analysis using DataSpot analyze method.

This endpoint provides deep statistical insights into your data patterns,
including confidence scores, statistical significance, and actionable insights
for each discovered pattern.

Args:
    request: Analysis parameters including fields and statistical options
    company_id: Company ID for data filtering
    deps: Application dependencies

Returns:
    AnomalyAnalyzeResponse with statistical analysis results and insights

> Body parameter

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "min_percentage": 10
}
```

<h3 id="analyze-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyAnalyzeRequest](#schemaanomalyanalyzerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="analyze-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Perform statistical analysis using DataSpot|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="analyze-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Compare

<a id="opIdcompare_api_v0_anomalies_compare_post"></a>

`POST /api/v0/anomalies/compare`

Compare data patterns between current and baseline periods using DataSpot compare method.

This endpoint detects changes, new patterns, and disappeared patterns between
two time periods. Useful for A/B testing, change detection, and trend analysis.

Args:
    request: Comparison parameters including current/baseline periods and change thresholds
    company_id: Company ID for data filtering
    deps: Application dependencies

Returns:
    AnomalyCompareResponse with temporal comparison results and change detection

> Body parameter

```json
{
  "fields": [
    "string"
  ],
  "current_from_date": "2019-08-24T14:15:22Z",
  "current_to_date": "2019-08-24T14:15:22Z",
  "baseline_from_date": "2019-08-24T14:15:22Z",
  "baseline_to_date": "2019-08-24T14:15:22Z",
  "query": {},
  "change_threshold": 0.2,
  "statistical_significance": true
}
```

<h3 id="compare-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyCompareRequest](#schemaanomalycomparerequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="compare-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Compare data between time periods using DataSpot|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="compare-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Available Fields

<a id="opIdget_available_fields_api_v0_anomalies_fields_get"></a>

`GET /api/v0/anomalies/fields`

Get list of available fields that can be used for anomaly analysis.

Returns fields categorized by type:
- Customer fields (email, IP address, etc.)
- Payment fields (amount, currency, card details, etc.)
- Charge fields (status, timestamps, etc.)

Returns:
    Response with categorized list of available fields

> Example responses

> 200 Response

```json
null
```

<h3 id="get-available-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get available fields for anomaly analysis|Inline|

<h3 id="get-available-fields-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-charges">charges</h1>

## Get Charge

<a id="opIdget_charge_api_v0_charges__charge_id__get"></a>

`GET /api/v0/charges/{charge_id}`

Get a charge by id.

<h3 id="get-charge-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-charge-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get a charge by id|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-charge-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Charges

<a id="opIdlist_charges_api_v0_charges__get"></a>

`GET /api/v0/charges/`

Fetch all charges with pagination.

<h3 id="list-charges-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|none|
|page_size|query|integer|false|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="list-charges-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fetch charges|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="list-charges-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-graph">graph</h1>

## Get Graph Data

<a id="opIdget_graph_data_api_v0_graph__get"></a>

`GET /api/v0/graph/`

Get customer graph data for visualization.

This endpoint returns the relationship graph data for a specific customer,
including all connected customers (nodes) and their relationships (edges).
The data is optimized for graph visualization libraries like D3.js, vis.js, or Cytoscape.

Args:
    company_id: Company ID from authentication
    deps: Application dependencies
    customer_id: Customer ID to get graph data for

Returns:
    Response with graph nodes and edges data for visualization

Example:
    GET /api/v0/graph?customer_id=CUSTOMER_123

<h3 id="get-graph-data-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|customer_id|query|string|true|Customer ID to get graph data for|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-graph-data-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get customer graph data for visualization|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-graph-data-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Add Customer

<a id="opIdadd_customer_api_v0_graph__post"></a>

`POST /api/v0/graph/`

Add a new customer to the graph and calculate relationships.

This endpoint adds a customer to the relationship graph and automatically
calculates their relationships with existing customers based on shared
attributes like email, phone, card number, IP addresses, and device IDs.

Args:
    company_id: Company ID from authentication
    deps: Application dependencies
    request: Customer data to add to the graph

Returns:
    Response with relationship information for the added customer

> Body parameter

```json
{
  "customer_id": "string",
  "email": "string",
  "phone": "string",
  "card_number": "string",
  "merchant_id": "",
  "ip_addresses": [
    "string"
  ],
  "device_ids": [
    "string"
  ],
  "acceptance": 0,
  "declined": 0,
  "chargeback_fraud": 0,
  "chargeback_authorization": 0,
  "chargeback_processing_error": 0,
  "chargeback_customer_dispute": 0,
  "chargeback_non_receipt": 0,
  "chargeback_cancelled_recurring": 0,
  "chargeback_product_not_received": 0,
  "chargeback_duplicate_processing": 0
}
```

<h3 id="add-customer-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AddCustomerRequest](#schemaaddcustomerrequest)|true|none|

> Example responses

> 201 Response

```json
null
```

<h3 id="add-customer-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Add customer to graph and calculate relationships|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="add-customer-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Graph Stats

<a id="opIdget_graph_stats_api_v0_graph_stats_get"></a>

`GET /api/v0/graph/stats`

Get comprehensive customer graph statistics and analytics.

This endpoint provides detailed statistics about a customer's relationship component,
including the complete profile of the requested customer, transaction analytics,
chargeback analysis, and individual customer details for all related customers.
Perfect for fraud analysis and risk assessment with 360° visibility.

Args:
    company_id: Company ID from authentication
    deps: Application dependencies
    customer_id: Customer ID to get statistics for

Returns:
    Response with comprehensive statistics and analytics

<h3 id="get-graph-stats-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|customer_id|query|string|true|Customer ID to get statistics for|

> Example responses

> 200 Response

```json
null
```

<h3 id="get-graph-stats-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get customer graph statistics and analytics|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="get-graph-stats-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Health Check

<a id="opIdhealth_check_api_v0_graph_health_get"></a>

`GET /api/v0/graph/health`

Check the health status of the graph service.

This endpoint provides information about:
- Total customers in the graph
- Fraud ring distribution statistics (ring size → count)
- Overall service health

Note:
    Fraud ring distribution shows how customers are grouped:
    - "1": isolated customers (no connections)
    - "2": pairs of connected customers
    - "5": fraud rings with 5 connected customers

Returns:
    Response with health status and basic statistics

> Example responses

> 200 Response

```json
null
```

<h3 id="health-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Check graph service health and statistics|Inline|

<h3 id="health-check-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="fastapi-companies">companies</h1>

## Get Configuration

<a id="opIdget_configuration_api_v0_companies_configuration_execution__get"></a>

`GET /api/v0/companies/configuration/execution/`

Get the execution configuration for a company.

> Example responses

> 200 Response

```json
null
```

<h3 id="get-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get company execution configuration|Inline|

<h3 id="get-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Configuration

<a id="opIdupdate_configuration_api_v0_companies_configuration_execution__put"></a>

`PUT /api/v0/companies/configuration/execution/`

Update an existing execution configuration.

> Body parameter

```json
{
  "configuration": [
    {
      "priority": 0,
      "name": "string",
      "type": "string",
      "description": "string",
      "enabled": true,
      "stop_on_match": false
    }
  ]
}
```

<h3 id="update-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationRequest](#schemaconfigurationrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update execution configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create Configuration

<a id="opIdcreate_configuration_api_v0_companies_configuration_execution__post"></a>

`POST /api/v0/companies/configuration/execution/`

Create a new execution configuration for a company.

> Body parameter

```json
{
  "configuration": [
    {
      "priority": 0,
      "name": "string",
      "type": "string",
      "description": "string",
      "enabled": true,
      "stop_on_match": false
    }
  ]
}
```

<h3 id="create-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationRequest](#schemaconfigurationrequest)|true|none|

> Example responses

> 201 Response

```json
null
```

<h3 id="create-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Create execution configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="create-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Decision Configuration

<a id="opIdget_decision_configuration_api_v0_companies_configuration_decision__get"></a>

`GET /api/v0/companies/configuration/decision/`

Get the decision configuration for a company.

> Example responses

> 200 Response

```json
null
```

<h3 id="get-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get company decision configuration|Inline|

<h3 id="get-decision-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Decision Configuration

<a id="opIdupdate_decision_configuration_api_v0_companies_configuration_decision__put"></a>

`PUT /api/v0/companies/configuration/decision/`

Update an existing decision configuration.

> Body parameter

```json
{
  "configuration": [
    {
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}
```

<h3 id="update-decision-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationDecisionRequest](#schemaconfigurationdecisionrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update decision configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-decision-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create Decision Configuration

<a id="opIdcreate_decision_configuration_api_v0_companies_configuration_decision__post"></a>

`POST /api/v0/companies/configuration/decision/`

Create a new decision configuration for a company.

> Body parameter

```json
{
  "configuration": [
    {
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}
```

<h3 id="create-decision-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationDecisionRequest](#schemaconfigurationdecisionrequest)|true|none|

> Example responses

> 201 Response

```json
null
```

<h3 id="create-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Create decision configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="create-decision-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Model Configuration

<a id="opIdget_model_configuration_api_v0_companies_configuration_models__get"></a>

`GET /api/v0/companies/configuration/models/`

Get the ML model configuration for a company.

> Example responses

> 200 Response

```json
null
```

<h3 id="get-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get company ML model configuration|Inline|

<h3 id="get-model-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Model Configuration

<a id="opIdupdate_model_configuration_api_v0_companies_configuration_models__put"></a>

`PUT /api/v0/companies/configuration/models/`

Update an existing ML model configuration.

> Body parameter

```json
{
  "configuration": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}
```

<h3 id="update-model-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationModelRequest](#schemaconfigurationmodelrequest)|true|none|

> Example responses

> 200 Response

```json
null
```

<h3 id="update-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update ML model configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-model-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create Model Configuration

<a id="opIdcreate_model_configuration_api_v0_companies_configuration_models__post"></a>

`POST /api/v0/companies/configuration/models/`

Create a new ML model configuration for a company.

> Body parameter

```json
{
  "configuration": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}
```

<h3 id="create-model-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationModelRequest](#schemaconfigurationmodelrequest)|true|none|

> Example responses

> 201 Response

```json
null
```

<h3 id="create-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Create ML model configuration|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="create-model-configuration-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Company Details

<a id="opIdget_company_details_api_v0_companies_details_get"></a>

`GET /api/v0/companies/details`

Get the details of the current company from the session token.

> Example responses

> 200 Response

```json
{
  "company_id": "string",
  "name": "string",
  "description": "string",
  "legal_representative_name": "string",
  "legal_representative_email": "string"
}
```

<h3 id="get-company-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get current company details|[CompanyResponse](#schemacompanyresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

# Schemas

<h2 id="tocS_AddCustomerRequest">AddCustomerRequest</h2>
<!-- backwards compatibility -->
<a id="schemaaddcustomerrequest"></a>
<a id="schema_AddCustomerRequest"></a>
<a id="tocSaddcustomerrequest"></a>
<a id="tocsaddcustomerrequest"></a>

```json
{
  "customer_id": "string",
  "email": "string",
  "phone": "string",
  "card_number": "string",
  "merchant_id": "",
  "ip_addresses": [
    "string"
  ],
  "device_ids": [
    "string"
  ],
  "acceptance": 0,
  "declined": 0,
  "chargeback_fraud": 0,
  "chargeback_authorization": 0,
  "chargeback_processing_error": 0,
  "chargeback_customer_dispute": 0,
  "chargeback_non_receipt": 0,
  "chargeback_cancelled_recurring": 0,
  "chargeback_product_not_received": 0,
  "chargeback_duplicate_processing": 0
}

```

AddCustomerRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|customer_id|string|true|none|Unique customer identifier|
|email|string|true|none|Customer email address|
|phone|string|true|none|Customer phone number|
|card_number|string|true|none|Customer card number|
|merchant_id|string|false|none|Merchant identifier|
|ip_addresses|[string]|false|none|List of IP addresses|
|device_ids|[string]|false|none|List of device identifiers|
|acceptance|integer|false|none|Number of accepted transactions|
|declined|integer|false|none|Number of declined transactions|
|chargeback_fraud|integer|false|none|Fraud chargebacks count|
|chargeback_authorization|integer|false|none|Authorization chargebacks count|
|chargeback_processing_error|integer|false|none|Processing error chargebacks count|
|chargeback_customer_dispute|integer|false|none|Customer dispute chargebacks count|
|chargeback_non_receipt|integer|false|none|Non-receipt chargebacks count|
|chargeback_cancelled_recurring|integer|false|none|Cancelled recurring chargebacks count|
|chargeback_product_not_received|integer|false|none|Product not received chargebacks count|
|chargeback_duplicate_processing|integer|false|none|Duplicate processing chargebacks count|

<h2 id="tocS_AggregationRequest">AggregationRequest</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationrequest"></a>
<a id="schema_AggregationRequest"></a>
<a id="tocSaggregationrequest"></a>
<a id="tocsaggregationrequest"></a>

```json
{
  "name": "string",
  "value": "string",
  "periods": [
    0
  ]
}

```

AggregationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|value|string|true|none|none|
|periods|[integer]|true|none|none|

<h2 id="tocS_AnomalyAnalyzeRequest">AnomalyAnalyzeRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyanalyzerequest"></a>
<a id="schema_AnomalyAnalyzeRequest"></a>
<a id="tocSanomalyanalyzerequest"></a>
<a id="tocsanomalyanalyzerequest"></a>

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "min_percentage": 10
}

```

AnomalyAnalyzeRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze statistically|
|query|any|false|none|Query filters for data retrieval|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|any|false|none|Start date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|to_date|any|false|none|End date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|min_percentage|number|false|none|Minimum percentage threshold for analysis|

<h2 id="tocS_AnomalyCompareRequest">AnomalyCompareRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalycomparerequest"></a>
<a id="schema_AnomalyCompareRequest"></a>
<a id="tocSanomalycomparerequest"></a>
<a id="tocsanomalycomparerequest"></a>

```json
{
  "fields": [
    "string"
  ],
  "current_from_date": "2019-08-24T14:15:22Z",
  "current_to_date": "2019-08-24T14:15:22Z",
  "baseline_from_date": "2019-08-24T14:15:22Z",
  "baseline_to_date": "2019-08-24T14:15:22Z",
  "query": {},
  "change_threshold": 0.2,
  "statistical_significance": true
}

```

AnomalyCompareRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to compare between periods|
|current_from_date|string(date-time)|true|none|Start date for current period|
|current_to_date|string(date-time)|true|none|End date for current period|
|baseline_from_date|string(date-time)|true|none|Start date for baseline period|
|baseline_to_date|string(date-time)|true|none|End date for baseline period|
|query|any|false|none|Query filters for data retrieval|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|change_threshold|number|false|none|Threshold for detecting significant changes|
|statistical_significance|boolean|false|none|Include statistical significance tests|

<h2 id="tocS_AnomalyDiscoverRequest">AnomalyDiscoverRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalydiscoverrequest"></a>
<a id="schema_AnomalyDiscoverRequest"></a>
<a id="tocSanomalydiscoverrequest"></a>
<a id="tocsanomalydiscoverrequest"></a>

```json
{
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "max_fields": 3,
  "min_percentage": 5,
  "limit": 20
}

```

AnomalyDiscoverRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|query|any|false|none|Query filters for data retrieval|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|any|false|none|Start date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|to_date|any|false|none|End date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|max_fields|integer|false|none|Maximum number of fields to analyze simultaneously|
|min_percentage|number|false|none|Minimum percentage threshold for pattern discovery|
|limit|integer|false|none|Maximum number of patterns to discover|

<h2 id="tocS_AnomalyFindRequest">AnomalyFindRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyfindrequest"></a>
<a id="schema_AnomalyFindRequest"></a>
<a id="tocSanomalyfindrequest"></a>
<a id="tocsanomalyfindrequest"></a>

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "min_percentage": 5,
  "max_depth": 3,
  "contains": "string",
  "min_count": 1,
  "sort_by": "percentage",
  "limit": 50
}

```

AnomalyFindRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze for patterns|
|query|any|false|none|Query filters for data retrieval|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|any|false|none|Start date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|to_date|any|false|none|End date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|min_percentage|number|false|none|Minimum percentage threshold for patterns|
|max_depth|integer|false|none|Maximum depth for pattern hierarchy|
|contains|any|false|none|Pattern must contain this string|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|min_count|integer|false|none|Minimum count for patterns|
|sort_by|string|false|none|Sort patterns by: percentage, count|
|limit|integer|false|none|Maximum number of patterns to return|

<h2 id="tocS_AnomalyOptimizedRequest">AnomalyOptimizedRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyoptimizedrequest"></a>
<a id="schema_AnomalyOptimizedRequest"></a>
<a id="tocSanomalyoptimizedrequest"></a>
<a id="tocsanomalyoptimizedrequest"></a>

```json
{
  "fields": [
    "string"
  ],
  "query": {},
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "top": 5,
  "min_value": 0,
  "min_percentage": 0
}

```

AnomalyOptimizedRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze for anomalies|
|query|any|false|none|Query filters for data retrieval|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|any|false|none|Start date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|to_date|any|false|none|End date for data analysis|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|top|integer|false|none|Number of top elements to consider in optimization|
|min_value|any|false|none|Minimum value threshold for optimization|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|integer|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|min_percentage|any|false|none|Minimum percentage threshold for optimization|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|integer|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_BlacklistRequest">BlacklistRequest</h2>
<!-- backwards compatibility -->
<a id="schemablacklistrequest"></a>
<a id="schema_BlacklistRequest"></a>
<a id="tocSblacklistrequest"></a>
<a id="tocsblacklistrequest"></a>

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}

```

BlacklistRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|none|
|expire_at|string(date-time)|false|none|none|

<h2 id="tocS_ChargeRequest">ChargeRequest</h2>
<!-- backwards compatibility -->
<a id="schemachargerequest"></a>
<a id="schema_ChargeRequest"></a>
<a id="tocSchargerequest"></a>
<a id="tocschargerequest"></a>

```json
{
  "charge_id": "string",
  "status": "pending",
  "customer": {
    "full_name": "string",
    "phone_number": "string",
    "email": "string",
    "ip_address": "string",
    "fingerprint": "string"
  },
  "payment": {
    "currency": "USD",
    "amount": 0,
    "fee": 0,
    "card_hash": "string",
    "card_type": "string",
    "exp_month": "string",
    "brand": "string",
    "bin_number": "string",
    "cvc": "string"
  }
}

```

ChargeRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|charge_id|string|true|none|none|
|status|string|false|none|none|
|customer|[CustomerRequest](#schemacustomerrequest)|false|none|Pydantic model for customer data in charge requests.|
|payment|[PaymentRequest](#schemapaymentrequest)|false|none|Pydantic model for payment data in charge requests.|

<h2 id="tocS_CompanyResponse">CompanyResponse</h2>
<!-- backwards compatibility -->
<a id="schemacompanyresponse"></a>
<a id="schema_CompanyResponse"></a>
<a id="tocScompanyresponse"></a>
<a id="tocscompanyresponse"></a>

```json
{
  "company_id": "string",
  "name": "string",
  "description": "string",
  "legal_representative_name": "string",
  "legal_representative_email": "string"
}

```

CompanyResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|company_id|string|true|none|none|
|name|string|true|none|none|
|description|string|true|none|none|
|legal_representative_name|string|true|none|none|
|legal_representative_email|string|true|none|none|

<h2 id="tocS_ConfigurationDecisionItemRequest">ConfigurationDecisionItemRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationdecisionitemrequest"></a>
<a id="schema_ConfigurationDecisionItemRequest"></a>
<a id="tocSconfigurationdecisionitemrequest"></a>
<a id="tocsconfigurationdecisionitemrequest"></a>

```json
{
  "name": "string",
  "description": "string",
  "enabled": true
}

```

ConfigurationDecisionItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|description|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|enabled|boolean|false|none|none|

<h2 id="tocS_ConfigurationDecisionRequest">ConfigurationDecisionRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationdecisionrequest"></a>
<a id="schema_ConfigurationDecisionRequest"></a>
<a id="tocSconfigurationdecisionrequest"></a>
<a id="tocsconfigurationdecisionrequest"></a>

```json
{
  "configuration": [
    {
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}

```

ConfigurationDecisionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationDecisionItemRequest](#schemaconfigurationdecisionitemrequest)]|true|none|[Request model for a decision configuration item.]|

<h2 id="tocS_ConfigurationItemRequest">ConfigurationItemRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationitemrequest"></a>
<a id="schema_ConfigurationItemRequest"></a>
<a id="tocSconfigurationitemrequest"></a>
<a id="tocsconfigurationitemrequest"></a>

```json
{
  "priority": 0,
  "name": "string",
  "type": "string",
  "description": "string",
  "enabled": true,
  "stop_on_match": false
}

```

ConfigurationItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|priority|integer|true|none|none|
|name|string|true|none|none|
|type|string|true|none|none|
|description|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|enabled|boolean|false|none|none|
|stop_on_match|boolean|false|none|none|

<h2 id="tocS_ConfigurationModelItemRequest">ConfigurationModelItemRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationmodelitemrequest"></a>
<a id="schema_ConfigurationModelItemRequest"></a>
<a id="tocSconfigurationmodelitemrequest"></a>
<a id="tocsconfigurationmodelitemrequest"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "enabled": true
}

```

ConfigurationModelItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|name|string|true|none|none|
|description|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|enabled|boolean|false|none|none|

<h2 id="tocS_ConfigurationModelRequest">ConfigurationModelRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationmodelrequest"></a>
<a id="schema_ConfigurationModelRequest"></a>
<a id="tocSconfigurationmodelrequest"></a>
<a id="tocsconfigurationmodelrequest"></a>

```json
{
  "configuration": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "enabled": true
    }
  ]
}

```

ConfigurationModelRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationModelItemRequest](#schemaconfigurationmodelitemrequest)]|true|none|[Request model for a ML model configuration item.]|

<h2 id="tocS_ConfigurationRequest">ConfigurationRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationrequest"></a>
<a id="schema_ConfigurationRequest"></a>
<a id="tocSconfigurationrequest"></a>
<a id="tocsconfigurationrequest"></a>

```json
{
  "configuration": [
    {
      "priority": 0,
      "name": "string",
      "type": "string",
      "description": "string",
      "enabled": true,
      "stop_on_match": false
    }
  ]
}

```

ConfigurationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationItemRequest](#schemaconfigurationitemrequest)]|true|none|[Request model for a configuration item.]|

<h2 id="tocS_CustomerRequest">CustomerRequest</h2>
<!-- backwards compatibility -->
<a id="schemacustomerrequest"></a>
<a id="schema_CustomerRequest"></a>
<a id="tocScustomerrequest"></a>
<a id="tocscustomerrequest"></a>

```json
{
  "full_name": "string",
  "phone_number": "string",
  "email": "string",
  "ip_address": "string",
  "fingerprint": "string"
}

```

CustomerRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|full_name|string|true|none|none|
|phone_number|string|true|none|none|
|email|string|true|none|none|
|ip_address|string|true|none|none|
|fingerprint|string|true|none|none|

<h2 id="tocS_HTTPValidationError">HTTPValidationError</h2>
<!-- backwards compatibility -->
<a id="schemahttpvalidationerror"></a>
<a id="schema_HTTPValidationError"></a>
<a id="tocShttpvalidationerror"></a>
<a id="tocshttpvalidationerror"></a>

```json
{
  "detail": [
    {
      "loc": [
        "string"
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}

```

HTTPValidationError

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|detail|[[ValidationError](#schemavalidationerror)]|false|none|none|

<h2 id="tocS_PaymentRequest">PaymentRequest</h2>
<!-- backwards compatibility -->
<a id="schemapaymentrequest"></a>
<a id="schema_PaymentRequest"></a>
<a id="tocSpaymentrequest"></a>
<a id="tocspaymentrequest"></a>

```json
{
  "currency": "USD",
  "amount": 0,
  "fee": 0,
  "card_hash": "string",
  "card_type": "string",
  "exp_month": "string",
  "brand": "string",
  "bin_number": "string",
  "cvc": "string"
}

```

PaymentRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|currency|string|false|none|none|
|amount|number|true|none|none|
|fee|number|true|none|none|
|card_hash|string|true|none|none|
|card_type|string|true|none|none|
|exp_month|string|true|none|none|
|brand|string|true|none|none|
|bin_number|string|true|none|none|
|cvc|string|true|none|none|

<h2 id="tocS_RuleRequest">RuleRequest</h2>
<!-- backwards compatibility -->
<a id="schemarulerequest"></a>
<a id="schema_RuleRequest"></a>
<a id="tocSrulerequest"></a>
<a id="tocsrulerequest"></a>

```json
{
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}

```

RuleRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|none|
|decision|string|true|none|none|
|expire_at|string(date-time)|false|none|none|

<h2 id="tocS_SimulationRequest">SimulationRequest</h2>
<!-- backwards compatibility -->
<a id="schemasimulationrequest"></a>
<a id="schema_SimulationRequest"></a>
<a id="tocSsimulationrequest"></a>
<a id="tocssimulationrequest"></a>

```json
{
  "from_date": "2019-08-24T14:15:22Z",
  "to_date": "2019-08-24T14:15:22Z",
  "rules": [
    {
      "value": "string",
      "decision": "string",
      "expire_at": "2019-08-24T14:15:22Z"
    }
  ],
  "include_charge_ids": false
}

```

SimulationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|string(date-time)|true|none|none|
|to_date|string(date-time)|true|none|none|
|rules|[[RuleRequest](#schemarulerequest)]|true|none|[Pydantic model for the rule object.]|
|include_charge_ids|boolean|false|none|Whether to include charge IDs in rule applications|

<h2 id="tocS_SnapshotCompareRequest">SnapshotCompareRequest</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotcomparerequest"></a>
<a id="schema_SnapshotCompareRequest"></a>
<a id="tocSsnapshotcomparerequest"></a>
<a id="tocssnapshotcomparerequest"></a>

```json
{
  "baseline_snapshot_id": "string",
  "current_snapshot_id": "string"
}

```

SnapshotCompareRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|baseline_snapshot_id|string|true|none|none|
|current_snapshot_id|string|true|none|none|

<h2 id="tocS_SnapshotRequest">SnapshotRequest</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotrequest"></a>
<a id="schema_SnapshotRequest"></a>
<a id="tocSsnapshotrequest"></a>
<a id="tocssnapshotrequest"></a>

```json
{
  "description": "",
  "collections": [
    "string"
  ],
  "drop_existing": false
}

```

SnapshotRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|description|string|false|none|none|
|collections|[string]|true|none|none|
|drop_existing|boolean|false|none|none|

<h2 id="tocS_ValidationError">ValidationError</h2>
<!-- backwards compatibility -->
<a id="schemavalidationerror"></a>
<a id="schema_ValidationError"></a>
<a id="tocSvalidationerror"></a>
<a id="tocsvalidationerror"></a>

```json
{
  "loc": [
    "string"
  ],
  "msg": "string",
  "type": "string"
}

```

ValidationError

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|loc|[anyOf]|true|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|integer|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|msg|string|true|none|none|
|type|string|true|none|none|

<h2 id="tocS_WhitelistRequest">WhitelistRequest</h2>
<!-- backwards compatibility -->
<a id="schemawhitelistrequest"></a>
<a id="schema_WhitelistRequest"></a>
<a id="tocSwhitelistrequest"></a>
<a id="tocswhitelistrequest"></a>

```json
{
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z"
}

```

WhitelistRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|none|
|expire_at|string(date-time)|false|none|none|

