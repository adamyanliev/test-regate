---
title: Authentication
excerpt: How to authenticate while using the Regate API
category: 63bd467548701e007e6ae9da
slug: authentication
---

# Token API authentication aaa

The Token API uses [HTTP basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication). In each request you need to provide your Regate API and secret key.

# Invoice API authentication

The Invoice API endpoints use Bearer token authentication. Once the bearer token is generated using a `POST` request to the Token API endpoint, the client must send this token in the Authorization header when making requests to the Invoice API.
