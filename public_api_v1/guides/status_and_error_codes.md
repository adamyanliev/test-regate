---
title: Status codes and errors
excerpt: Possible status code responses when using the Regate API
category: 64510dd40228561019a31111
slug: status-codes-and-errors
---

# Overview

The Regate API uses standard HTTP response codes to indicate the success or failure of an API request. Overall:

- Codes in the 2xx range indicate a successfully processed request.
- Codes in the 4xx range indicate that there was an error with the request (e.g. unauthorized access, missing required attribute, etc.).
- Codes in the 5xx range indicate that there is an issue with Regate's servers. Those are quite rare.

Error responses include an Error Identifier, Error Message and Status Code.

# List of error codes

| Status code | Reason                  | Description                                                                                                                                                                                                                                 |
| :---------- | :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `200`       | `OK`                    | Successful operation. Congratulations!                                                                                                                                                                                                      |
| `201`       | `Created`               | Returned when a `POST` request was successful.                                                                                                                                                                                              |
| `202`       | `No Content`            | Returned when a `DELETE` request was successfully processed.                                                                                                                                                                                |
| `400`       | `Bad request`           | Request cannot be processed due to a client error - e.g. bad syntax, missing mandatory attribute in the payload, etc.                                                                                                                       |
| `401`       | `Unauthorized`          | Invalid authentication credentials.                                                                                                                                                                                                         |
| `403`       | `Forbidden`             | Authentication has passed, but the user has insufficient rights to perform the requested action.                                                                                                                                            |
| `404`       | `Not found`             | The URL has not been found.                                                                                                                                                                                                                 |
| `422`       | `Unprocessable Entity`  | The payload contains attribute values which contradict the Regate application logic. For example, a request to create an invoice where the total amount is lower than the VAT amount in the payload will be declined with this error code.  |
| `429`       | `Too many requests`     | The maximum number of calls per minute allowed by our API has been reached.                                                                                                                                                                 |
| `500`       | `Internal server error` | There is an issue on our side and we apologize. These types of errors will contain an error identifier in its description (**example?**). Please contact our support team, providing the error identifier, and we will do our best to help. |