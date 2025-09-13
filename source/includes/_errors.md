# Errors

The Frauddi API uses conventional HTTP response codes to indicate the success or failure of an API request.

Error Code | Meaning
---------- | -------
400 | Bad Request -- The request was invalid or cannot be served
401 | Unauthorized -- Authentication is required to access this resource
403 | Forbidden -- You do not have permission to access this resource
404 | Not Found -- The requested resource could not be found
409 | Conflict -- The request conflicts with the current state of the resource
422 | Unprocessable Entity -- Validation errors in the request data
500 | Internal Server Error -- An unexpected error occurred on the server

## Error Response Format

```json
{
  "error": {
    "type": "bad_request_error",
    "message": "The request was invalid or cannot be served.",
    "status_code": 400
  }
}
```

All errors return a JSON object with an `error` field containing:

- **type**: The specific error type (e.g., "unauthorized_error", "validation_error")
- **message**: Human-readable error message
- **status_code**: HTTP status code

## Error Types

- `bad_request_error` - Invalid request format or parameters
- `unauthorized_error` - Missing or invalid API key
- `forbidden_error` - Insufficient permissions
- `not_found_error` - Resource does not exist
- `conflict_error` - Request conflicts with current state
- `unprocessable_entity_error` - Validation failed
- `internal_server_error` - Server-side error
