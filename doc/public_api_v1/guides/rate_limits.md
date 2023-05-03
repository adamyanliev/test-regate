---
title: Rate limiting
excerpt: Learn how to work with the Regate API rate limits
category: 64510dd40228561019a31111
slug: rate-limiting
---

We have implemented several features to ensure the stability of the Regate API. If users send too many API requests in quick succession, a `429 - Too many requests` error message will be returned.

The rate limitations on the Regate API are the same across all API endpoints. The limit is shared across all tokens linked to a holding on Regate.

The current limits are as follows:

- 60 API calls per minute
- 10 API calls per second