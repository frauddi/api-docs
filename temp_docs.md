---
title: Frauddi API v1.0.0
language_tabs:
  - shell: cURL
  - javascript: JavaScript
  - python: Python
language_clients:
  - shell: ""
  - javascript: ""
  - python: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="frauddi-api">Frauddi API v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

The Frauddi API is organized around REST. Our API has predictable resource-oriented URLs, accepts JSON-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes and authentication.

## Authentication

Authenticate API requests using your API key in the Authorization header:

```
Authorization: Bearer your_api_key_here
```

## Making Requests

All API requests should be made over HTTPS to the base URL. Request and response bodies are JSON.

## Response Format

All API responses follow a consistent structure with appropriate HTTP status codes. Successful requests return relevant data objects, while errors return detailed error information.

## Getting Started

1. Obtain your API key from the Frauddi dashboard or by contacting our sales team
2. Make a test request to the health check endpoint
3. Submit transaction data to assessment endpoints
4. Configure rules and thresholds for your use case
    

Base URLs:

* <a href="https://api.frauddi.com">https://api.frauddi.com</a>

Email: <a href="mailto:support@frauddi.com">Frauddi Support</a> Web: <a href="https://frauddi.com/support">Frauddi Support</a> 

# Authentication

- HTTP Authentication, scheme: bearer 

<h1 id="frauddi-api-default">Default</h1>

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

<h1 id="frauddi-api-assessments">Assessments</h1>

## Assess Charge for Fraud Risk

<a id="opIdassessment_charge_api_v1_assessments_charges_post"></a>

`POST /api/v1/assessments/charges`

Submit a payment charge for real-time fraud assessment.

    This endpoint processes the charge through multiple detection layers:
    - **Whitelist/Blacklist checking** - Verify against trusted and blocked entities
    - **Rule Engine** - Apply custom fraud detection rules
    - **ML Models** - Advanced pattern recognition and anomaly detection
    - **Graph Analysis** - Relationship mapping and network analysis
    - **Email Validation** - Email risk assessment and verification

    Returns a comprehensive risk assessment with decision rationale and score.

> Body parameter

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}
```

<h3 id="assess-charge-for-fraud-risk-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "decision": "ACCEPT",
  "score": 0.15,
  "decided_by": {
    "module": "RULES",
    "priority": 1,
    "decision": "ACCEPT"
  },
  "assessment_id": "550e8400-e29b-41d4-a716-446655440000",
  "details": {
    "whitelists": {
      "decision": "NO_DECISION"
    },
    "blacklists": {
      "decision": "NO_DECISION"
    },
    "rules": {
      "decision": "ACCEPT",
      "matched_rules": [
        "rule_1"
      ]
    }
  }
}
```

<h3 id="assess-charge-for-fraud-risk-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fraud assessment completed successfully|[AssessmentDataResponse](#schemaassessmentdataresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid charge data or configuration error|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in charge data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assess Email Risk

<a id="opIdassessment_email_api_v1_assessments_emails_post"></a>

`POST /api/v1/assessments/emails`

Validate and assess risk for customer email addresses.

    This endpoint analyzes email addresses for:
    - **Domain reputation** - Check email domain against threat databases
    - **Disposable email detection** - Identify temporary or throwaway emails
    - **Syntax validation** - Verify email format and structure
    - **Risk scoring** - Calculate fraud probability based on email patterns

    Returns assessment with email-specific risk indicators and recommendations.

> Body parameter

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}
```

<h3 id="assess-email-risk-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "decision": "ACCEPT",
  "assessment_id": "550e8400-e29b-41d4-a716-446655440000",
  "assessment_type": "EMAIL",
  "decided_by": {
    "module": "EMAIL",
    "priority": 1,
    "decision": "ACCEPT"
  },
  "decision_details": {
    "EMAIL": {
      "result": {
        "is_valid": true,
        "is_disposable": false,
        "domain_reputation": "good"
      }
    }
  }
}
```

<h3 id="assess-email-risk-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Email assessment completed successfully|[AssessmentDataResponse](#schemaassessmentdataresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid email format or charge data|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Assess Risk Using Rules

<a id="opIdassessment_rule_api_v1_assessments_rules_post"></a>

`POST /api/v1/assessments/rules`

Evaluate transaction risk using your custom fraud detection rules.

    This endpoint applies all active rules configured for your company and returns:
    - **Rule evaluation results** - Which rules matched and their outcomes
    - **Decision hierarchy** - Rule priority and decision logic
    - **Custom logic execution** - DSL-based business rules processing
    - **Threshold analysis** - Rule confidence scores and thresholds

    Rules are processed in priority order and can trigger various actions (ACCEPT, REVIEW, DECLINE).

> Body parameter

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}
```

<h3 id="assess-risk-using-rules-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "decision": "REVIEW",
  "assessment_id": "550e8400-e29b-41d4-a716-446655440000",
  "assessment_type": "RULE",
  "decided_by": {
    "module": "RULES",
    "priority": 1,
    "decision": "REVIEW"
  },
  "decision_details": {
    "RULES": {
      "result": {
        "matched_rules": [
          "high_amount_rule",
          "new_customer_rule"
        ],
        "rule_scores": {
          "high_amount_rule": 0.8,
          "new_customer_rule": 0.6
        },
        "final_score": 0.85
      }
    }
  }
}
```

<h3 id="assess-risk-using-rules-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Rules assessment completed successfully|[AssessmentDataResponse](#schemaassessmentdataresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid charge data or rule configuration error|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Check Against Blacklists

<a id="opIdassessment_blacklist_api_v1_assessments_blacklists_post"></a>

`POST /api/v1/assessments/blacklists`

Check transaction and customer data against your company's blacklists.

    This endpoint validates multiple data points against blacklisted entities:
    - **Email addresses** - Blocked customer emails
    - **IP addresses** - Suspicious or blocked IPs
    - **Card numbers** - Blocked payment methods (hashed for security)
    - **Phone numbers** - Blocked customer phone numbers
    - **Device fingerprints** - Blocked devices or browsers

    Returns immediate DECLINE decision if any blacklisted entity is detected.

> Body parameter

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}
```

<h3 id="check-against-blacklists-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "decision": "DECLINE",
  "assessment_id": "550e8400-e29b-41d4-a716-446655440000",
  "assessment_type": "BLACKLIST",
  "decided_by": {
    "module": "BLACKLISTS",
    "priority": 1,
    "decision": "DECLINE"
  },
  "decision_details": {
    "BLACKLISTS": {
      "result": {
        "matches_found": [
          "email",
          "ip_address"
        ],
        "blacklisted_email": "fraud@example.com",
        "blacklisted_ip": "192.168.1.100"
      }
    }
  }
}
```

<h3 id="check-against-blacklists-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Blacklist assessment completed successfully|[AssessmentDataResponse](#schemaassessmentdataresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid charge data|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Check Against Whitelists

<a id="opIdassessment_whitelist_api_v1_assessments_whitelists_post"></a>

`POST /api/v1/assessments/whitelists`

Check transaction and customer data against your company's whitelists.

    This endpoint validates multiple data points against trusted entities:
    - **Email addresses** - Trusted customer emails
    - **IP addresses** - Trusted or corporate IPs
    - **Card numbers** - Trusted payment methods (hashed for security)
    - **Phone numbers** - Verified customer phone numbers
    - **Device fingerprints** - Trusted devices or browsers

    Returns immediate ACCEPT decision if any whitelisted entity is detected, bypassing other fraud checks.

> Body parameter

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}
```

<h3 id="check-against-whitelists-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ChargeRequest](#schemachargerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "decision": "ACCEPT",
  "assessment_id": "550e8400-e29b-41d4-a716-446655440000",
  "assessment_type": "WHITELIST",
  "decided_by": {
    "module": "WHITELISTS",
    "priority": 1,
    "decision": "ACCEPT"
  },
  "decision_details": {
    "WHITELISTS": {
      "result": {
        "matches_found": [
          "email"
        ],
        "whitelisted_email": "trusted@company.com",
        "bypass_reason": "trusted_customer"
      }
    }
  }
}
```

<h3 id="check-against-whitelists-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Whitelist assessment completed successfully|[AssessmentDataResponse](#schemaassessmentdataresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid charge data|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Assessment Details

<a id="opIdget_assessment_api_v1_assessments__assessment_id__get"></a>

`GET /api/v1/assessments/{assessment_id}`

Retrieve detailed information about a specific fraud assessment by its ID.

<h3 id="get-assessment-details-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|assessment_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "assessment_id": "string",
  "assessment_type": "string",
  "charge_id": "string",
  "company_id": "string",
  "decision": "string",
  "decided_by": {},
  "decision_details": {},
  "configuration": {},
  "data": {},
  "snapshot_id": "string",
  "created_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="get-assessment-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessment details retrieved successfully|[AssessmentResponse](#schemaassessmentresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Assessment not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Assessments by Type

<a id="opIdget_assessments_by_type_api_v1_assessments_type__assessment_type__get"></a>

`GET /api/v1/assessments/type/{assessment_type}`

Retrieve a paginated list of assessments filtered by type.

    Available assessment types:
    - **CHARGE** - Full transaction assessments
    - **EMAIL** - Email validation assessments
    - **RULE** - Rules-based assessments
    - **BLACKLIST** - Blacklist check assessments
    - **WHITELIST** - Whitelist check assessments

    Results are ordered by creation date (newest first) and support pagination.

<h3 id="list-assessments-by-type-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|assessment_type|path|string|true|none|
|current_page|query|integer|false|Page number (1-based)|
|page_size|query|integer|false|Number of assessments per page|

> Example responses

> 200 Response

```json
{
  "data": [],
  "pagination": {
    "current_page": 1,
    "has_next": true,
    "has_previous": false,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

<h3 id="list-assessments-by-type-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Assessments retrieved successfully|[AssessmentListResponse](#schemaassessmentlistresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid assessment type|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-rules">Rules</h1>

## Create fraud detection rule

<a id="opIdadd_rule_api_v1_rules__post"></a>

`POST /api/v1/rules/`

Create a new custom fraud detection rule using Frauddi's domain-specific language (DSL). Rules are evaluated in real-time during fraud assessments.

> Body parameter

```json
{
  "value": "payment.amount > 1000 and customer.email.contains('@gmail.com')",
  "decision": "ACCEPT",
  "expire_at": "2024-12-31T23:59:59Z"
}
```

<h3 id="create-fraud-detection-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RuleRequest](#schemarulerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="create-fraud-detection-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully created fraud detection rule|[RuleResponse](#schemaruleresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List fraud detection rules

<a id="opIdlist_rules_api_v1_rules__get"></a>

`GET /api/v1/rules/`

Retrieve a paginated list of all fraud detection rules for your company.

<h3 id="list-fraud-detection-rules-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number (1-based)|
|page_size|query|integer|false|Number of rules per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "id": "rule_123456",
      "value": "payment.amount > 1000 and customer.email.contains('@suspicious.com')",
      "decision": "REJECT",
      "expire_at": "2024-12-31T23:59:59Z",
      "created_at": "2024-01-15T10:30:00Z",
      "updated_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

> 422 Response

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

<h3 id="list-fraud-detection-rules-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved fraud detection rules with pagination|[RuleListResponse](#schemarulelistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update fraud detection rule

<a id="opIdupdate_rule_api_v1_rules__rule_id__put"></a>

`PUT /api/v1/rules/{rule_id}`

Update an existing fraud detection rule. The rule will be validated before applying changes.

> Body parameter

```json
{
  "value": "payment.amount > 1000 and customer.email.contains('@gmail.com')",
  "decision": "ACCEPT",
  "expire_at": "2024-12-31T23:59:59Z"
}
```

<h3 id="update-fraud-detection-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|
|body|body|[RuleRequest](#schemarulerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="update-fraud-detection-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated fraud detection rule|[RuleResponse](#schemaruleresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete fraud detection rule

<a id="opIddelete_rule_api_v1_rules__rule_id__delete"></a>

`DELETE /api/v1/rules/{rule_id}`

Permanently delete a fraud detection rule. This action cannot be undone.

<h3 id="delete-fraud-detection-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|

> Example responses

> 422 Response

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

<h3 id="delete-fraud-detection-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Successfully deleted fraud detection rule|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get fraud detection rule

<a id="opIdget_rule_api_v1_rules__rule_id__get"></a>

`GET /api/v1/rules/{rule_id}`

Retrieve a specific fraud detection rule by its ID.

<h3 id="get-fraud-detection-rule-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|rule_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="get-fraud-detection-rule-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved fraud detection rule|[RuleResponse](#schemaruleresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Simulate fraud detection rules

<a id="opIdsimulate_rules_api_v1_rules_simulate_post"></a>

`POST /api/v1/rules/simulate`

Test how your fraud detection rules would perform against historical transaction data without affecting live assessments. This endpoint allows you to optimize rule logic and validate effectiveness before deploying to production.

> Body parameter

```json
{
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "rules": [
    {
      "decision": "REJECT",
      "expire_at": "2024-12-31T23:59:59Z",
      "value": "amount > 500"
    }
  ],
  "include_charge_ids": false
}
```

<h3 id="simulate-fraud-detection-rules-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SimulationRequest](#schemasimulationrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "baseline": {},
  "current": {},
  "impact": {
    "acceptance_change": 0,
    "acceptance_change_percentage": 0,
    "declined_change": 0,
    "declined_change_percentage": 0
  },
  "errors": [],
  "total_charges_analyzed": 0,
  "total_rules_evaluated": 0,
  "rule_applications": []
}
```

<h3 id="simulate-fraud-detection-rules-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully simulated fraud detection rules with performance metrics|[SimulationResponse](#schemasimulationresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-graph">Graph</h1>

## Get Customer Relationship Graph

<a id="opIdget_graph_data_api_v1_graph__get"></a>

`GET /api/v1/graph/`

Retrieve the relationship graph data for a specific customer showing all connected entities.

    This endpoint returns network analysis data including:
    - **Connected customers** - Other customers linked through shared attributes
    - **Relationship strength** - Confidence scores for connections
    - **Graph nodes** - Customer entities with their properties
    - **Graph edges** - Relationships between customers with metadata
    - **Visualization data** - Optimized for D3.js, vis.js, or Cytoscape libraries

    Perfect for fraud ring detection, customer network analysis, and relationship visualization.

<h3 id="get-customer-relationship-graph-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|customer_id|query|string|true|Customer ID to analyze relationships for|

> Example responses

> 200 Response

```json
{
  "nodes": [
    {
      "id": "CUSTOMER_123",
      "label": "John Doe",
      "email": "john@example.com",
      "risk_score": 0.3,
      "connections": 2
    }
  ],
  "edges": [
    {
      "source": "CUSTOMER_123",
      "target": "CUSTOMER_456",
      "relationship_type": "shared_email",
      "strength": 0.85
    }
  ]
}
```

> 422 Response

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

<h3 id="get-customer-relationship-graph-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Graph data retrieved successfully|[GraphDataResponse](#schemagraphdataresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Customer not found in graph|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Add Customer to Graph

<a id="opIdadd_customer_api_v1_graph__post"></a>

`POST /api/v1/graph/`

Add a new customer to the relationship graph and automatically detect connections.

    This endpoint performs intelligent relationship detection based on shared attributes:
    - **Email addresses** - Exact and domain-based matching
    - **Phone numbers** - Direct number matching
    - **Card numbers** - Secure hash-based matching
    - **IP addresses** - Geographic and exact IP matching
    - **Device fingerprints** - Browser/device identification
    - **Address data** - Physical location correlation

    The system automatically calculates relationship strength and identifies potential fraud rings.

> Body parameter

```json
{
  "customer_id": "CUST_12345",
  "email": "customer@example.com",
  "phone": "+1234567890",
  "card_number": "4111111111111111",
  "merchant_id": "MERCH_001",
  "ip_addresses": [
    "192.168.1.1",
    "10.0.0.1"
  ],
  "device_ids": [
    "device_123",
    "mobile_456"
  ],
  "acceptance": 10,
  "declined": 2,
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

<h3 id="add-customer-to-graph-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AddCustomerRequest](#schemaaddcustomerrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "customer_id": "CUSTOMER_789",
  "relationships_detected": 3,
  "connected_customers": [
    "CUSTOMER_123",
    "CUSTOMER_456"
  ],
  "risk_indicators": [
    "shared_device",
    "same_ip_range"
  ],
  "graph_updated": true
}
```

<h3 id="add-customer-to-graph-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Customer added to graph successfully|[AddCustomerResponse](#schemaaddcustomerresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid customer data|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Graph Analytics & Statistics

<a id="opIdget_graph_stats_api_v1_graph_stats_get"></a>

`GET /api/v1/graph/stats`

Get comprehensive analytics and statistics for a customer's relationship network.

    This endpoint provides deep insights into customer relationships including:
    - **Network metrics** - Connection count, cluster size, centrality scores
    - **Risk indicators** - Network-based risk patterns and anomalies
    - **Transaction analytics** - Aggregated transaction data across the network
    - **Behavioral patterns** - Shared behaviors and suspicious activities
    - **Chargeback analysis** - Network-wide chargeback rates and patterns

    Essential for fraud investigation, risk assessment, and customer profiling with 360° network visibility.

<h3 id="get-graph-analytics-&-statistics-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|customer_id|query|string|true|Customer ID to analyze network statistics for|

> Example responses

> 200 Response

```json
{
  "customer_id": "CUSTOMER_123",
  "network_size": 15,
  "risk_score": 0.75,
  "transaction_count": 42,
  "chargeback_rate": 0.05,
  "connected_customers": 8,
  "suspicious_patterns": [
    "shared_device",
    "velocity_matching"
  ]
}
```

> 422 Response

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

<h3 id="get-graph-analytics-&-statistics-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Graph statistics retrieved successfully|[GraphStatsResponse](#schemagraphstatsresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Customer not found in graph|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-analytics">Analytics</h1>

## Create Analytics Aggregation

<a id="opIdadd_aggregation_api_v1_aggregations__post"></a>

`POST /api/v1/aggregations/`

Create a new data aggregation rule for analytics and pattern detection.

    Aggregations allow you to:
    - **Monitor transaction patterns** - Track volume, velocity, and behavior over time
    - **Set detection thresholds** - Define limits for suspicious activity
    - **Analyze customer behavior** - Aggregate data by customer, location, or device
    - **Create custom metrics** - Build business-specific fraud indicators
    - **Real-time monitoring** - Continuous evaluation of aggregated data

    Perfect for velocity checks, spending pattern analysis, and behavioral anomaly detection.

> Body parameter

```json
{
  "name": "daily_transactions",
  "value": "card:5m:count > 10",
  "periods": [
    5,
    30,
    60
  ]
}
```

<h3 id="create-analytics-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AggregationRequest](#schemaaggregationrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "aggregation_id": "agg_123456",
  "name": "Daily Transaction Volume",
  "field": "amount",
  "operation": "SUM",
  "time_window": "24h",
  "threshold": 10000,
  "status": "active"
}
```

<h3 id="create-analytics-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Aggregation created successfully|[AggregationResponse](#schemaaggregationresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid aggregation configuration|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Aggregation already exists|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Analytics Aggregations

<a id="opIdlist_aggregations_api_v1_aggregations__get"></a>

`GET /api/v1/aggregations/`

Retrieve a paginated list of all analytics aggregation rules for your company.

<h3 id="list-analytics-aggregations-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number (1-based)|
|page_size|query|integer|false|Number of aggregations per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "id": "agg_123456",
      "name": "Daily Transaction Volume",
      "value": "card:24h:count > 50 and customer:1h:amount_sum > 10000",
      "periods": [
        5,
        30,
        60,
        360
      ],
      "status": "ACTIVE",
      "created_at": "2024-01-15T10:30:00Z",
      "updated_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

> 422 Response

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

<h3 id="list-analytics-aggregations-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved aggregation rules with pagination|[AggregationListResponse](#schemaaggregationlistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update Analytics Aggregation

<a id="opIdupdate_aggregation_api_v1_aggregations__aggregation_id__put"></a>

`PUT /api/v1/aggregations/{aggregation_id}`

Update an existing analytics aggregation rule configuration, including thresholds, time windows, and monitoring parameters.

> Body parameter

```json
{
  "name": "daily_transactions",
  "value": "card:5m:count > 10",
  "periods": [
    5,
    30,
    60
  ]
}
```

<h3 id="update-analytics-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|
|body|body|[AggregationRequest](#schemaaggregationrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "name": "string",
  "value": "string",
  "periods": [
    0
  ],
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "company_id": "2242269",
    "name": "rule1",
    "value": "not (b == 2 and a == 2)"
  }
}
```

