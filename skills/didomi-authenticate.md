---
name: didomi-authenticate
description: >-
  Obtain and maintain a Didomi Platform API session — exchange an organization
  API key and secret for a 1-hour JWT, cache it, and handle expiry, rate limits
  and the error envelope correctly. Read this before any other Didomi skill;
  every other call depends on it.
api: Didomi Platform API
base_url: https://api.didomi.io/v1
openapi: ../openapi/didomi-platform-api-openapi.yml
operations:
  - POST /sessions
  - GET /sessions/{id}
  - GET /quotas
  - GET /keys
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/_original/didomi-platform-api-openapi.yml and
  https://developers.didomi.io/api-and-platform/introduction/authentication
---

# Authenticate against the Didomi Platform API

Didomi does not accept an API key directly. Every call needs a JWT, and the JWT
is minted from the key.

## Get the credentials

Didomi Console → the correct organization → **Settings / Private API keys** →
generate a key and secret. The secret is shown once.

## Mint a token

```
POST https://api.didomi.io/v1/sessions
Content-Type: application/json

{"type": "api-key", "key": "<API_KEY>", "secret": "<API_SECRET>"}
```

Response:

```json
{"access_token": "<jwt>"}
```

Then, on every other call:

```
Authorization: Bearer <access_token>
```

## The rules that actually matter

1. **TTL is 3600 seconds.** Cache the token and reuse it. Didomi explicitly asks
   you not to mint one per request. For long-running processes, refresh on a
   timer at ~50 minutes rather than waiting for a 401.
2. **Bad credentials return `400`, not `401`.** A 401 means the token on THIS
   call was missing, malformed or expired — a different failure with a different
   fix. Do not collapse them into one handler.
3. **HTTPS only.** Plain HTTP gets a `301` to the HTTPS equivalent; some clients
   drop the Authorization header across that redirect. Always call https://
   directly.
4. **`type` is `api-key`.** The endpoint also accepts `email` type sessions for
   Console users — do not use those for machine access.
5. **No OAuth, no scopes, no refresh token.** The bearer JWT is
   all-or-nothing for the organization the key belongs to. There is no way to
   mint a reduced-privilege token, which means an agent given a Didomi key has
   the same reach as the key itself. Scope the key, not the token.

## Know your limits before you start

```
GET /quotas?organization_id={org}
```

Returns the organization's enforced limits — `api_requests` (100 per 15s),
`parallel_notices_deployments` (3), `exports_configs` (3),
`exports_destinations` (2), `consent_proof_reports` (10/month), `secrets` (300),
`metadata_partners` (500), `metadata_purposes` (300),
`scraper_enabled_properties` (250). Quota increases go through
support@didomi.io.

## Rate limiting

- Default: **100 requests every 15 seconds, per ORGANIZATION** — shared across
  every API key that organization holds. Adding keys does not add headroom.
- `/consents/*` is exempt, except `GET /consents/users` and
  `GET /consents/users/{id}` with `$include_full_tree=true`.
- Every rate-limited response carries IETF draft-07 headers:
  - `RateLimit: limit=100, remaining=60, reset=7`
  - `RateLimit-Policy: 100;w=15`
- On exhaustion: `429` plus `Retry-After: <seconds>`.

Read `remaining` on every response and back off before you are throttled.
Didomi states these limits "are subject to change at any time without prior
communication" — do not hard-code 100/15s as an invariant, read the headers.

## Caching

Some high-traffic routes are served from Didomi's cache for API-key traffic.
Two response headers tell you:

- `X-DidomiCacheEnabled: true|false`
- `X-DidomiCacheHit: true|false`

Cached data is purged automatically when the underlying record changes, so a
write-then-read is safe. There is no ETag / conditional-request support.

## Error envelope

Every failure, on every route:

```json
{"code": 401, "name": "Unauthorized", "message": "…", "errors": {}}
```

It is **not** RFC 9457 problem+json. Branch on `code`.

## Key hygiene

`GET /keys?organization_id={org}` lists the organization's keys;
`DELETE /keys/{id}` revokes one. Rotate on a schedule — there is no key
expiry and no last-used timestamp exposed, so a leaked key stays valid until
somebody deletes it.
