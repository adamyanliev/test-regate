---
title: Filtering
excerpt: How to use filters and pagination in the Regate API
category: 64510dd40228561019a31111
slug: filtering
---

# Overview

This section will explain how to use filters in the Regate API. Filtering helps you retrieve only the resources you need with your request.

# How it works

Use the `filter` object to set a query parameter when making a `GET` request. 

The query parameter name should be `filter[attributename_operator]`, where:

- `attributename` is the name of the attribute, on which you want to filter the result (`state`, `amount`, `currency` etc.)
- `operator` is the operator you want to compare by. See **Allowed operators** below for more details.

The syntax should be as follows:

```shell
GET /api/endpoint?filter[attributename_operator]=attributevalue&filter[attribute2_operator2]=attribute2value
```

# Allowed operators

The following operators can be used for filtering purposes:

| Operator | Description                                                                                                                                                                 |
| :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| eq       | Equal to                                                                                                                                                                    |
| not_eq   | Not equal to                                                                                                                                                                |
| gt       | Greater than                                                                                                                                                                |
| gteq     | Greater than or equal to                                                                                                                                                    |
| lt       | Less than                                                                                                                                                                   |
| lteq     | Less than or equal to                                                                                                                                                       |
| in       | Returns all records where a field is within a specified list. The list can be defined by specifying a range of values (e.g. `1..5`) or a list of values (e.g. `1,2,3,4,5`). |
| not_in   | Returns all records where a field is **not** within a specified list.                                                                                                       |

## Example 1 - Retrieve only recorded invoices

Let's say you want to retrieve only the invoices that are already recorded. You need the `state` attribute and the `eq` operator, and you need to set the value as `recorded`:

```shell
curl --request GET \
     --url 'https://api.regate.io/v1/customer_invoices?filter[state_eq]=recorded' \
     --header 'accept: application/json'
```

## Example 2 - Filter by invoice amount and currency

If you want to see all invoices with net amounts of 500 EUR or more, you need to filter by two different attributes - `currency` and `net_amount_cents`. 

Since you are looking for an exact match for the currency, you need to use the `eq` operator for it. For the amount, however, you need to use `gteq` instead.

```shell
curl --request GET \
     --url 'https://api.regate.io/v1/customer_invoices?filter[currency_eq]=EUR&filter[net_amount_cents_gteq]=50000' \
     --header 'accept: application/json'
```

# Pagination

## Limit number of results

To set a limit for the returned objects per page, set the `per_page` parameter to the desired number. The default limit for returned objects is 10 and the maximum is 1000.

**Example**

```shell
curl --request GET \
     --url 'https://api.regate.io/v1/customer_invoices?per_page=100' \
     --header 'accept: application/json'
```

## Select specific page of results

When the number of objects is too large to be returned in a single response page, you might want to retrieve a list starting from a specific page. Set the value of the `page` parameter to page you want to retrieve. The offset starts from `1`.

**Example**

```shell
curl --request GET \
     --url 'https://api.regate.io/v1/customer_invoices?page=5' \
     --header 'accept: application/json'
```

## Pagination in the response body

Whenever you are making a `GET` request, the response body will include two objects:

- `links` - Contains information on pagination
- `data` - Contains the retrieved objects

The `links` object contains three attributes, indicating specific URLs to call for different pages of results:

- `self` - The URL the current call was made to.
- `first` - The URL to call for the first page of results.
- `prev` - The URL to call for the previous page of results.
- `next` - The URL to call for the next page of results.
- `last` - The URL to call for the the last page of results.

**Example**

Here's an example of a `links` object after retrieving the third of 10 total pages of invoice objects:

```json
{
  "links": {
    "self": "https://api.regate.io/v1/customer_invoices?page=3",
    "first": "https://api.regate.io/v1/customer_invoices?page=1",
    "prev": "https://api.regate.io/v1/customer_invoices?page=2",
    "next": "https://api.regate.io/v1/customer_invoices?page=4",
    "last": "https://api.regate.io/v1/customer_invoices?page=10"
  },
  "data": [{
     ...
  }]
}`