<h3 id="update-analytics-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Aggregation updated successfully|[AggregationResponse](#schemaaggregationresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid aggregation configuration|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Aggregation not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation error in request data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete Analytics Aggregation

<a id="opIddelete_aggregation_api_v1_aggregations__aggregation_id__delete"></a>

`DELETE /api/v1/aggregations/{aggregation_id}`

Permanently delete an analytics aggregation rule. This action cannot be undone.

<h3 id="delete-analytics-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|

> Example responses

> 422 Response

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

<h3 id="delete-analytics-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Aggregation deleted successfully|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Aggregation not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Analytics Aggregation

<a id="opIdget_aggregation_api_v1_aggregations__aggregation_id__get"></a>

`GET /api/v1/aggregations/{aggregation_id}`

Retrieve a specific analytics aggregation rule by its ID.

<h3 id="get-analytics-aggregation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|aggregation_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "name": "string",
  "value": "string",
  "periods": [
    0
  ],
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "company_id": "2242269",
    "name": "rule1",
    "value": "not (b == 2 and a == 2)"
  }
}
```

<h3 id="get-analytics-aggregation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Aggregation retrieved successfully|[AggregationResponse](#schemaaggregationresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Aggregation not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List Available Aggregation Fields

<a id="opIdlist_fields_api_v1_aggregations_fields_get"></a>

`GET /api/v1/aggregations/fields`

Get the list of available fields that can be used in analytics aggregations.

    Returns all transaction and customer fields that can be aggregated including:
    - **Transaction fields** - amount, currency, status, timestamps
    - **Customer fields** - email, phone, location, device data
    - **Payment fields** - card type, BIN, payment method
    - **Metadata fields** - Custom fields from transaction metadata

    Use these fields to build custom aggregation rules for pattern detection.

> Example responses

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="list-available-aggregation-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fields retrieved successfully|[AggregationFieldsResponse](#schemaaggregationfieldsresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Field Descriptions

<a id="opIdlist_fields_description_api_v1_aggregations_fields_description_get"></a>

`GET /api/v1/aggregations/fields/description`

Get detailed descriptions and data types for all available aggregation fields.

> Example responses

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="get-field-descriptions-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Field descriptions retrieved successfully|[AggregationFieldsResponse](#schemaaggregationfieldsresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Invalid or missing API key|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Aggregation Events

<a id="opIdget_aggregation_events_api_v1_aggregations_charges__charge_id__events_get"></a>

`GET /api/v1/aggregations/charges/{charge_id}/events`

Get analytics events triggered for a specific transaction charge.

<h3 id="get-aggregation-events-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|
|current_page|query|integer|false|Page number (1-based)|
|page_size|query|integer|false|Number of events per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {}
  ],
  "pagination": {}
}
```

<h3 id="get-aggregation-events-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|List of aggregation events for the charge|[AggregationEventListResponse](#schemaaggregationeventlistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get Aggregation Event Logs

<a id="opIdget_aggregation_events_logs_api_v1_aggregations_charges__charge_id__logs_get"></a>

`GET /api/v1/aggregations/charges/{charge_id}/logs`

Get detailed logs of analytics events for a specific transaction charge.

<h3 id="get-aggregation-event-logs-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|
|current_page|query|integer|false|Page number (1-based)|
|page_size|query|integer|false|Number of logs per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {}
  ],
  "pagination": {}
}
```

<h3 id="get-aggregation-event-logs-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Detailed logs of aggregation events for the charge|[AggregationEventLogListResponse](#schemaaggregationeventloglistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-blacklists">Blacklists</h1>

## Create blacklist entry

<a id="opIdadd_blacklist_api_v1_blacklists__post"></a>

`POST /api/v1/blacklists/`

Add a value to the blacklist for automated fraud prevention. Accepts customer emails, phone numbers, or payment card hashes. Blacklisted values will automatically trigger fraud alerts in future assessments.

> Body parameter

```json
{
  "value": "user@example.com",
  "expire_at": "2024-12-31T23:59:59Z"
}
```

<h3 id="create-blacklist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BlacklistRequest](#schemablacklistrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

> 409 Response

```json
{
  "detail": "The blacklist already exists."
}
```

> 422 Response

```json
{
  "detail": "The blacklist could not be added."
}
```

<h3 id="create-blacklist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully created blacklist entry|[BlacklistResponse](#schemablacklistresponse)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Blacklist entry already exists|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Invalid blacklist data provided|None|

<h3 id="create-blacklist-entry-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List blacklist entries

<a id="opIdlist_blacklists_api_v1_blacklists__get"></a>

`GET /api/v1/blacklists/`

Retrieve all blacklist entries with pagination. Returns customer emails, phone numbers, and payment card hashes currently blocked by fraud prevention system.

<h3 id="list-blacklist-entries-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number for pagination|
|page_size|query|integer|false|Number of entries per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "id": "bl_123456",
      "value": "fraud@suspicious.com",
      "type": "email",
      "reason": "Multiple failed transactions",
      "created_at": "2024-01-15T10:30:00Z",
      "updated_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

> 422 Response

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

<h3 id="list-blacklist-entries-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved blacklist entries with pagination|[BlacklistListResponse](#schemablacklistlistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update blacklist entry

<a id="opIdupdate_blacklist_api_v1_blacklists__blacklist_id__put"></a>

`PUT /api/v1/blacklists/{blacklist_id}`

Modify an existing blacklist entry. Updates the value (email, phone number, or card hash) and metadata while preserving the entry's fraud prevention status.

> Body parameter

```json
{
  "value": "user@example.com",
  "expire_at": "2024-12-31T23:59:59Z"
}
```

<h3 id="update-blacklist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|
|body|body|[BlacklistRequest](#schemablacklistrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

> 404 Response

```json
{
  "detail": "The blacklist does not exist."
}
```

<h3 id="update-blacklist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated blacklist entry|[BlacklistResponse](#schemablacklistresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Blacklist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="update-blacklist-entry-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete blacklist entry

<a id="opIddelete_blacklist_api_v1_blacklists__blacklist_id__delete"></a>

`DELETE /api/v1/blacklists/{blacklist_id}`

Remove a value from the blacklist. Deleted entries (email, phone number, or card hash) will no longer trigger fraud alerts in future assessments.

<h3 id="delete-blacklist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|

> Example responses

> 404 Response

```json
{
  "detail": "The blacklist does not exist."
}
```

> 422 Response

```json
{
  "detail": "The blacklist could not be deleted."
}
```

<h3 id="delete-blacklist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Blacklist entry successfully deleted|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Blacklist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unable to delete blacklist entry|None|

<h3 id="delete-blacklist-entry-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Retrieve blacklist entry

<a id="opIdget_blacklist_api_v1_blacklists__blacklist_id__get"></a>

`GET /api/v1/blacklists/{blacklist_id}`

Get details of a specific blacklist entry including its value (email, phone number, or card hash), type, and metadata.

<h3 id="retrieve-blacklist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blacklist_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

> 404 Response

```json
{
  "detail": "The blacklist does not exist."
}
```

<h3 id="retrieve-blacklist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Blacklist entry details|[BlacklistResponse](#schemablacklistresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Blacklist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="retrieve-blacklist-entry-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-whitelists">Whitelists</h1>

## Create whitelist entry

<a id="opIdadd_whitelist_api_v1_whitelists__post"></a>

`POST /api/v1/whitelists/`

Add a value to the whitelist for fraud prevention bypass. Accepts customer emails, phone numbers, or payment card hashes. Whitelisted values will automatically be excluded from fraud alerts in future assessments.

> Body parameter

```json
{
  "value": "user@example.com",
  "expire_at": "2025-12-31T23:59:59Z"
}
```

<h3 id="create-whitelist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[WhitelistRequest](#schemawhitelistrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

> 409 Response

```json
{
  "detail": "The whitelist already exists."
}
```

> 422 Response

```json
{
  "detail": "The whitelist could not be added."
}
```

<h3 id="create-whitelist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully created whitelist entry|[WhitelistResponse](#schemawhitelistresponse)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Whitelist entry already exists|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Invalid whitelist data provided|None|

<h3 id="create-whitelist-entry-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List whitelist entries

<a id="opIdfetch_whitelists_api_v1_whitelists__get"></a>

`GET /api/v1/whitelists/`

Retrieve all whitelist entries with pagination. Returns customer emails, phone numbers, and payment card hashes currently excluded from fraud prevention system.

<h3 id="list-whitelist-entries-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number for pagination|
|page_size|query|integer|false|Number of entries per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "id": "wl_123456",
      "value": "trusted@company.com",
      "type": "email",
      "reason": "VIP customer",
      "created_at": "2024-01-15T10:30:00Z",
      "updated_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

> 422 Response

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

<h3 id="list-whitelist-entries-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved whitelist entries with pagination|[WhitelistListResponse](#schemawhitelistlistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update whitelist entry

<a id="opIdupdate_whitelist_api_v1_whitelists__whitelist_id__put"></a>

`PUT /api/v1/whitelists/{whitelist_id}`

Modify an existing whitelist entry. Updates the value (email, phone number, or card hash) and metadata while preserving the entry's fraud prevention bypass status.

> Body parameter

```json
{
  "value": "user@example.com",
  "expire_at": "2025-12-31T23:59:59Z"
}
```

<h3 id="update-whitelist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|
|body|body|[WhitelistRequest](#schemawhitelistrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="update-whitelist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated whitelist entry|[WhitelistResponse](#schemawhitelistresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Whitelist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete whitelist entry

<a id="opIddelete_whitelist_api_v1_whitelists__whitelist_id__delete"></a>

`DELETE /api/v1/whitelists/{whitelist_id}`

Remove a value from the whitelist. Deleted entries (email, phone number, or card hash) will no longer be excluded from fraud alerts in future assessments.

<h3 id="delete-whitelist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|

<h3 id="delete-whitelist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Whitelist entry successfully deleted|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Whitelist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unable to delete whitelist entry|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Retrieve whitelist entry

<a id="opIdget_whitelist_api_v1_whitelists__whitelist_id__get"></a>

`GET /api/v1/whitelists/{whitelist_id}`

Get details of a specific whitelist entry including its value (email, phone number, or card hash), type, and metadata.

<h3 id="retrieve-whitelist-entry-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|whitelist_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}
```

