---
name: didomi-dsar-erasure
description: >-
  Execute a GDPR Article 17 / CCPA delete request against Didomi — locate the
  consent subject, export their record for the response pack, then erase their
  consent events and user record. Use when handling a data-subject erasure
  request or a right-to-delete.
api: Didomi Platform API
base_url: https://api.didomi.io/v1
openapi: ../openapi/didomi-platform-api-openapi.yml
operations:
  - POST /sessions
  - GET /consents/users
  - GET /consents/users/{id}
  - GET /consents/events
  - DELETE /consents/events
  - DELETE /consents/events/{id}
  - DELETE /consents/users/{id}
mirrors: ../arazzo/didomi-data-subject-erasure-workflow.yml
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/_original/didomi-platform-api-openapi.yml and
  https://developers.didomi.io/api-and-platform/consents/events
---

# Erase a data subject from Didomi

This is a destructive, legally-consequential flow. Every step below is
irreversible once executed and Didomi publishes no undo.

**Require human confirmation before step 4.**

## 1. Get a token

```
POST https://api.didomi.io/v1/sessions
{"type": "api-key", "key": "<API_KEY>", "secret": "<API_SECRET>"}
```

Send `Authorization: Bearer <access_token>` on everything that follows. Token
TTL is 3600 seconds.

## 2. Resolve the subject

You will usually be given the customer's own identifier, not Didomi's.

```
GET /consents/users?organization_id={org}&organization_user_id={their_id}
```

- `organization_user_id` is whatever your organization used at collection time —
  an email, a phone number, a client ID.
- The Didomi `id` on the returned record is what the erasure calls need.
- **`/consents/*` does not support generic filtering.** Use the documented
  query parameters only; do not attempt arbitrary field filters here.

If you need the full expanded record:

```
GET /consents/users/{id}?organization_id={org}&$include_full_tree=true
```

⚠️ `$include_full_tree=true` moves this call OUT of the unlimited `/consents/*`
pool and INTO the 100-requests / 15-seconds bucket. Do not loop on it.

## 3. Export before you delete

Retrieve the full consent history so it can go in the response pack — after
step 4 it is gone.

```
GET /consents/events?organization_id={org}&organization_user_id={their_id}&status[$in]=confirmed&status[$in]=pending_approval&regulation[$in]=gdpr&regulation[$in]=cpra
```

Set both filters deliberately: with no `status` filter you get only confirmed
events, and with no `regulation` filter you get only GDPR events. An export that
silently omits pending or non-GDPR events is an incomplete Article 15 response.

Page with `$limit` and `$skip`; the envelope is `{total, limit, skip, data}`.

## 4. Erase — HUMAN CONFIRMATION REQUIRED

Delete the events, filtered:

```
DELETE /consents/events?organization_id={org}&organization_user_id={their_id}
```

Or a single event:

```
DELETE /consents/events/{id}?organization_id={org}
```

The filter keys are property names from the Event schema, with nested paths
separated by `.` — e.g. `metadata.booking_id={value}` to scope the delete to one
booking. Didomi documents this exact form.

Then delete the user record:

```
DELETE /consents/users/{id}?organization_id={org}
```

## 5. Verify

```
GET /consents/events?organization_id={org}&organization_user_id={their_id}
```

Expect `total: 0`. A `404` from `GET /consents/users/{id}` confirms the user
record is gone.

## Consent proofs are NOT erased by this flow

`/consents/proofs` exposes only `POST` (upload) and `GET /{id}` (retrieve).
There is **no delete operation for a consent proof** in the API. If proofs were
uploaded for this subject you must handle them out of band — raise it with
support@didomi.io and record the decision in your erasure log. Do not report the
erasure as complete without addressing them.

## Webhooks fire

Erasure emits `event.deleted` and `user.deleted` to your configured webhook
endpoint. Downstream systems subscribed to those events will act on them. If
your CRM maps Didomi events onto contact records, confirm it handles deletes
before running this at volume.

## Errors

- `401` — token expired (TTL 3600s). Mint a new one and retry once.
- `404` — the id does not exist, or belongs to another organization. Re-check
  `organization_id`.
- `403` — the Consents API is priced separately from CMP/PMP; a 403 here may
  mean the module is not in your contract, not that the record is protected.
