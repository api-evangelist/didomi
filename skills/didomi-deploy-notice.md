---
name: didomi-deploy-notice
description: >-
  Create, configure and publish a Didomi consent notice to production —
  including the multi-regulation configuration that decides which notice a user
  sees in which jurisdiction. Use when standing up a new property, changing
  notice copy or vendors, or rolling a configuration change to live traffic.
api: Didomi Platform API
base_url: https://api.didomi.io/v1
openapi: ../openapi/didomi-platform-api-openapi.yml
operations:
  - POST /sessions
  - POST /widgets/notices
  - GET /widgets/notices
  - POST /widgets/notices/texts
  - POST /widgets/notices/texts-contents
  - GET /widgets/notices/configs
  - PATCH /widgets/notices/configs/{id}
  - POST /widgets/notices/deployments
  - GET /widgets/notices/deployments/{id}
  - GET /widgets/notices/sdk-configs
mirrors: ../arazzo/didomi-deploy-notice-workflow.yml
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/_original/didomi-platform-api-openapi.yml and
  https://developers.didomi.io/api-and-platform/widgets/consent-notices
---

# Publish a Didomi consent notice

A deployment changes what every visitor to the property sees. Treat step 5 as a
production release, not an API call.

## The object chain

```
notice ──► notice_config ──► notice_regulation_config (one per regulation)
   │              └──► notice_text ──► notice_text_content (one per language)
   └──► notice_deployment ──► sdk_config   (what the loader actually serves)
```

Understanding this chain is most of the job. A notice on its own renders
nothing; a configuration on its own is not live; only a **deployment** promotes
a configuration to production.

## 1. Token

```
POST /sessions   {"type":"api-key","key":"<API_KEY>","secret":"<API_SECRET>"}
```

`Authorization: Bearer <access_token>` on everything after. TTL 3600s.

## 2. Create or find the notice

```
POST /widgets/notices?organization_id={org}
GET  /widgets/notices?organization_id={org}
```

Lists are paged with `$limit` / `$skip` and return
`{total, limit, skip, data}`. `$limit` should stay under 100.

## 3. Text and translations

```
POST /widgets/notices/texts?organization_id={org}
POST /widgets/notices/texts-contents?organization_id={org}
```

`notices-text` is the bundle; `notices-text-content` is one language of it,
bound by `text_id`. Create the bundle first, then a content record per language.
`GET /languages` returns the supported set.

## 4. Configuration — including regulations

```
GET   /widgets/notices/configs?organization_id={org}&notice_id={notice_id}
PATCH /widgets/notices/configs/{id}?organization_id={org}
```

**A configuration carries an array of per-regulation configurations.** Since
Didomi's multi-regulation migration, `notices-config.regulation_configurations[]`
holds a `notices-regulations-config` per regulation, each with its own
`regulation_id`, `template_id` and `text_id`. Editing only the top-level config
and expecting it to apply everywhere is the classic mistake here — read
Didomi's migration note at
`/api-and-platform/widgets/consent-notices/multi-reg-configurations/migration-of-existing-notices-and-api-updates`
before touching an existing notice.

Vendor and purpose behaviour can be overridden per notice AND per regulation via
`/metadata/partners-purposes-notices-regulations-overrides`. If a vendor appears
under one regulation but not another, that is where to look.

## 5. Deploy — HUMAN CONFIRMATION REQUIRED

```
POST /widgets/notices/deployments?organization_id={org}
{
  "notice_id": "{notice_id}",
  "production_config_id": "{config_id}"
}
```

- **Quota: `parallel_notices_deployments` defaults to 3.** More than three
  concurrent publishes will be rejected. Check with
  `GET /quotas?organization_id={org}`.
- This route is under the general limit — **100 requests / 15 seconds per
  organization**, shared across all keys.
- **There is no idempotency key.** If the POST times out, do NOT blind-retry.
  Call `GET /widgets/notices/deployments?organization_id={org}&notice_id={id}`
  and check whether the deployment already exists.

## 6. Verify what went live

```
GET /widgets/notices/deployments/{id}?organization_id={org}
GET /widgets/notices/sdk-configs?organization_id={org}
```

`sdk-configs` is the rendered artefact the CDN loader serves. Reading it back is
the only way to confirm what a browser will actually receive.

The loader itself is:

```
https://sdk.privacy-center.org/{apiKey}/loader.js?platform=web&target_type=notice&target={noticeId}
```

Note the URL is **unversioned** — you cannot pin a Web SDK build from it. Mobile
SDKs cache the remote configuration and refresh it every 60 minutes, so a mobile
rollout is not instantaneous.

## Rollback

There is no rollback endpoint. To revert, deploy the previous configuration id
again — so record the `production_config_id` you replaced before you deploy.

## Errors

- `400` — invalid configuration payload; read `message`.
- `401` — expired token (3600s).
- `403` — the module or premium feature is not in the organization's contract.
- `429` — general limit exceeded; honour `Retry-After`.
- `500` — check https://status.didomi.io (Platform API is a tracked component)
  before escalating to support@didomi.io.