<h3 id="retrieve-whitelist-entry-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Whitelist entry details|[WhitelistResponse](#schemawhitelistresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Whitelist entry not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-snapshots">Snapshots</h1>

## Create data snapshot

<a id="opIdcreate_snapshot_api_v1_snapshots__post"></a>

`POST /api/v1/snapshots/`

Create a backup snapshot of specified data collections. Snapshot creation runs asynchronously in the background.

> Body parameter

```json
{
  "description": "Pre-deployment snapshot",
  "collections": [
    "RULES",
    "BLACKLISTS"
  ],
  "drop_existing": false
}
```

<h3 id="create-data-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SnapshotRequest](#schemasnapshotrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "collections": [
    "string"
  ],
  "size_bytes": 0,
  "status": "string",
  "compressed": false,
  "description": "string",
  "backup_path": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  }
}
```

<h3 id="create-data-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully initiated snapshot creation|[SnapshotResponse](#schemasnapshotresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unable to create snapshot|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List snapshots

<a id="opIdlist_snapshots_api_v1_snapshots__get"></a>

`GET /api/v1/snapshots/`

Retrieve all snapshots with pagination. Returns snapshot history including creation dates, status, and collection information.

<h3 id="list-snapshots-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number for pagination|
|page_size|query|integer|false|Number of snapshots per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {}
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

<h3 id="list-snapshots-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Paginated list of snapshots|[SnapshotListResponse](#schemasnapshotlistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Retrieve snapshot details

<a id="opIdget_snapshot_api_v1_snapshots__snapshot_id__get"></a>

`GET /api/v1/snapshots/{snapshot_id}`

Get detailed information about a specific snapshot including its status, creation date, and collections included.

<h3 id="retrieve-snapshot-details-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "collections": [
    "string"
  ],
  "size_bytes": 0,
  "status": "string",
  "compressed": false,
  "description": "string",
  "backup_path": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  }
}
```

<h3 id="retrieve-snapshot-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Snapshot details and metadata|[SnapshotResponse](#schemasnapshotresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Snapshot not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Delete snapshot

<a id="opIddelete_snapshot_api_v1_snapshots__snapshot_id__delete"></a>

`DELETE /api/v1/snapshots/{snapshot_id}`

Permanently delete a snapshot and all its associated data. This action cannot be undone.

<h3 id="delete-snapshot-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

<h3 id="delete-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Snapshot successfully deleted|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Snapshot not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unable to delete snapshot|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get snapshot metadata

<a id="opIdget_snapshot_details_api_v1_snapshots__snapshot_id__metadata_get"></a>

`GET /api/v1/snapshots/{snapshot_id}/metadata`

Retrieve detailed metadata about a snapshot including collection statistics, data counts, and snapshot integrity information.

<h3 id="get-snapshot-metadata-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="get-snapshot-metadata-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Detailed snapshot metadata and statistics|[SnapshotMetadataResponse](#schemasnapshotmetadataresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Snapshot not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Restore snapshot

<a id="opIdrestore_snapshot_api_v1_snapshots__snapshot_id__restore_post"></a>

`POST /api/v1/snapshots/{snapshot_id}/restore`

Restore data from a snapshot to specified collections. Restoration runs asynchronously in the background and may overwrite existing data.

> Body parameter

```json
{
  "description": "Pre-deployment snapshot",
  "collections": [
    "RULES",
    "BLACKLISTS"
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
{
  "restore_id": "string",
  "snapshot_id": "string",
  "company_id": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "collections": [
    "string"
  ],
  "description": "",
  "status": "string",
  "drop_existing": false,
  "snapshot_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  },
  "snapshot_restore_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_restore_id": "string",
    "snapshot_id": "",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "collections": [
      "string"
    ],
    "description": "",
    "status": "string",
    "drop_existing": false,
    "snapshot_model": {
      "_id": "5eb7cf5a86d9755df3a6c593",
      "snapshot_id": "string",
      "company_id": "",
      "created_at": "2019-08-24T14:15:22Z",
      "description": "",
      "backup_path": "string",
      "database_name": "string",
      "collections": [
        "string"
      ],
      "size_bytes": 0,
      "status": "string",
      "compressed": false
    }
  }
}
```

<h3 id="restore-snapshot-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully initiated snapshot restoration|[SnapshotRestoreResponse](#schemasnapshotrestoreresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Snapshot not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unable to restore snapshot|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List restore operations

<a id="opIdlist_restore_snapshots_api_v1_snapshots__snapshot_id__restore_get"></a>

`GET /api/v1/snapshots/{snapshot_id}/restore`

Retrieve all restore operations for a specific snapshot with pagination. Shows restore history including status and timestamps.

<h3 id="list-restore-operations-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|
|current_page|query|integer|false|Page number for pagination|
|page_size|query|integer|false|Number of restore operations per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {}
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}
```

<h3 id="list-restore-operations-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Paginated list of restore operations|[SnapshotRestoreListResponse](#schemasnapshotrestorelistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get restore operation details

<a id="opIdget_restore_snapshot_api_v1_snapshots__snapshot_id__restore__snapshot_restore_id__get"></a>

`GET /api/v1/snapshots/{snapshot_id}/restore/{snapshot_restore_id}`

Retrieve detailed information about a specific restore operation including status, progress, and any errors encountered.

<h3 id="get-restore-operation-details-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|snapshot_id|path|string|true|none|
|snapshot_restore_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "restore_id": "string",
  "snapshot_id": "string",
  "company_id": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "collections": [
    "string"
  ],
  "description": "",
  "status": "string",
  "drop_existing": false,
  "snapshot_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  },
  "snapshot_restore_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_restore_id": "string",
    "snapshot_id": "",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "collections": [
      "string"
    ],
    "description": "",
    "status": "string",
    "drop_existing": false,
    "snapshot_model": {
      "_id": "5eb7cf5a86d9755df3a6c593",
      "snapshot_id": "string",
      "company_id": "",
      "created_at": "2019-08-24T14:15:22Z",
      "description": "",
      "backup_path": "string",
      "database_name": "string",
      "collections": [
        "string"
      ],
      "size_bytes": 0,
      "status": "string",
      "compressed": false
    }
  }
}
```

<h3 id="get-restore-operation-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Restore operation details and status|[SnapshotRestoreResponse](#schemasnapshotrestoreresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Restore operation not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Compare snapshots

<a id="opIdcompare_snapshots_api_v1_snapshots_compare_post"></a>

`POST /api/v1/snapshots/compare`

Compare two snapshots to identify differences in fraud detection module data, providing detailed change analysis for audit and rollback purposes.

> Body parameter

```json
{
  "baseline_snapshot_id": "snapshot_20240101_baseline",
  "current_snapshot_id": "snapshot_20240201_current"
}
```

<h3 id="compare-snapshots-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SnapshotCompareRequest](#schemasnapshotcomparerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "rules": {},
  "whitelists": {},
  "blacklists": {}
}
```

<h3 id="compare-snapshots-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Detailed comparison showing differences between snapshots|[SnapshotCompareResponse](#schemasnapshotcompareresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|One or both snapshots not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Invalid snapshot IDs or comparison parameters|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-anomalies">Anomalies</h1>

## Detect optimized anomalies

<a id="opIdpost_anomalies_tree_api_v1_anomalies_tree_post"></a>

`POST /api/v1/anomalies/tree`

Execute optimized anomaly detection using isolation forest algorithm to identify unusual patterns in transaction data efficiently.

> Body parameter

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "top": 5,
  "min_value": 10,
  "min_percentage": 5
}
```

<h3 id="detect-optimized-anomalies-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyOptimizedRequest](#schemaanomalyoptimizedrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": {},
  "params": {},
  "query": {}
}
```

<h3 id="detect-optimized-anomalies-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Detected anomalies with confidence scores and optimization metrics|[AnomalyOptimizedResult](#schemaanomalyoptimizedresult)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Invalid request parameters or malformed data|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Auto-discover anomaly patterns

<a id="opIddiscover_api_v1_anomalies_discover_post"></a>

`POST /api/v1/anomalies/discover`

Automatically discover the most important concentration patterns in your data without specifying fields in advance. Uses DataSpot's discovery algorithm.

> Body parameter

```json
{
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "max_fields": 2,
  "min_percentage": 1,
  "limit": 10
}
```

<h3 id="auto-discover-anomaly-patterns-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyDiscoverRequest](#schemaanomalydiscoverrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "total_records": 0,
  "fields": [
    {}
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {}
}
```

<h3 id="auto-discover-anomaly-patterns-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Discovered patterns and field rankings|[AnomalyDiscoverResult](#schemaanomalydiscoverresult)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Find concentration patterns

<a id="opIdfind_api_v1_anomalies_find_post"></a>

`POST /api/v1/anomalies/find`

Find where your data concentrates across specified fields using DataSpot's pattern detection. Includes configurable filtering options and depth control.

> Body parameter

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "min_percentage": 1,
  "max_depth": 2,
  "contains": "visa",
  "min_count": 10,
  "sort_by": "percentage",
  "limit": 20
}
```

<h3 id="find-concentration-patterns-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyFindRequest](#schemaanomalyfindrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {}
}
```

<h3 id="find-concentration-patterns-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Found concentration patterns in specified fields|[AnomalyFindResponse](#schemaanomalyfindresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Perform statistical analysis

<a id="opIdanalyze_api_v1_anomalies_analyze_post"></a>

`POST /api/v1/anomalies/analyze`

Conduct deep statistical analysis on data patterns using DataSpot. Provides confidence scores, statistical significance, and actionable insights for each pattern.

> Body parameter

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "min_percentage": 5
}
```

<h3 id="perform-statistical-analysis-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyAnalyzeRequest](#schemaanomalyanalyzerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {},
  "insights": {},
  "statistics": {}
}
```

<h3 id="perform-statistical-analysis-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Statistical analysis results with insights and confidence scores|[AnomalyAnalyzeResponse](#schemaanomalyanalyzeresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Compare data between time periods

<a id="opIdcompare_api_v1_anomalies_compare_post"></a>

`POST /api/v1/anomalies/compare`

Compare data patterns between current and baseline periods using DataSpot. Detects changes, new patterns, and disappeared patterns for A/B testing and trend analysis.

> Body parameter

```json
{
  "fields": [
    "payment.amount"
  ],
  "current_from_date": "2024-02-01T00:00:00Z",
  "current_to_date": "2024-02-29T23:59:59Z",
  "baseline_from_date": "2024-01-01T00:00:00Z",
  "baseline_to_date": "2024-01-31T23:59:59Z",
  "query": {
    "status": "completed"
  },
  "change_threshold": 0.1,
  "statistical_significance": true
}
```

<h3 id="compare-data-between-time-periods-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[AnomalyCompareRequest](#schemaanomalycomparerequest)|true|none|

> Example responses

> 200 Response

```json
{
  "current_records": 0,
  "baseline_records": 0,
  "fields": [
    "string"
  ],
  "changes": [
    {}
  ],
  "added_patterns": [
    {}
  ],
  "removed_patterns": [
    {}
  ],
  "statistics": {},
  "params": {},
  "query": {}
}
```

<h3 id="compare-data-between-time-periods-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Temporal comparison results with change detection|[AnomalyCompareResponse](#schemaanomalycompareresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get available analysis fields

<a id="opIdget_available_fields_api_v1_anomalies_fields_get"></a>

`GET /api/v1/anomalies/fields`

Retrieve categorized list of fields available for anomaly analysis including customer, payment, and charge fields.

> Example responses

> 200 Response

```json
{
  "customer_fields": [
    "string"
  ],
  "payment_fields": [
    "string"
  ],
  "charge_fields": [
    "string"
  ]
}
```

<h3 id="get-available-analysis-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Categorized list of available fields for analysis|[AnomalyFieldsResponse](#schemaanomalyfieldsresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-charges">Charges</h1>

## Retrieve charge details

<a id="opIdget_charge_api_v1_charges__charge_id__get"></a>

`GET /api/v1/charges/{charge_id}`

Get detailed information about a specific charge including transaction data, customer information, and assessment results.

<h3 id="retrieve-charge-details-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|charge_id|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "charge_id": "string",
  "status": "pending",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z",
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

> 404 Response

```json
{
  "detail": "The charge does not exist."
}
```

<h3 id="retrieve-charge-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Charge details with transaction and assessment data|[ChargeResponse](#schemachargeresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Charge not found|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<h3 id="retrieve-charge-details-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## List charges

<a id="opIdlist_charges_api_v1_charges__get"></a>

`GET /api/v1/charges/`

Retrieve all charges with pagination. Returns transaction history including amounts, customer data, and fraud assessment results.

<h3 id="list-charges-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|current_page|query|integer|false|Page number for pagination|
|page_size|query|integer|false|Number of charges per page|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "charge_id": "string",
      "status": "pending",
      "created_at": "2019-08-24T14:15:22Z",
      "updated_at": "2019-08-24T14:15:22Z",
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
  ],
  "pagination": {}
}
```

<h3 id="list-charges-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Paginated list of charges with transaction details|[ChargeListResponse](#schemachargelistresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

<h1 id="frauddi-api-companies">Companies</h1>

## Get execution configuration

<a id="opIdget_configuration_api_v1_companies_configuration_execution__get"></a>

`GET /api/v1/companies/configuration/execution/`

Retrieve the execution pipeline configuration for a company, including rule priorities, execution order, and stop conditions.

> Example responses

> 200 Response

```json
{
  "configuration": []
}
```

<h3 id="get-execution-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Execution configuration with prioritized rules and control settings|[ConfigurationExecutionResponse](#schemaconfigurationexecutionresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Configuration not found for this company|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update execution configuration

<a id="opIdupdate_configuration_api_v1_companies_configuration_execution__put"></a>

`PUT /api/v1/companies/configuration/execution/`

Replace the execution configuration with new rule priorities, execution order, and control settings. Maintains configuration ID while updating all items.

> Body parameter

```json
{
  "configuration": [
    {
      "enabled": true,
      "name": "Blacklist Check",
      "priority": 1,
      "stop_on_match": true,
      "type": "BLACKLISTS"
    },
    {
      "enabled": true,
      "name": "Whitelist Validation",
      "priority": 2,
      "stop_on_match": false,
      "type": "WHITELISTS"
    },
    {
      "enabled": true,
      "name": "Fraud Rules",
      "priority": 3,
      "stop_on_match": false,
      "type": "RULES"
    }
  ]
}
```

<h3 id="update-execution-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationExecutionRequest](#schemaconfigurationexecutionrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "configuration": []
}
```

