# Errors

The Frauddi API uses conventional HTTP response codes to indicate the success or failure of an API request.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- Access denied
404 | Not Found -- The specified resource could not be found
422 | Unprocessable Entity -- Validation error
429 | Too Many Requests -- You're making too many requests
500 | Internal Server Error -- We had a problem with our server
503 | Service Unavailable -- We're temporarily offline for maintenance

## Error Response Format

```json
{
  "error": {
    "type": "validation_error",
    "message": "The request parameters are invalid",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

All errors return a JSON object with an `error` field containing:

- **type**: The category of error
- **message**: Human-readable error message  
- **details**: Array of specific validation errors (when applicable)
