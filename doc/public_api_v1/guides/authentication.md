---
title: Authentication
excerpt: How to authenticate while using the Regate API
category: 63bd467548701e007e6ae9da
slug: authentication
---

# Overview

The Regate API uses Bearer tokens to authenticate requests. The tokens are generated and managed in the Regate app under [Settings > Connect Regate to your tools > Public API > Generate a token](link).

> Info
>
> Only Regate users with specific permissions (## more details needed ##) are able to access this section of the Regate app and create / manage Bearer tokens.

# Create a token

When creating a token, the user selects the following attributes:

- Token name
- User role permissions

The bearer tokens do not have a validity period and do not expire. A user is able to create multiple tokens.

## Token Visibility

Once created, **the token value will be visible only once.** For security purposes, the token value is not stored on Regate's end. Please make sure to copy its value before proceeding further.

## Token permissions

The user role permissions selected for the token regulate what type of API calls can be made using it. For example, permissions may allow users to only retrieve sales invoices, but not create new ones. In case an API request is authenticated with a token without permissions for that specific call, a `403 - Forbidden` error code will be returned.

(## probably will need a list of available API actions, dependent on role permissions##)

# Manage your tokens

You can see the active tokens for your holding by going to [Settings > Connect Regate to your tools > Public API > Generate a token](link). The following information is available:

- Token name
- User role permissions
- Creation date
- Last used date

Tokens can also be revoked from this section.

> Warning
>
> Once revoked, a token cannot be reinstated.