<h3 id="update-execution-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Updated execution configuration with new settings applied|[ConfigurationExecutionResponse](#schemaconfigurationexecutionresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Configuration not found for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create execution configuration

<a id="opIdcreate_configuration_api_v1_companies_configuration_execution__post"></a>

`POST /api/v1/companies/configuration/execution/`

Create a new execution pipeline configuration defining rule execution order, priorities, and control flow for fraud detection.

> Body parameter

```json
{
  "configuration": [
    {
      "enabled": true,
      "name": "Blacklist Check",
      "priority": 1,
      "stop_on_match": true,
      "type": "BLACKLISTS"
    },
    {
      "enabled": true,
      "name": "Whitelist Validation",
      "priority": 2,
      "stop_on_match": false,
      "type": "WHITELISTS"
    },
    {
      "enabled": true,
      "name": "Fraud Rules",
      "priority": 3,
      "stop_on_match": false,
      "type": "RULES"
    }
  ]
}
```

<h3 id="create-execution-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationExecutionRequest](#schemaconfigurationexecutionrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "configuration": []
}
```

<h3 id="create-execution-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created execution configuration with generated IDs and applied settings|[ConfigurationExecutionResponse](#schemaconfigurationexecutionresponse)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Configuration already exists for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get decision configuration

<a id="opIdget_decision_configuration_api_v1_companies_configuration_decision__get"></a>

`GET /api/v1/companies/configuration/decision/`

Retrieve the decision-making configuration for a company, including score thresholds, risk levels, and action mappings for fraud detection outcomes.

> Example responses

> 200 Response

```json
{
  "configuration": []
}
```

<h3 id="get-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Decision configuration with score thresholds and action rules|[ConfigurationDecisionResponse](#schemaconfigurationdecisionresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Decision configuration not found for this company|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update decision configuration

<a id="opIdupdate_decision_configuration_api_v1_companies_configuration_decision__put"></a>

`PUT /api/v1/companies/configuration/decision/`

Replace the decision configuration with new score thresholds, risk levels, and action rules for fraud detection outcomes.

> Body parameter

```json
{
  "configuration": [
    {
      "description": "Accept takes precedence",
      "enabled": true,
      "name": "ACCEPT_PRIORITY"
    },
    {
      "description": "Reject takes precedence",
      "enabled": false,
      "name": "REJECT_PRIORITY"
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
{
  "configuration": []
}
```

<h3 id="update-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Updated decision configuration with new thresholds and actions|[ConfigurationDecisionResponse](#schemaconfigurationdecisionresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Decision configuration not found for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create decision configuration

<a id="opIdcreate_decision_configuration_api_v1_companies_configuration_decision__post"></a>

`POST /api/v1/companies/configuration/decision/`

Create decision-making rules defining score thresholds, risk levels, and automated actions for fraud detection results.

> Body parameter

```json
{
  "configuration": [
    {
      "description": "Accept takes precedence",
      "enabled": true,
      "name": "ACCEPT_PRIORITY"
    },
    {
      "description": "Reject takes precedence",
      "enabled": false,
      "name": "REJECT_PRIORITY"
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
{
  "configuration": []
}
```

<h3 id="create-decision-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created decision configuration with defined thresholds and actions|[ConfigurationDecisionResponse](#schemaconfigurationdecisionresponse)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Decision configuration already exists for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get ML model configuration

<a id="opIdget_model_configuration_api_v1_companies_configuration_models__get"></a>

`GET /api/v1/companies/configuration/models/`

Retrieve machine learning model configuration for a company, including model parameters, feature engineering settings, and inference thresholds.

> Example responses

> 200 Response

```json
{
  "configuration": []
}
```

<h3 id="get-ml-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|ML model configuration with parameters and inference settings|[ConfigurationModelResponse](#schemaconfigurationmodelresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|ML model configuration not found for this company|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Update ML model configuration

<a id="opIdupdate_model_configuration_api_v1_companies_configuration_models__put"></a>

`PUT /api/v1/companies/configuration/models/`

Replace the ML model configuration with new parameters, feature engineering settings, and inference thresholds for fraud detection models.

> Body parameter

```json
{
  "configuration": [
    {
      "description": "High security fraud detection",
      "enabled": true,
      "id": "model_001",
      "name": "PROTECTIVE"
    },
    {
      "description": "Balanced fraud detection",
      "enabled": false,
      "id": "model_002",
      "name": "PERMISSIVE"
    }
  ]
}
```

<h3 id="update-ml-model-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationModelRequest](#schemaconfigurationmodelrequest)|true|none|

> Example responses

> 200 Response

```json
{
  "configuration": []
}
```

<h3 id="update-ml-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Updated ML model configuration with new parameters applied|[ConfigurationModelResponse](#schemaconfigurationmodelresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|ML model configuration not found for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Create ML model configuration

<a id="opIdcreate_model_configuration_api_v1_companies_configuration_models__post"></a>

`POST /api/v1/companies/configuration/models/`

Create machine learning model configuration defining model parameters, feature engineering pipeline, and inference settings for fraud detection.

> Body parameter

```json
{
  "configuration": [
    {
      "description": "High security fraud detection",
      "enabled": true,
      "id": "model_001",
      "name": "PROTECTIVE"
    },
    {
      "description": "Balanced fraud detection",
      "enabled": false,
      "id": "model_002",
      "name": "PERMISSIVE"
    }
  ]
}
```

<h3 id="create-ml-model-configuration-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ConfigurationModelRequest](#schemaconfigurationmodelrequest)|true|none|

> Example responses

> 201 Response

```json
{
  "configuration": []
}
```

<h3 id="create-ml-model-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created ML model configuration with applied parameters|[ConfigurationModelResponse](#schemaconfigurationmodelresponse)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|ML model configuration already exists for this company|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
HTTPBearer
</aside>

## Get company details

<a id="opIdget_company_details_api_v1_companies_details_get"></a>

`GET /api/v1/companies/details`

Retrieve current company information including name, description, and legal representative details based on authentication token.

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
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Company details and configuration information|[CompanyResponse](#schemacompanyresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Company not found|None|

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
  "customer_id": "CUST_12345",
  "email": "customer@example.com",
  "phone": "+1234567890",
  "card_number": "4111111111111111",
  "merchant_id": "MERCH_001",
  "ip_addresses": [
    "192.168.1.1",
    "10.0.0.1"
  ],
  "device_ids": [
    "device_123",
    "mobile_456"
  ],
  "acceptance": 10,
  "declined": 2,
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
|customer_id|string|true|none|Unique customer identifier. Must be unique across the system.|
|email|string|true|none|Customer email address. Must be a valid email format.|
|phone|string|true|none|Customer phone number including country code. Must be a valid phone format.|
|card_number|string|true|none|Customer card number (digits only). Can be full card number (13-19 digits), BIN (6-8 digits), or last 4 digits. Should be masked or tokenized for security.|
|merchant_id|string|false|none|Merchant identifier associated with this customer. Optional field.|
|ip_addresses|[string]|false|none|List of IP addresses associated with this customer's transactions.|
|device_ids|[string]|false|none|List of device identifiers used by this customer.|
|acceptance|integer|false|none|Number of accepted transactions for this customer. Must be non-negative.|
|declined|integer|false|none|Number of declined transactions for this customer. Must be non-negative.|
|chargeback_fraud|integer|false|none|Number of fraud-related chargebacks. Must be non-negative.|
|chargeback_authorization|integer|false|none|Number of authorization-related chargebacks. Must be non-negative.|
|chargeback_processing_error|integer|false|none|Number of processing error chargebacks. Must be non-negative.|
|chargeback_customer_dispute|integer|false|none|Number of customer dispute chargebacks. Must be non-negative.|
|chargeback_non_receipt|integer|false|none|Number of non-receipt chargebacks. Must be non-negative.|
|chargeback_cancelled_recurring|integer|false|none|Number of cancelled recurring transaction chargebacks. Must be non-negative.|
|chargeback_product_not_received|integer|false|none|Number of product not received chargebacks. Must be non-negative.|
|chargeback_duplicate_processing|integer|false|none|Number of duplicate processing chargebacks. Must be non-negative.|

<h2 id="tocS_AddCustomerResponse">AddCustomerResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaddcustomerresponse"></a>
<a id="schema_AddCustomerResponse"></a>
<a id="tocSaddcustomerresponse"></a>
<a id="tocsaddcustomerresponse"></a>

```json
{
  "customer_id": "string",
  "related_customers": [
    "string"
  ],
  "shared_attributes": {
    "property1": {
      "property1": [
        "string"
      ],
      "property2": [
        "string"
      ]
    },
    "property2": {
      "property1": [
        "string"
      ],
      "property2": [
        "string"
      ]
    }
  },
  "ring_id": "string"
}

```

AddCustomerResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|customer_id|string|true|none|Customer ID|
|related_customers|[string]|true|none|List of related customer IDs|
|shared_attributes|object|true|none|Shared attributes mapping|
|» **additionalProperties**|object|false|none|none|
|»» **additionalProperties**|[string]|false|none|none|
|ring_id|string|true|none|Fraud ring identifier|

<h2 id="tocS_AggregationEventListResponse">AggregationEventListResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationeventlistresponse"></a>
<a id="schema_AggregationEventListResponse"></a>
<a id="tocSaggregationeventlistresponse"></a>
<a id="tocsaggregationeventlistresponse"></a>

```json
{
  "data": [
    {}
  ],
  "pagination": {}
}

```

AggregationEventListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|object|true|none|none|

<h2 id="tocS_AggregationEventLogListResponse">AggregationEventLogListResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationeventloglistresponse"></a>
<a id="schema_AggregationEventLogListResponse"></a>
<a id="tocSaggregationeventloglistresponse"></a>
<a id="tocsaggregationeventloglistresponse"></a>

```json
{
  "data": [
    {}
  ],
  "pagination": {}
}

```

AggregationEventLogListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|object|true|none|none|

<h2 id="tocS_AggregationFieldsResponse">AggregationFieldsResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationfieldsresponse"></a>
<a id="schema_AggregationFieldsResponse"></a>
<a id="tocSaggregationfieldsresponse"></a>
<a id="tocsaggregationfieldsresponse"></a>

```json
{
  "data": {}
}

```

AggregationFieldsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|object|true|none|none|

<h2 id="tocS_AggregationListResponse">AggregationListResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationlistresponse"></a>
<a id="schema_AggregationListResponse"></a>
<a id="tocSaggregationlistresponse"></a>
<a id="tocsaggregationlistresponse"></a>

```json
{
  "data": [
    {}
  ],
  "pagination": {}
}

```

AggregationListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|object|true|none|none|

<h2 id="tocS_AggregationRequest">AggregationRequest</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationrequest"></a>
<a id="schema_AggregationRequest"></a>
<a id="tocSaggregationrequest"></a>
<a id="tocsaggregationrequest"></a>

```json
{
  "name": "daily_transactions",
  "value": "card:5m:count > 10",
  "periods": [
    5,
    30,
    60
  ]
}

```

AggregationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|Name identifier for the aggregation. Must be unique, start with a letter, and contain only letters, numbers, underscores, and hyphens.|
|value|string|true|none|Aggregation expression containing metrics in format 'entity:period:metric'. Valid entities: card, customer, company. Valid periods: 5m, 10m, 15m, 30m, 1h, 3h, 6h, 12h, 1d. Valid metrics: count, sum, avg, successful, declined, unique_companies, unique_customers, unique_cards, unique_ips, success_rate, decline_rate, velocity, median, std, min, max, p90, p95, p99, round_ratio, shannon_entropy, company_diversity.|
|periods|[integer]|true|none|List of time periods (in minutes) for which to calculate aggregations. Valid periods: 5, 10, 15, 30, 60 (1h), 180 (3h), 360 (6h), 720 (12h), 1440 (1d). Must contain at least one period.|

<h2 id="tocS_AggregationResponse">AggregationResponse</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationresponse"></a>
<a id="schema_AggregationResponse"></a>
<a id="tocSaggregationresponse"></a>
<a id="tocsaggregationresponse"></a>

```json
{
  "id": "string",
  "name": "string",
  "value": "string",
  "periods": [
    0
  ],
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "company_id": "2242269",
    "name": "rule1",
    "value": "not (b == 2 and a == 2)"
  }
}

```

AggregationResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|name|string|true|none|none|
|value|string|true|none|none|
|periods|[integer]|true|none|none|
|created_at|string(date-time)|true|none|none|
|updated_at|string(date-time)|true|none|none|
|db_model|[AggregationRules](#schemaaggregationrules)|true|none|Represents an aggregation rule in the antifraud system.|

<h2 id="tocS_AggregationRules">AggregationRules</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationrules"></a>
<a id="schema_AggregationRules"></a>
<a id="tocSaggregationrules"></a>
<a id="tocsaggregationrules"></a>

```json
{
  "company_id": "2242269",
  "name": "rule1",
  "value": "not (b == 2 and a == 2)"
}

```

AggregationRules

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|_id|any|false|none|MongoDB document ObjectID|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[PydanticObjectId](#schemapydanticobjectid)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|aggregation_id|string|false|none|none|
|value|string|false|none|none|
|name|string|false|none|none|
|periods|[integer]|false|none|none|
|company_id|string|false|none|none|
|status|[AggregationStatus](#schemaaggregationstatus)|false|none|Aggregation status enum.|
|created_at|string(date-time)|false|none|none|
|updated_at|string(date-time)|false|none|none|
|processed_at|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string(date-time)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AggregationStatus">AggregationStatus</h2>
<!-- backwards compatibility -->
<a id="schemaaggregationstatus"></a>
<a id="schema_AggregationStatus"></a>
<a id="tocSaggregationstatus"></a>
<a id="tocsaggregationstatus"></a>

```json
"PENDING"

```

AggregationStatus

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|AggregationStatus|string|false|none|Aggregation status enum.|

#### Enumerated Values

|Property|Value|
|---|---|
|AggregationStatus|PENDING|
|AggregationStatus|ACTIVE|
|AggregationStatus|FAILED|

<h2 id="tocS_AnomalyAnalyzeRequest">AnomalyAnalyzeRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyanalyzerequest"></a>
<a id="schema_AnomalyAnalyzeRequest"></a>
<a id="tocSanomalyanalyzerequest"></a>
<a id="tocsanomalyanalyzerequest"></a>

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "min_percentage": 5
}

```

AnomalyAnalyzeRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze statistically. Must specify at least one field name from the charges collection.|
|query|any|false|none|MongoDB query filters for data retrieval. Use standard MongoDB query syntax.|

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
|from_date|any|false|none|Start date for data analysis. ISO format with timezone.|

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
|to_date|any|false|none|End date for data analysis. Must be after from_date if specified.|

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
|min_percentage|number|false|none|Minimum percentage threshold for statistical analysis. Only patterns representing at least this percentage will be analyzed in detail.|

<h2 id="tocS_AnomalyAnalyzeResponse">AnomalyAnalyzeResponse</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyanalyzeresponse"></a>
<a id="schema_AnomalyAnalyzeResponse"></a>
<a id="tocSanomalyanalyzeresponse"></a>
<a id="tocsanomalyanalyzeresponse"></a>

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {},
  "insights": {},
  "statistics": {}
}

```

AnomalyAnalyzeResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|total_records|integer|true|none|Total number of records analyzed|
|fields|[string]|true|none|Fields to analyze for patterns|
|patterns|[object]|true|none|Statistical patterns found|
|params|object|true|none|Parameters used for statistical analysis|
|query|any|false|none|Query filters that were applied|

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
|insights|object|true|none|Statistical insights and recommendations|
|statistics|object|true|none|Statistics of the analysis|

<h2 id="tocS_AnomalyCompareRequest">AnomalyCompareRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalycomparerequest"></a>
<a id="schema_AnomalyCompareRequest"></a>
<a id="tocSanomalycomparerequest"></a>
<a id="tocsanomalycomparerequest"></a>

```json
{
  "fields": [
    "payment.amount"
  ],
  "current_from_date": "2024-02-01T00:00:00Z",
  "current_to_date": "2024-02-29T23:59:59Z",
  "baseline_from_date": "2024-01-01T00:00:00Z",
  "baseline_to_date": "2024-01-31T23:59:59Z",
  "query": {
    "status": "completed"
  },
  "change_threshold": 0.1,
  "statistical_significance": true
}

```

AnomalyCompareRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to compare between periods. Must specify at least one field name from the charges collection.|
|current_from_date|string(date-time)|true|none|Start date for current period analysis. Must be before current_to_date.|
|current_to_date|string(date-time)|true|none|End date for current period analysis. Must be after current_from_date.|
|baseline_from_date|string(date-time)|true|none|Start date for baseline period analysis. Must be before baseline_to_date.|
|baseline_to_date|string(date-time)|true|none|End date for baseline period analysis. Must be after baseline_from_date.|
|query|any|false|none|MongoDB query filters applied to both periods. Use standard MongoDB query syntax.|

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
|change_threshold|number|false|none|Threshold for detecting significant changes (0.01 = 1%, 1.0 = 100%). Changes above this threshold will be highlighted.|
|statistical_significance|boolean|false|none|Include statistical significance tests in the analysis. Provides p-values and confidence intervals for detected changes.|

<h2 id="tocS_AnomalyCompareResponse">AnomalyCompareResponse</h2>
<!-- backwards compatibility -->
<a id="schemaanomalycompareresponse"></a>
<a id="schema_AnomalyCompareResponse"></a>
<a id="tocSanomalycompareresponse"></a>
<a id="tocsanomalycompareresponse"></a>

```json
{
  "current_records": 0,
  "baseline_records": 0,
  "fields": [
    "string"
  ],
  "changes": [
    {}
  ],
  "added_patterns": [
    {}
  ],
  "removed_patterns": [
    {}
  ],
  "statistics": {},
  "params": {},
  "query": {}
}

```

AnomalyCompareResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|current_records|integer|true|none|Number of records in current period|
|baseline_records|integer|true|none|Number of records in baseline period|
|fields|[string]|true|none|Fields to compare between periods|
|changes|[object]|true|none|Detected changes between periods|
|added_patterns|[object]|true|none|New patterns found in current period|
|removed_patterns|[object]|true|none|Patterns that disappeared from baseline|
|statistics|any|false|none|Statistical significance test results|

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
|params|object|true|none|Parameters used for comparison|
|query|any|false|none|Query filters that were applied|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AnomalyDiscoverRequest">AnomalyDiscoverRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalydiscoverrequest"></a>
<a id="schema_AnomalyDiscoverRequest"></a>
<a id="tocSanomalydiscoverrequest"></a>
<a id="tocsanomalydiscoverrequest"></a>

```json
{
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "max_fields": 2,
  "min_percentage": 1,
  "limit": 10
}

```

AnomalyDiscoverRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|query|any|false|none|MongoDB query filters for data retrieval. Use standard MongoDB query syntax.|

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
|from_date|any|false|none|Start date for data analysis. ISO format with timezone.|

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
|to_date|any|false|none|End date for data analysis. Must be after from_date if specified.|

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
|max_fields|integer|false|none|Maximum number of fields to analyze simultaneously. Higher values provide more detailed patterns but require more processing time.|
|min_percentage|number|false|none|Minimum percentage threshold for pattern discovery. Only patterns representing at least this percentage of data will be discovered.|
|limit|integer|false|none|Maximum number of patterns to discover. Higher limits provide more comprehensive results but slower performance.|

<h2 id="tocS_AnomalyDiscoverResult">AnomalyDiscoverResult</h2>
<!-- backwards compatibility -->
<a id="schemaanomalydiscoverresult"></a>
<a id="schema_AnomalyDiscoverResult"></a>
<a id="tocSanomalydiscoverresult"></a>
<a id="tocsanomalydiscoverresult"></a>

```json
{
  "total_records": 0,
  "fields": [
    {}
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {}
}

```

AnomalyDiscoverResult

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|total_records|integer|true|none|Total number of records analyzed|
|fields|[object]|true|none|Ranking of fields by importance and concentration potential|
|patterns|[object]|true|none|Auto-discovered concentration patterns|
|params|object|true|none|Parameters used for auto-discovery|
|query|any|false|none|Query filters that were applied|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AnomalyFieldsResponse">AnomalyFieldsResponse</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyfieldsresponse"></a>
<a id="schema_AnomalyFieldsResponse"></a>
<a id="tocSanomalyfieldsresponse"></a>
<a id="tocsanomalyfieldsresponse"></a>

```json
{
  "customer_fields": [
    "string"
  ],
  "payment_fields": [
    "string"
  ],
  "charge_fields": [
    "string"
  ]
}

```

AnomalyFieldsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|customer_fields|[string]|true|none|List of customer-related fields available for analysis|
|payment_fields|[string]|true|none|List of payment-related fields available for analysis|
|charge_fields|[string]|true|none|List of charge-related fields available for analysis|

<h2 id="tocS_AnomalyFindRequest">AnomalyFindRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyfindrequest"></a>
<a id="schema_AnomalyFindRequest"></a>
<a id="tocSanomalyfindrequest"></a>
<a id="tocsanomalyfindrequest"></a>

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "min_percentage": 1,
  "max_depth": 2,
  "contains": "visa",
  "min_count": 10,
  "sort_by": "percentage",
  "limit": 20
}

```

AnomalyFindRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze for patterns. Must specify at least one field name from the charges collection.|
|query|any|false|none|MongoDB query filters for data retrieval. Use standard MongoDB query syntax.|

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
|from_date|any|false|none|Start date for data analysis. ISO format with timezone.|

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
|to_date|any|false|none|End date for data analysis. Must be after from_date if specified.|

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
|min_percentage|number|false|none|Minimum percentage threshold for patterns. Only patterns representing at least this percentage will be included.|
|max_depth|integer|false|none|Maximum depth for pattern hierarchy. Higher depths provide more detailed analysis but require more processing.|
|contains|any|false|none|Pattern must contain this string. Use for filtering patterns by specific values.|

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
|min_count|integer|false|none|Minimum count for patterns. Only patterns with at least this many occurrences will be included.|
|sort_by|string|false|none|Sort patterns by 'percentage' (default) or 'count'. Percentage sorts by relative frequency, count by absolute occurrences.|
|limit|integer|false|none|Maximum number of patterns to return. Higher limits provide more comprehensive results.|

<h2 id="tocS_AnomalyFindResponse">AnomalyFindResponse</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyfindresponse"></a>
<a id="schema_AnomalyFindResponse"></a>
<a id="tocSanomalyfindresponse"></a>
<a id="tocsanomalyfindresponse"></a>

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": [
    {}
  ],
  "params": {},
  "query": {}
}

```

AnomalyFindResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|total_records|integer|true|none|Total number of records analyzed|
|fields|[string]|true|none|Fields to analyze for patterns|
|patterns|[object]|true|none|Found concentration patterns|
|params|object|true|none|Parameters used for pattern finding|
|query|any|false|none|Query filters that were applied|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AnomalyOptimizedRequest">AnomalyOptimizedRequest</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyoptimizedrequest"></a>
<a id="schema_AnomalyOptimizedRequest"></a>
<a id="tocSanomalyoptimizedrequest"></a>
<a id="tocsanomalyoptimizedrequest"></a>

```json
{
  "fields": [
    "payment.amount"
  ],
  "query": {
    "status": "completed"
  },
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "top": 5,
  "min_value": 10,
  "min_percentage": 5
}

```

AnomalyOptimizedRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fields|[string]|true|none|Fields to analyze for anomalies. Must specify at least one field name from the charges collection.|
|query|any|false|none|MongoDB query filters for data retrieval. Use standard MongoDB query syntax.|

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
|from_date|any|false|none|Start date for data analysis. ISO format with timezone.|

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
|to_date|any|false|none|End date for data analysis. Must be after from_date if specified.|

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
|top|integer|false|none|Number of top elements to consider in optimization. Higher values provide more detailed analysis but slower performance.|
|min_value|any|false|none|Minimum value threshold for optimization. Only patterns with at least this many occurrences will be included.|

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
|min_percentage|any|false|none|Minimum percentage threshold for optimization. Only patterns representing at least this percentage will be included.|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|integer|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AnomalyOptimizedResult">AnomalyOptimizedResult</h2>
<!-- backwards compatibility -->
<a id="schemaanomalyoptimizedresult"></a>
<a id="schema_AnomalyOptimizedResult"></a>
<a id="tocSanomalyoptimizedresult"></a>
<a id="tocsanomalyoptimizedresult"></a>

```json
{
  "total_records": 0,
  "fields": [
    "string"
  ],
  "patterns": {},
  "params": {},
  "query": {}
}

```

AnomalyOptimizedResult

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|total_records|integer|true|none|Total number of records analyzed|
|fields|[string]|true|none|Fields that were analyzed|
|patterns|object|true|none|Optimized hierarchical tree structure of anomalies|
|params|object|true|none|Parameters used in the optimizer|
|query|any|false|none|Query filters that were applied|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AssessmentDataResponse">AssessmentDataResponse</h2>
<!-- backwards compatibility -->
<a id="schemaassessmentdataresponse"></a>
<a id="schema_AssessmentDataResponse"></a>
<a id="tocSassessmentdataresponse"></a>
<a id="tocsassessmentdataresponse"></a>

```json
{
  "assessment_id": "string",
  "assessment_type": "string",
  "charge_id": "string",
  "company_id": "string",
  "decision": "string",
  "decided_by": {},
  "decision_details": {},
  "configuration": {},
  "data": {},
  "snapshot_id": "string"
}

```

AssessmentDataResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|assessment_id|string|true|none|none|
|assessment_type|string|true|none|none|
|charge_id|string|true|none|none|
|company_id|string|true|none|none|
|decision|string|true|none|none|
|decided_by|object|false|none|none|
|decision_details|object|false|none|none|
|configuration|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[any]|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|object|false|none|none|
|snapshot_id|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_AssessmentListResponse">AssessmentListResponse</h2>
<!-- backwards compatibility -->
<a id="schemaassessmentlistresponse"></a>
<a id="schema_AssessmentListResponse"></a>
<a id="tocSassessmentlistresponse"></a>
<a id="tocsassessmentlistresponse"></a>

```json
{
  "data": [],
  "pagination": {
    "current_page": 1,
    "has_next": true,
    "has_previous": false,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}

```

AssessmentListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[AssessmentResponse](#schemaassessmentresponse)]|true|none|[AssessmentResponse model.]|
|pagination|object|true|none|Pagination metadata|

<h2 id="tocS_AssessmentResponse">AssessmentResponse</h2>
<!-- backwards compatibility -->
<a id="schemaassessmentresponse"></a>
<a id="schema_AssessmentResponse"></a>
<a id="tocSassessmentresponse"></a>
<a id="tocsassessmentresponse"></a>

```json
{
  "assessment_id": "string",
  "assessment_type": "string",
  "charge_id": "string",
  "company_id": "string",
  "decision": "string",
  "decided_by": {},
  "decision_details": {},
  "configuration": {},
  "data": {},
  "snapshot_id": "string",
  "created_at": "2019-08-24T14:15:22Z"
}

```

AssessmentResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|assessment_id|string|true|none|none|
|assessment_type|string|true|none|none|
|charge_id|string|true|none|none|
|company_id|string|true|none|none|
|decision|string|true|none|none|
|decided_by|object|false|none|none|
|decision_details|object|false|none|none|
|configuration|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[any]|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|object|false|none|none|
|snapshot_id|any|false|none|none|

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
|created_at|string(date-time)|true|none|none|

<h2 id="tocS_BlacklistListResponse">BlacklistListResponse</h2>
<!-- backwards compatibility -->
<a id="schemablacklistlistresponse"></a>
<a id="schema_BlacklistListResponse"></a>
<a id="tocSblacklistlistresponse"></a>
<a id="tocsblacklistlistresponse"></a>

```json
{
  "data": [
    {
      "id": "string",
      "value": "string",
      "expire_at": "2019-08-24T14:15:22Z",
      "created_at": "2019-08-24T14:15:22Z",
      "updated_at": "2019-08-24T14:15:22Z"
    }
  ],
  "pagination": {}
}

```

BlacklistListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[BlacklistResponse](#schemablacklistresponse)]|true|none|[Pydantic model for the blacklist object.]|
|pagination|object|true|none|none|

<h2 id="tocS_BlacklistRequest">BlacklistRequest</h2>
<!-- backwards compatibility -->
<a id="schemablacklistrequest"></a>
<a id="schema_BlacklistRequest"></a>
<a id="tocSblacklistrequest"></a>
<a id="tocsblacklistrequest"></a>

```json
{
  "value": "user@example.com",
  "expire_at": "2024-12-31T23:59:59Z"
}

```

BlacklistRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|Value to be blacklisted. Accepts customer emails, phone numbers, or payment card hashes. Cannot be empty.|
|expire_at|string(date-time)|false|none|Expiration date and time for the blacklist entry. Defaults to 1 year from creation.|

<h2 id="tocS_BlacklistResponse">BlacklistResponse</h2>
<!-- backwards compatibility -->
<a id="schemablacklistresponse"></a>
<a id="schema_BlacklistResponse"></a>
<a id="tocSblacklistresponse"></a>
<a id="tocsblacklistresponse"></a>

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}

```

BlacklistResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|value|string|true|none|none|
|expire_at|string(date-time)|true|none|none|
|created_at|string(date-time)|true|none|none|
|updated_at|string(date-time)|true|none|none|

<h2 id="tocS_ChargeListResponse">ChargeListResponse</h2>
<!-- backwards compatibility -->
<a id="schemachargelistresponse"></a>
<a id="schema_ChargeListResponse"></a>
<a id="tocSchargelistresponse"></a>
<a id="tocschargelistresponse"></a>

```json
{
  "data": [
    {
      "charge_id": "string",
      "status": "pending",
      "created_at": "2019-08-24T14:15:22Z",
      "updated_at": "2019-08-24T14:15:22Z",
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
  ],
  "pagination": {}
}

```

ChargeListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[ChargeResponse](#schemachargeresponse)]|true|none|[Pydantic model for charge responses.]|
|pagination|object|true|none|none|

<h2 id="tocS_ChargeRequest">ChargeRequest</h2>
<!-- backwards compatibility -->
<a id="schemachargerequest"></a>
<a id="schema_ChargeRequest"></a>
<a id="tocSchargerequest"></a>
<a id="tocschargerequest"></a>

```json
{
  "charge_id": "ch_1234567890",
  "status": "pending",
  "customer": {
    "full_name": "John Doe",
    "phone_number": "+1234567890",
    "email": "customer@example.com",
    "ip_address": "192.168.1.1",
    "fingerprint": "fp_1234abcd5678efgh"
  },
  "payment": {
    "currency": "USD",
    "amount": 100.5,
    "fee": 2.5,
    "card_hash": "hash_1a2b3c4d5e6f",
    "card_type": "credit",
    "exp_month": "01",
    "brand": "visa",
    "bin_number": "424242",
    "cvc": "123"
  },
  "metadata": {
    "campaign_id": "summer_sale_2024",
    "checkout_steps": 3,
    "customer_tier": "premium",
    "referral_source": "google_ads",
    "session_duration": 1200
  }
}

```

ChargeRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|charge_id|string|true|none|Unique identifier for the charge transaction.|
|status|string|false|none|Current status of the charge. Must be one of: pending, completed, failed, cancelled, refunded, paid. Defaults to 'pending'.|
|customer|any|false|none|Customer information associated with this charge.|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[CustomerRequest](#schemacustomerrequest)|false|none|Pydantic model for customer data in charge requests.|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|payment|any|false|none|Payment method and transaction details.|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[PaymentRequest](#schemapaymentrequest)|false|none|Pydantic model for payment data in charge requests.|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|any|false|none|Additional metadata for the charge. Can contain any custom fields relevant to your business logic or fraud detection rules.|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_ChargeResponse">ChargeResponse</h2>
<!-- backwards compatibility -->
<a id="schemachargeresponse"></a>
<a id="schema_ChargeResponse"></a>
<a id="tocSchargeresponse"></a>
<a id="tocschargeresponse"></a>

```json
{
  "charge_id": "string",
  "status": "pending",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z",
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

ChargeResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|charge_id|string|true|none|none|
|status|string|false|none|none|
|created_at|string(date-time)|false|none|none|
|updated_at|string(date-time)|false|none|none|
|customer|[CustomerResponse](#schemacustomerresponse)|false|none|Pydantic model for customer data in charge responses.|
|payment|[PaymentResponse](#schemapaymentresponse)|false|none|Pydantic model for payment data in charge responses.|

<h2 id="tocS_ChargebackCategoryResponse">ChargebackCategoryResponse</h2>
<!-- backwards compatibility -->
<a id="schemachargebackcategoryresponse"></a>
<a id="schema_ChargebackCategoryResponse"></a>
<a id="tocSchargebackcategoryresponse"></a>
<a id="tocschargebackcategoryresponse"></a>

```json
{
  "count": 0,
  "percentage": 0,
  "subcategories": {
    "property1": {
      "count": 0,
      "percentage": 0
    },
    "property2": {
      "count": 0,
      "percentage": 0
    }
  }
}

```

ChargebackCategoryResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|count|integer|true|none|Total chargebacks count|
|percentage|number|true|none|Percentage of total transactions|
|subcategories|object|true|none|Breakdown by subcategory|
|» **additionalProperties**|[ChargebackSubcategoryResponse](#schemachargebacksubcategoryresponse)|false|none|Chargeback subcategory with count and percentage.|

<h2 id="tocS_ChargebackStatsResponse">ChargebackStatsResponse</h2>
<!-- backwards compatibility -->
<a id="schemachargebackstatsresponse"></a>
<a id="schema_ChargebackStatsResponse"></a>
<a id="tocSchargebackstatsresponse"></a>
<a id="tocschargebackstatsresponse"></a>

```json
{
  "total": 0,
  "fraud": 0,
  "authorization": 0,
  "processing_error": 0,
  "customer_dispute": 0,
  "non_receipt": 0,
  "cancelled_recurring": 0,
  "product_issues": 0,
  "duplicate_processing": 0
}

```

ChargebackStatsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|total|integer|true|none|Total chargebacks|
|fraud|integer|true|none|Fraud chargebacks|
|authorization|integer|true|none|Authorization chargebacks|
|processing_error|integer|true|none|Processing error chargebacks|
|customer_dispute|integer|true|none|Customer dispute chargebacks|
|non_receipt|integer|true|none|Non-receipt chargebacks|
|cancelled_recurring|integer|true|none|Cancelled recurring chargebacks|
|product_issues|integer|true|none|Product issues chargebacks|
|duplicate_processing|integer|true|none|Duplicate processing chargebacks|

<h2 id="tocS_ChargebackSubcategoryResponse">ChargebackSubcategoryResponse</h2>
<!-- backwards compatibility -->
<a id="schemachargebacksubcategoryresponse"></a>
<a id="schema_ChargebackSubcategoryResponse"></a>
<a id="tocSchargebacksubcategoryresponse"></a>
<a id="tocschargebacksubcategoryresponse"></a>

```json
{
  "count": 0,
  "percentage": 0
}

```

ChargebackSubcategoryResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|count|integer|true|none|Chargeback count|
|percentage|number|true|none|Percentage of total chargebacks|

<h2 id="tocS_ChargesApplied">ChargesApplied</h2>
<!-- backwards compatibility -->
<a id="schemachargesapplied"></a>
<a id="schema_ChargesApplied"></a>
<a id="tocSchargesapplied"></a>
<a id="tocschargesapplied"></a>

```json
{
  "applied": 0,
  "ids": [
    "string"
  ]
}

```

ChargesApplied

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|applied|integer|true|none|Number of charges this rule applied to|
|ids|[string]|false|none|List of charge IDs (populated if include_charge_ids=True)|

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
  "name": "ACCEPT_PRIORITY",
  "description": "Use when fraud detection is high priority",
  "enabled": true
}

```

ConfigurationDecisionItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|Decision strategy name. Must be one of: ACCEPT_PRIORITY (accept takes precedence), REJECT_PRIORITY (reject takes precedence), or MAJORITY_RULE (majority vote decides).|
|description|any|false|none|Optional description explaining when and how this decision strategy should be used.|

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
|enabled|boolean|false|none|Whether this decision strategy is currently active. Only one strategy can be enabled at a time.|

<h2 id="tocS_ConfigurationDecisionItemResponse">ConfigurationDecisionItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationdecisionitemresponse"></a>
<a id="schema_ConfigurationDecisionItemResponse"></a>
<a id="tocSconfigurationdecisionitemresponse"></a>
<a id="tocsconfigurationdecisionitemresponse"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "enabled": true
}

```

ConfigurationDecisionItemResponse

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
      "description": "Accept takes precedence",
      "enabled": true,
      "name": "ACCEPT_PRIORITY"
    },
    {
      "description": "Reject takes precedence",
      "enabled": false,
      "name": "REJECT_PRIORITY"
    }
  ]
}

```

ConfigurationDecisionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationDecisionItemRequest](#schemaconfigurationdecisionitemrequest)]|true|none|List of decision strategies configuration. Must contain at least one strategy and exactly one must be enabled. Maximum 3 strategies allowed.|

<h2 id="tocS_ConfigurationDecisionResponse">ConfigurationDecisionResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationdecisionresponse"></a>
<a id="schema_ConfigurationDecisionResponse"></a>
<a id="tocSconfigurationdecisionresponse"></a>
<a id="tocsconfigurationdecisionresponse"></a>

```json
{
  "configuration": []
}

```

ConfigurationDecisionResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationDecisionItemResponse](#schemaconfigurationdecisionitemresponse)]|false|none|[Response model for a decision strategy item.]|

<h2 id="tocS_ConfigurationExecutionItemResponse">ConfigurationExecutionItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationexecutionitemresponse"></a>
<a id="schema_ConfigurationExecutionItemResponse"></a>
<a id="tocSconfigurationexecutionitemresponse"></a>
<a id="tocsconfigurationexecutionitemresponse"></a>

```json
{
  "config_item_id": "string",
  "priority": 0,
  "name": "string",
  "enabled": true,
  "stop_on_match": false,
  "type": "string",
  "description": "string",
  "configuration_id": "string"
}

```

ConfigurationExecutionItemResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|config_item_id|string|true|none|none|
|priority|integer|true|none|none|
|name|string|true|none|none|
|enabled|boolean|false|none|none|
|stop_on_match|boolean|false|none|none|
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
|configuration_id|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

<h2 id="tocS_ConfigurationExecutionRequest">ConfigurationExecutionRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationexecutionrequest"></a>
<a id="schema_ConfigurationExecutionRequest"></a>
<a id="tocSconfigurationexecutionrequest"></a>
<a id="tocsconfigurationexecutionrequest"></a>

```json
{
  "configuration": [
    {
      "enabled": true,
      "name": "Blacklist Check",
      "priority": 1,
      "stop_on_match": true,
      "type": "BLACKLISTS"
    },
    {
      "enabled": true,
      "name": "Whitelist Validation",
      "priority": 2,
      "stop_on_match": false,
      "type": "WHITELISTS"
    },
    {
      "enabled": true,
      "name": "Fraud Rules",
      "priority": 3,
      "stop_on_match": false,
      "type": "RULES"
    }
  ]
}

```

ConfigurationExecutionRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationItemRequest](#schemaconfigurationitemrequest)]|true|none|List of execution configuration items ordered by priority. Each item must have a unique priority and name. Maximum 20 items allowed for performance.|

<h2 id="tocS_ConfigurationExecutionResponse">ConfigurationExecutionResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationexecutionresponse"></a>
<a id="schema_ConfigurationExecutionResponse"></a>
<a id="tocSconfigurationexecutionresponse"></a>
<a id="tocsconfigurationexecutionresponse"></a>

```json
{
  "configuration": []
}

```

ConfigurationExecutionResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationExecutionItemResponse](#schemaconfigurationexecutionitemresponse)]|false|none|[Response model for a configuration item.]|

<h2 id="tocS_ConfigurationItemRequest">ConfigurationItemRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationitemrequest"></a>
<a id="schema_ConfigurationItemRequest"></a>
<a id="tocSconfigurationitemrequest"></a>
<a id="tocsconfigurationitemrequest"></a>

```json
{
  "priority": 1,
  "name": "High Risk Blacklist Check",
  "type": "BLACKLISTS",
  "description": "Checks customer email against known fraud database",
  "enabled": true,
  "stop_on_match": false
}

```

ConfigurationItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|priority|integer|true|none|Execution priority order. Lower numbers execute first. Must be unique across all items in the configuration.|
|name|string|true|none|Descriptive name for this configuration item. Must be unique and descriptive.|
|type|string|true|none|Type of fraud detection component to execute. Must be one of: BLACKLISTS (block known bad actors), WHITELISTS (allow trusted entities), RULES (custom business logic).|
|description|any|false|none|Optional detailed description of what this configuration item does and when it should be used.|

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
|enabled|boolean|false|none|Whether this configuration item is active. Disabled items are skipped during execution.|
|stop_on_match|boolean|false|none|Whether to stop processing remaining items if this one matches/triggers. Use for high-confidence blocking rules.|

<h2 id="tocS_ConfigurationModelItemRequest">ConfigurationModelItemRequest</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationmodelitemrequest"></a>
<a id="schema_ConfigurationModelItemRequest"></a>
<a id="tocSconfigurationmodelitemrequest"></a>
<a id="tocsconfigurationmodelitemrequest"></a>

```json
{
  "id": "model_001",
  "name": "PROTECTIVE",
  "description": "High precision fraud detection with minimal false positives",
  "enabled": true
}

```

ConfigurationModelItemRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|Unique identifier for the ML model configuration. Must be unique across all model configurations.|
|name|string|true|none|ML model strategy name. PROTECTIVE (high security, low false positives), PERMISSIVE (balanced approach), OPTIMIZED (maximum performance, may have more false positives).|
|description|any|false|none|Optional description explaining the model's behavior, use cases, and expected performance characteristics.|

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
|enabled|boolean|false|none|Whether this ML model configuration is currently active and available for use.|

<h2 id="tocS_ConfigurationModelItemResponse">ConfigurationModelItemResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationmodelitemresponse"></a>
<a id="schema_ConfigurationModelItemResponse"></a>
<a id="tocSconfigurationmodelitemresponse"></a>
<a id="tocsconfigurationmodelitemresponse"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "enabled": true,
  "configuration_id": "string"
}

```

ConfigurationModelItemResponse

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
|configuration_id|any|false|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

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
      "description": "High security fraud detection",
      "enabled": true,
      "id": "model_001",
      "name": "PROTECTIVE"
    },
    {
      "description": "Balanced fraud detection",
      "enabled": false,
      "id": "model_002",
      "name": "PERMISSIVE"
    }
  ]
}

```

ConfigurationModelRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationModelItemRequest](#schemaconfigurationmodelitemrequest)]|true|none|List of ML model configurations. Each configuration must have unique ID and name. Maximum 10 configurations allowed.|

<h2 id="tocS_ConfigurationModelResponse">ConfigurationModelResponse</h2>
<!-- backwards compatibility -->
<a id="schemaconfigurationmodelresponse"></a>
<a id="schema_ConfigurationModelResponse"></a>
<a id="tocSconfigurationmodelresponse"></a>
<a id="tocsconfigurationmodelresponse"></a>

```json
{
  "configuration": []
}

```

ConfigurationModelResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|configuration|[[ConfigurationModelItemResponse](#schemaconfigurationmodelitemresponse)]|false|none|[Response model for a ML model configuration item.]|

<h2 id="tocS_CustomerRequest">CustomerRequest</h2>
<!-- backwards compatibility -->
<a id="schemacustomerrequest"></a>
<a id="schema_CustomerRequest"></a>
<a id="tocScustomerrequest"></a>
<a id="tocscustomerrequest"></a>

```json
{
  "full_name": "John Doe",
  "phone_number": "+1234567890",
  "email": "customer@example.com",
  "ip_address": "192.168.1.1",
  "fingerprint": "fp_1234abcd5678efgh"
}

```

CustomerRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|full_name|string|true|none|Full name of the customer making the transaction.|
|phone_number|string|true|none|Customer's phone number including country code. Must be a valid phone format.|
|email|string|true|none|Customer's email address. Must be a valid email format.|
|ip_address|string|true|none|Customer's IP address (IPv4 or IPv6 format). Accepts standard IP formats.|
|fingerprint|string|true|none|Unique device/browser fingerprint for fraud detection.|

<h2 id="tocS_CustomerResponse">CustomerResponse</h2>
<!-- backwards compatibility -->
<a id="schemacustomerresponse"></a>
<a id="schema_CustomerResponse"></a>
<a id="tocScustomerresponse"></a>
<a id="tocscustomerresponse"></a>

```json
{
  "full_name": "string",
  "phone_number": "string",
  "email": "string",
  "ip_address": "string",
  "fingerprint": "string"
}

```

CustomerResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|full_name|string|true|none|none|
|phone_number|string|true|none|none|
|email|string|true|none|none|
|ip_address|string|true|none|none|
|fingerprint|string|true|none|none|

<h2 id="tocS_CustomerStatsResponse">CustomerStatsResponse</h2>
<!-- backwards compatibility -->
<a id="schemacustomerstatsresponse"></a>
<a id="schema_CustomerStatsResponse"></a>
<a id="tocScustomerstatsresponse"></a>
<a id="tocscustomerstatsresponse"></a>

```json
{
  "customer_id": "string",
  "email": "string",
  "phone": "string",
  "card_number": "string",
  "created_at": "string",
  "ip_addresses": [
    "string"
  ],
  "device_ids": [
    "string"
  ],
  "merchant_id": "",
  "acceptance": 0,
  "declined": 0,
  "chargebacks": {
    "total": 0,
    "fraud": 0,
    "authorization": 0,
    "processing_error": 0,
    "customer_dispute": 0,
    "non_receipt": 0,
    "cancelled_recurring": 0,
    "product_issues": 0,
    "duplicate_processing": 0
  }
}

```

CustomerStatsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|customer_id|string|true|none|Customer ID|
|email|string|true|none|Customer email address|
|phone|string|true|none|Customer phone number|
|card_number|string|true|none|Customer card number (last 4 digits)|
|created_at|string|true|none|Customer creation timestamp|
|ip_addresses|[string]|false|none|List of IP addresses used|
|device_ids|[string]|false|none|List of device identifiers used|
|merchant_id|string|false|none|Merchant identifier|
|acceptance|integer|true|none|Accepted transactions|
|declined|integer|true|none|Declined transactions|
|chargebacks|[ChargebackStatsResponse](#schemachargebackstatsresponse)|true|none|Chargeback breakdown|

<h2 id="tocS_GraphDataResponse">GraphDataResponse</h2>
<!-- backwards compatibility -->
<a id="schemagraphdataresponse"></a>
<a id="schema_GraphDataResponse"></a>
<a id="tocSgraphdataresponse"></a>
<a id="tocsgraphdataresponse"></a>

```json
{
  "nodes": [
    {
      "id": "string",
      "label": "string",
      "merchant_id": "string",
      "acceptance": 0,
      "declined": 0,
      "total_chargebacks": 0
    }
  ],
  "edges": [
    {
      "from": "string",
      "to": "string",
      "label": "string",
      "value": "string",
      "type": "string"
    }
  ],
  "ring_id": "string",
  "total_nodes": 0
}

```

GraphDataResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|nodes|[[GraphNodeResponse](#schemagraphnoderesponse)]|true|none|List of graph nodes|
|edges|[[GraphEdgeResponse](#schemagraphedgeresponse)]|true|none|List of graph edges|
|ring_id|string|true|none|Fraud ring identifier|
|total_nodes|integer|true|none|Total number of nodes|

<h2 id="tocS_GraphEdgeResponse">GraphEdgeResponse</h2>
<!-- backwards compatibility -->
<a id="schemagraphedgeresponse"></a>
<a id="schema_GraphEdgeResponse"></a>
<a id="tocSgraphedgeresponse"></a>
<a id="tocsgraphedgeresponse"></a>

```json
{
  "from": "string",
  "to": "string",
  "label": "string",
  "value": "string",
  "type": "string"
}

```

GraphEdgeResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from|string|true|none|Source customer ID|
|to|string|true|none|Target customer ID|
|label|string|true|none|Relationship description|
|value|string|true|none|Specific value(s) of shared attribute(s)|
|type|string|true|none|Attribute type (email, phone, card, etc.)|

<h2 id="tocS_GraphNodeResponse">GraphNodeResponse</h2>
<!-- backwards compatibility -->
<a id="schemagraphnoderesponse"></a>
<a id="schema_GraphNodeResponse"></a>
<a id="tocSgraphnoderesponse"></a>
<a id="tocsgraphnoderesponse"></a>

```json
{
  "id": "string",
  "label": "string",
  "merchant_id": "string",
  "acceptance": 0,
  "declined": 0,
  "total_chargebacks": 0
}

```

GraphNodeResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|Customer ID|
|label|string|true|none|Display label|
|merchant_id|string|true|none|Merchant identifier|
|acceptance|integer|true|none|Accepted transactions count|
|declined|integer|true|none|Declined transactions count|
|total_chargebacks|integer|true|none|Total chargebacks count|

<h2 id="tocS_GraphStatsResponse">GraphStatsResponse</h2>
<!-- backwards compatibility -->
<a id="schemagraphstatsresponse"></a>
<a id="schema_GraphStatsResponse"></a>
<a id="tocSgraphstatsresponse"></a>
<a id="tocsgraphstatsresponse"></a>

```json
{
  "relation_id": "string",
  "customer_id": "string",
  "customer_details": {
    "customer_id": "string",
    "email": "string",
    "phone": "string",
    "card_number": "string",
    "created_at": "string",
    "ip_addresses": [
      "string"
    ],
    "device_ids": [
      "string"
    ],
    "merchant_id": "",
    "acceptance": 0,
    "declined": 0,
    "chargebacks": {
      "total": 0,
      "fraud": 0,
      "authorization": 0,
      "processing_error": 0,
      "customer_dispute": 0,
      "non_receipt": 0,
      "cancelled_recurring": 0,
      "product_issues": 0,
      "duplicate_processing": 0
    }
  },
  "related_customers": [
    "string"
  ],
  "related_customers_details": [
    {
      "customer_id": "string",
      "email": "string",
      "phone": "string",
      "card_number": "string",
      "created_at": "string",
      "ip_addresses": [
        "string"
      ],
      "device_ids": [
        "string"
      ],
      "merchant_id": "",
      "acceptance": 0,
      "declined": 0,
      "chargebacks": {
        "total": 0,
        "fraud": 0,
        "authorization": 0,
        "processing_error": 0,
        "customer_dispute": 0,
        "non_receipt": 0,
        "cancelled_recurring": 0,
        "product_issues": 0,
        "duplicate_processing": 0
      }
    }
  ],
  "ring_stats": {
    "acceptance": {
      "count": 0,
      "percentage": 0
    },
    "declined": {
      "count": 0,
      "percentage": 0
    },
    "chargebacks": {
      "count": 0,
      "percentage": 0,
      "subcategories": {
        "property1": {
          "count": 0,
          "percentage": 0
        },
        "property2": {
          "count": 0,
          "percentage": 0
        }
      }
    },
    "total_transactions": 0
  },
  "ring_id": "string",
  "total_in_ring": 0
}

```

GraphStatsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|relation_id|string|true|none|Unique relation identifier|
|customer_id|string|true|none|Requested customer ID|
|customer_details|[CustomerStatsResponse](#schemacustomerstatsresponse)|true|none|Complete profile and statistics of the requested customer|
|related_customers|[string]|true|none|List of related customer IDs|
|related_customers_details|[[CustomerStatsResponse](#schemacustomerstatsresponse)]|true|none|Individual customer statistics|
|ring_stats|[RingStatsResponse](#schemaringstatsresponse)|true|none|Aggregated ring statistics|
|ring_id|string|true|none|Fraud ring identifier|
|total_in_ring|integer|true|none|Total customers in ring|

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

<h2 id="tocS_ImpactStats">ImpactStats</h2>
<!-- backwards compatibility -->
<a id="schemaimpactstats"></a>
<a id="schema_ImpactStats"></a>
<a id="tocSimpactstats"></a>
<a id="tocsimpactstats"></a>

```json
{
  "acceptance_change": 0,
  "acceptance_change_percentage": 0,
  "declined_change": 0,
  "declined_change_percentage": 0
}

```

ImpactStats

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|acceptance_change|integer|true|none|Change in accepted charges count|
|acceptance_change_percentage|number|true|none|Percentage change in acceptance rate|
|declined_change|integer|true|none|Change in declined charges count|
|declined_change_percentage|number|true|none|Percentage change in decline rate|

<h2 id="tocS_PaginationMetadata">PaginationMetadata</h2>
<!-- backwards compatibility -->
<a id="schemapaginationmetadata"></a>
<a id="schema_PaginationMetadata"></a>
<a id="tocSpaginationmetadata"></a>
<a id="tocspaginationmetadata"></a>

```json
{
  "current_page": 1,
  "has_next": false,
  "has_previous": true,
  "last_page": 1,
  "next_page": 2,
  "page_size": 20
}

```

PaginationMetadata

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|has_previous|boolean|true|none|Whether there is a previous page available|
|has_next|boolean|true|none|Whether there is a next page available|
|last_page|integer|true|none|The last page number (previous page)|
|current_page|integer|true|none|The current page number|
|next_page|integer|true|none|The next page number|
|page_size|integer|true|none|Number of items per page|

<h2 id="tocS_PaymentRequest">PaymentRequest</h2>
<!-- backwards compatibility -->
<a id="schemapaymentrequest"></a>
<a id="schema_PaymentRequest"></a>
<a id="tocSpaymentrequest"></a>
<a id="tocspaymentrequest"></a>

```json
{
  "currency": "USD",
  "amount": 100.5,
  "fee": 2.5,
  "card_hash": "hash_1a2b3c4d5e6f",
  "card_type": "credit",
  "exp_month": "01",
  "brand": "visa",
  "bin_number": "424242",
  "cvc": "123"
}

```

PaymentRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|currency|string|false|none|ISO 4217 currency code (3 uppercase letters). Defaults to USD.|
|amount|number|true|none|Transaction amount. Must be positive and not exceed 999,999.99.|
|fee|number|true|none|Processing fee amount. Must be non-negative.|
|card_hash|string|true|none|Hashed card number for security. Must not contain actual card number.|
|card_type|string|true|none|Type of card used. Must be either 'credit' or 'debit'.|
|exp_month|string|true|none|Card expiration month in MM format (01-12).|
|brand|string|true|none|Card brand/network. Must be one of the supported brands.|
|bin_number|string|true|none|Bank Identification Number (BIN) from the card. Can be 1 to 10 digits.|
|cvc|string|true|none|Card Verification Code (3-4 digits). Should be encrypted/hashed.|

<h2 id="tocS_PaymentResponse">PaymentResponse</h2>
<!-- backwards compatibility -->
<a id="schemapaymentresponse"></a>
<a id="schema_PaymentResponse"></a>
<a id="tocSpaymentresponse"></a>
<a id="tocspaymentresponse"></a>

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

PaymentResponse

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

<h2 id="tocS_PydanticObjectId">PydanticObjectId</h2>
<!-- backwards compatibility -->
<a id="schemapydanticobjectid"></a>
<a id="schema_PydanticObjectId"></a>
<a id="tocSpydanticobjectid"></a>
<a id="tocspydanticobjectid"></a>

```json
"5eb7cf5a86d9755df3a6c593"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

<h2 id="tocS_RingStatsResponse">RingStatsResponse</h2>
<!-- backwards compatibility -->
<a id="schemaringstatsresponse"></a>
<a id="schema_RingStatsResponse"></a>
<a id="tocSringstatsresponse"></a>
<a id="tocsringstatsresponse"></a>

```json
{
  "acceptance": {
    "count": 0,
    "percentage": 0
  },
  "declined": {
    "count": 0,
    "percentage": 0
  },
  "chargebacks": {
    "count": 0,
    "percentage": 0,
    "subcategories": {
      "property1": {
        "count": 0,
        "percentage": 0
      },
      "property2": {
        "count": 0,
        "percentage": 0
      }
    }
  },
  "total_transactions": 0
}

```

RingStatsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|acceptance|[TransactionStatsResponse](#schematransactionstatsresponse)|true|none|Acceptance statistics|
|declined|[TransactionStatsResponse](#schematransactionstatsresponse)|true|none|Declined statistics|
|chargebacks|[ChargebackCategoryResponse](#schemachargebackcategoryresponse)|true|none|Chargeback statistics|
|total_transactions|integer|true|none|Total transactions in ring|

<h2 id="tocS_RuleApplicationStats">RuleApplicationStats</h2>
<!-- backwards compatibility -->
<a id="schemaruleapplicationstats"></a>
<a id="schema_RuleApplicationStats"></a>
<a id="tocSruleapplicationstats"></a>
<a id="tocsruleapplicationstats"></a>

```json
{
  "rule": {},
  "charges": {
    "applied": 0,
    "ids": [
      "string"
    ]
  }
}

```

RuleApplicationStats

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rule|object|true|none|Rule information|
|charges|[ChargesApplied](#schemachargesapplied)|true|none|Charges application details|

<h2 id="tocS_RuleListResponse">RuleListResponse</h2>
<!-- backwards compatibility -->
<a id="schemarulelistresponse"></a>
<a id="schema_RuleListResponse"></a>
<a id="tocSrulelistresponse"></a>
<a id="tocsrulelistresponse"></a>

```json
{
  "data": [],
  "pagination": {
    "current_page": 1,
    "has_next": true,
    "has_previous": false,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}

```

RuleListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|object|true|none|Pagination metadata|

<h2 id="tocS_RuleRequest">RuleRequest</h2>
<!-- backwards compatibility -->
<a id="schemarulerequest"></a>
<a id="schema_RuleRequest"></a>
<a id="tocSrulerequest"></a>
<a id="tocsrulerequest"></a>

```json
{
  "value": "payment.amount > 1000 and customer.email.contains('@gmail.com')",
  "decision": "ACCEPT",
  "expire_at": "2024-12-31T23:59:59Z"
}

```

RuleRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|Rule expression using boolean logic operators (and, or, not) and comparison operators (==, !=, <, >, <=, >=). Can reference charge fields like payment.amount, customer.email, status, or aggregation metrics like card:5m:count. Cannot be empty.|
|decision|string|true|none|Decision action when rule matches. Must be either ACCEPT or REJECT in uppercase.|
|expire_at|string(date-time)|false|none|Expiration date and time for the rule. Defaults to 1 year from creation.|

<h2 id="tocS_RuleResponse">RuleResponse</h2>
<!-- backwards compatibility -->
<a id="schemaruleresponse"></a>
<a id="schema_RuleResponse"></a>
<a id="tocSruleresponse"></a>
<a id="tocsruleresponse"></a>

```json
{
  "id": "string",
  "value": "string",
  "decision": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}

```

RuleResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|value|string|true|none|none|
|decision|string|true|none|none|
|expire_at|string(date-time)|true|none|none|
|created_at|string(date-time)|true|none|none|
|updated_at|string(date-time)|true|none|none|

<h2 id="tocS_SimulationRequest">SimulationRequest</h2>
<!-- backwards compatibility -->
<a id="schemasimulationrequest"></a>
<a id="schema_SimulationRequest"></a>
<a id="tocSsimulationrequest"></a>
<a id="tocssimulationrequest"></a>

```json
{
  "from_date": "2024-01-01T00:00:00Z",
  "to_date": "2024-01-31T23:59:59Z",
  "rules": [
    {
      "decision": "REJECT",
      "expire_at": "2024-12-31T23:59:59Z",
      "value": "amount > 500"
    }
  ],
  "include_charge_ids": false
}

```

SimulationRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|from_date|string(date-time)|true|none|Start date for the simulation period. Must be before to_date.|
|to_date|string(date-time)|true|none|End date for the simulation period. Must be after from_date.|
|rules|[[RuleRequest](#schemarulerequest)]|true|none|List of rules to simulate. Must contain at least one rule.|
|include_charge_ids|boolean|false|none|Whether to include individual charge IDs in rule application results. Default is False for performance.|

<h2 id="tocS_SimulationResponse">SimulationResponse</h2>
<!-- backwards compatibility -->
<a id="schemasimulationresponse"></a>
<a id="schema_SimulationResponse"></a>
<a id="tocSsimulationresponse"></a>
<a id="tocssimulationresponse"></a>

```json
{
  "baseline": {},
  "current": {},
  "impact": {
    "acceptance_change": 0,
    "acceptance_change_percentage": 0,
    "declined_change": 0,
    "declined_change_percentage": 0
  },
  "errors": [],
  "total_charges_analyzed": 0,
  "total_rules_evaluated": 0,
  "rule_applications": []
}

```

SimulationResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|baseline|object|true|none|Statistics for current rules|
|current|object|true|none|Statistics for current + new rules|
|impact|[ImpactStats](#schemaimpactstats)|true|none|Impact analysis of new rules|
|errors|[object]|false|none|Validation errors for new rules|
|total_charges_analyzed|integer|true|none|Total number of charges analyzed|
|total_rules_evaluated|integer|true|none|Total number of rules evaluated|
|rule_applications|[[RuleApplicationStats](#schemaruleapplicationstats)]|false|none|Rules and their application counts|

<h2 id="tocS_Snapshot">Snapshot</h2>
<!-- backwards compatibility -->
<a id="schemasnapshot"></a>
<a id="schema_Snapshot"></a>
<a id="tocSsnapshot"></a>
<a id="tocssnapshot"></a>

```json
{
  "_id": "5eb7cf5a86d9755df3a6c593",
  "snapshot_id": "string",
  "company_id": "",
  "created_at": "2019-08-24T14:15:22Z",
  "description": "",
  "backup_path": "string",
  "database_name": "string",
  "collections": [
    "string"
  ],
  "size_bytes": 0,
  "status": "string",
  "compressed": false
}

```

Snapshot

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|_id|any|false|none|MongoDB document ObjectID|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[PydanticObjectId](#schemapydanticobjectid)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|snapshot_id|string|false|none|none|
|company_id|string|false|none|none|
|created_at|string(date-time)|false|none|none|
|description|string|false|none|none|
|backup_path|string|true|none|none|
|database_name|string|true|none|none|
|collections|[string]|true|none|none|
|size_bytes|any|false|none|none|

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
|status|any|false|none|none|

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
|compressed|boolean|false|none|none|

<h2 id="tocS_SnapshotCompareRequest">SnapshotCompareRequest</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotcomparerequest"></a>
<a id="schema_SnapshotCompareRequest"></a>
<a id="tocSsnapshotcomparerequest"></a>
<a id="tocssnapshotcomparerequest"></a>

```json
{
  "baseline_snapshot_id": "snapshot_20240101_baseline",
  "current_snapshot_id": "snapshot_20240201_current"
}

```

SnapshotCompareRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|baseline_snapshot_id|string|true|none|ID of the baseline snapshot to compare against. This is the reference point for comparison.|
|current_snapshot_id|string|true|none|ID of the current snapshot to compare. This will be compared against the baseline.|

<h2 id="tocS_SnapshotCompareResponse">SnapshotCompareResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotcompareresponse"></a>
<a id="schema_SnapshotCompareResponse"></a>
<a id="tocSsnapshotcompareresponse"></a>
<a id="tocssnapshotcompareresponse"></a>

```json
{
  "rules": {},
  "whitelists": {},
  "blacklists": {}
}

```

SnapshotCompareResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rules|object|false|none|none|
|whitelists|object|false|none|none|
|blacklists|object|false|none|none|

<h2 id="tocS_SnapshotListResponse">SnapshotListResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotlistresponse"></a>
<a id="schema_SnapshotListResponse"></a>
<a id="tocSsnapshotlistresponse"></a>
<a id="tocssnapshotlistresponse"></a>

```json
{
  "data": [
    {}
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}

```

SnapshotListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|[PaginationMetadata](#schemapaginationmetadata)|true|none|Pagination metadata model for list responses.|

<h2 id="tocS_SnapshotMetadataResponse">SnapshotMetadataResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotmetadataresponse"></a>
<a id="schema_SnapshotMetadataResponse"></a>
<a id="tocSsnapshotmetadataresponse"></a>
<a id="tocssnapshotmetadataresponse"></a>

```json
{
  "data": {}
}

```

SnapshotMetadataResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|object|true|none|none|

<h2 id="tocS_SnapshotRequest">SnapshotRequest</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotrequest"></a>
<a id="schema_SnapshotRequest"></a>
<a id="tocSsnapshotrequest"></a>
<a id="tocssnapshotrequest"></a>

```json
{
  "description": "Pre-deployment snapshot",
  "collections": [
    "RULES",
    "BLACKLISTS"
  ],
  "drop_existing": false
}

```

SnapshotRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|description|string|false|none|Optional description for the snapshot to help identify its purpose.|
|collections|[string]|true|none|List of fraud detection modules to include in the snapshot. Available modules: RULES, BLACKLISTS, WHITELISTS, ASSESSMENTS, AGGREGATIONS, ANOMALIES, SCORES.|
|drop_existing|boolean|false|none|Whether to drop existing module data before restoring. Use with caution as this is destructive.|

<h2 id="tocS_SnapshotResponse">SnapshotResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotresponse"></a>
<a id="schema_SnapshotResponse"></a>
<a id="tocSsnapshotresponse"></a>
<a id="tocssnapshotresponse"></a>

```json
{
  "id": "string",
  "collections": [
    "string"
  ],
  "size_bytes": 0,
  "status": "string",
  "compressed": false,
  "description": "string",
  "backup_path": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "db_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  }
}

```

SnapshotResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|collections|[string]|true|none|none|
|size_bytes|any|false|none|none|

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
|status|any|false|none|none|

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
|compressed|boolean|false|none|none|
|description|string|true|none|none|
|backup_path|string|true|none|none|
|created_at|string(date-time)|true|none|none|
|db_model|[Snapshot](#schemasnapshot)|true|none|Document model representing a snapshot of data with metadata.|

<h2 id="tocS_SnapshotRestore">SnapshotRestore</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotrestore"></a>
<a id="schema_SnapshotRestore"></a>
<a id="tocSsnapshotrestore"></a>
<a id="tocssnapshotrestore"></a>

```json
{
  "_id": "5eb7cf5a86d9755df3a6c593",
  "snapshot_restore_id": "string",
  "snapshot_id": "",
  "company_id": "",
  "created_at": "2019-08-24T14:15:22Z",
  "collections": [
    "string"
  ],
  "description": "",
  "status": "string",
  "drop_existing": false,
  "snapshot_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  }
}

```

SnapshotRestore

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|_id|any|false|none|MongoDB document ObjectID|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[PydanticObjectId](#schemapydanticobjectid)|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|null|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|snapshot_restore_id|string|false|none|none|
|snapshot_id|string|false|none|none|
|company_id|string|false|none|none|
|created_at|string(date-time)|false|none|none|
|collections|[string]|true|none|none|
|description|string|false|none|none|
|status|any|false|none|none|

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
|drop_existing|boolean|false|none|none|
|snapshot_model|[Snapshot](#schemasnapshot)|true|none|Document model representing a snapshot of data with metadata.|

<h2 id="tocS_SnapshotRestoreListResponse">SnapshotRestoreListResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotrestorelistresponse"></a>
<a id="schema_SnapshotRestoreListResponse"></a>
<a id="tocSsnapshotrestorelistresponse"></a>
<a id="tocssnapshotrestorelistresponse"></a>

```json
{
  "data": [
    {}
  ],
  "pagination": {
    "current_page": 1,
    "has_next": false,
    "has_previous": true,
    "last_page": 1,
    "next_page": 2,
    "page_size": 20
  }
}

```

SnapshotRestoreListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[object]|true|none|none|
|pagination|[PaginationMetadata](#schemapaginationmetadata)|true|none|Pagination metadata model for list responses.|

<h2 id="tocS_SnapshotRestoreResponse">SnapshotRestoreResponse</h2>
<!-- backwards compatibility -->
<a id="schemasnapshotrestoreresponse"></a>
<a id="schema_SnapshotRestoreResponse"></a>
<a id="tocSsnapshotrestoreresponse"></a>
<a id="tocssnapshotrestoreresponse"></a>

```json
{
  "restore_id": "string",
  "snapshot_id": "string",
  "company_id": "string",
  "created_at": "2019-08-24T14:15:22Z",
  "collections": [
    "string"
  ],
  "description": "",
  "status": "string",
  "drop_existing": false,
  "snapshot_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_id": "string",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "description": "",
    "backup_path": "string",
    "database_name": "string",
    "collections": [
      "string"
    ],
    "size_bytes": 0,
    "status": "string",
    "compressed": false
  },
  "snapshot_restore_model": {
    "_id": "5eb7cf5a86d9755df3a6c593",
    "snapshot_restore_id": "string",
    "snapshot_id": "",
    "company_id": "",
    "created_at": "2019-08-24T14:15:22Z",
    "collections": [
      "string"
    ],
    "description": "",
    "status": "string",
    "drop_existing": false,
    "snapshot_model": {
      "_id": "5eb7cf5a86d9755df3a6c593",
      "snapshot_id": "string",
      "company_id": "",
      "created_at": "2019-08-24T14:15:22Z",
      "description": "",
      "backup_path": "string",
      "database_name": "string",
      "collections": [
        "string"
      ],
      "size_bytes": 0,
      "status": "string",
      "compressed": false
    }
  }
}

```

SnapshotRestoreResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|restore_id|string|true|none|none|
|snapshot_id|string|true|none|none|
|company_id|string|true|none|none|
|created_at|string(date-time)|true|none|none|
|collections|[string]|true|none|none|
|description|string|false|none|none|
|status|any|false|none|none|

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
|drop_existing|boolean|false|none|none|
|snapshot_model|[Snapshot](#schemasnapshot)|true|none|Document model representing a snapshot of data with metadata.|
|snapshot_restore_model|[SnapshotRestore](#schemasnapshotrestore)|true|none|Document model representing a snapshot of data with metadata.|

<h2 id="tocS_TransactionStatsResponse">TransactionStatsResponse</h2>
<!-- backwards compatibility -->
<a id="schematransactionstatsresponse"></a>
<a id="schema_TransactionStatsResponse"></a>
<a id="tocStransactionstatsresponse"></a>
<a id="tocstransactionstatsresponse"></a>

```json
{
  "count": 0,
  "percentage": 0
}

```

TransactionStatsResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|count|integer|true|none|Transaction count|
|percentage|number|true|none|Percentage of total transactions|

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

<h2 id="tocS_WhitelistListResponse">WhitelistListResponse</h2>
<!-- backwards compatibility -->
<a id="schemawhitelistlistresponse"></a>
<a id="schema_WhitelistListResponse"></a>
<a id="tocSwhitelistlistresponse"></a>
<a id="tocswhitelistlistresponse"></a>

```json
{
  "data": [
    {
      "id": "string",
      "value": "string",
      "expire_at": "2019-08-24T14:15:22Z",
      "created_at": "2019-08-24T14:15:22Z",
      "updated_at": "2019-08-24T14:15:22Z"
    }
  ],
  "pagination": {}
}

```

WhitelistListResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[WhitelistResponse](#schemawhitelistresponse)]|true|none|[Pydantic model for the whitelist object.]|
|pagination|object|true|none|none|

<h2 id="tocS_WhitelistRequest">WhitelistRequest</h2>
<!-- backwards compatibility -->
<a id="schemawhitelistrequest"></a>
<a id="schema_WhitelistRequest"></a>
<a id="tocSwhitelistrequest"></a>
<a id="tocswhitelistrequest"></a>

```json
{
  "value": "user@example.com",
  "expire_at": "2025-12-31T23:59:59Z"
}

```

WhitelistRequest

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|true|none|Value to be whitelisted. Accepts customer emails, phone numbers, or payment card hashes. Must not be empty.|
|expire_at|string(date-time)|false|none|Expiration date for this whitelist entry. Defaults to 1 year from creation.|

<h2 id="tocS_WhitelistResponse">WhitelistResponse</h2>
<!-- backwards compatibility -->
<a id="schemawhitelistresponse"></a>
<a id="schema_WhitelistResponse"></a>
<a id="tocSwhitelistresponse"></a>
<a id="tocswhitelistresponse"></a>

```json
{
  "id": "string",
  "value": "string",
  "expire_at": "2019-08-24T14:15:22Z",
  "created_at": "2019-08-24T14:15:22Z",
  "updated_at": "2019-08-24T14:15:22Z"
}

```

WhitelistResponse

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|none|
|value|string|true|none|none|
|expire_at|string(date-time)|true|none|none|
|created_at|string(date-time)|true|none|none|
|updated_at|string(date-time)|true|none|none|

