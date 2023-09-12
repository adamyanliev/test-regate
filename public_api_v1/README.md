#### Public API best practices:

1.  Use standards: Follow established standards like REST or GraphQL.
2.  Document thoroughly: Provide clear and comprehensive documentation with examples.
3.  Versioning: Use versioning to maintain backwards compatibility and avoid breaking changes.
4.  Security: Implement proper authentication and authorization mechanisms to protect data.
5.  Error handling: Return meaningful error responses and messages to help debug issues.
6.  CORS: Enable CORS (Cross-Origin Resource Sharing) to allow requests from different domains.
7.  Rate limiting: Implement rate limiting to prevent abuse and maintain system stability.
8.  Performance: Optimize API performance for speed and scalability.
9.  Testing: Automate testing to catch bugs and ensure API reliability.
10. Monitoring: Monitor API usage and performance to catch and address issues quickly.

**Current phase:** Customers Endpoint

TODO:

- Modify cors to allow external requests
- error handling and payload structure
- json_api/stripe best practices for the payloads
- authorization context for pundit instead of user
- customers pagination
- customers filtering

#### Curl Test Example

In the rails console:

```
token = PublicApi::V1::ApiKeys::Token.generate
ApiKey.create(bearer: HoldingUser.first, **token.attributes)
token.raw_token # only available during the lifetime of this object
```

Returns:

```
"api_usr_vJF8jHTUHwNz26GLKYizXaQwxdN2QVJwtXm7mm"
```

In a terminal:

- **With a correct key**

```
curl http://localhost:3000/public_api/v1/api_keys \
  -H "Authorization: Bearer api_usr_vJF8jHTUHwNz26GLKYizXaQwxdN2QVJwtXm7mm" \
  -H "Accept: application/vnd.regate_api.v1.json"
```

Returns:

```
{
  "api_keys":[
    {
      "id":"<api_key_id>",
      "token":"api_usr_vJF8jH******************************",
      "created_at":"2023-02-09T12:29:35.682Z",
      "updated_at":"2023-02-09T12:29:35.682Z",
      "revoked_at":null
    }
  ]
}%
```

- **With a fake key**

```
curl http://localhost:3000/public_api/v1/api_keys \
  -H "Authorization: Bearer fake_key" \
  -H "Accept: application/vnd.regate_api.v1.json"
```

Returns:

```
{
  "errors": [
    "Access denied"
  ]
}
```

- **With insufficient rights**

```
curl http://localhost:3000/public_api/v1/api_keys \
  -H "Authorization: Bearer fake_key" \
  -H "Accept: application/vnd.regate_api.v1.json"
```

Returns:

```
{
  "errors": [
    "Unauthorized"
  ]
}
```

NOTE: Check the Postman collection for all the endpoints (public_api folder)
