# Didomi (didomi)

Didomi is a Paris-based consent and preference management platform (CMP/PMP) that helps publishers, advertisers, retailers, and large enterprises collect, manage, and act on user privacy choices across web, mobile, CTV, AMP, and in-game surfaces. The platform covers GDPR, CCPA and the wider US-state law landscape, IAB TCF v2.x, IAB GPP, GPC, EU DMA, Chilean Law 25, Australian privacy law, and Nordic regimes through a single multi-regulation configuration model. Didomi exposes a JSON REST API (`https://api.didomi.io/v1/`) plus first-party SDKs for Web, iOS / tvOS, Android / Android TV, Unity, React Native, Flutter, Vega OS, and AMP, alongside IAB-compliant consent-string tooling and reverse-proxy boilerplates for Fastly, AWS CloudFront, and Cloudflare.

**URL:** [Visit APIs.json](https://raw.githubusercontent.com/api-evangelist/didomi/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

- Advertising, AdTech, CCPA, CMP, Consent, Consent Management, DSAR, Data Privacy, GDPR, IAB TCF, MarTech, Preference Management, Privacy, Privacy Requests, Regulatory Compliance

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## APIs

### Didomi Platform API

REST API at `https://api.didomi.io/v1/` exposing 80+ operations across consents (events, proofs, tokens, users), widgets (notices, configs, deployments, SDK configs, templates), data manager metadata (vendors, purposes, partners, taxonomies, regulations), and administration (organizations, members, keys, secrets, domains, SSO, premium features). Authentication is JWT bearer — POST `api-key` + `secret` to `/v1/sessions` and reuse `access_token` for one hour. Default rate limit: 100 requests / 15 seconds per organization (the `/consents/*` family is exempt).

**Human URL:** [https://developers.didomi.io/api-and-platform/introduction](https://developers.didomi.io/api-and-platform/introduction)

- [Documentation](https://developers.didomi.io/api-and-platform/introduction)
- [Authentication](https://developers.didomi.io/api-and-platform/introduction/authentication)
- [Rate Limiting](https://developers.didomi.io/api-and-platform/introduction/rate-limiting)
- [Errors](https://developers.didomi.io/api-and-platform/introduction/errors)
- [Pagination](https://developers.didomi.io/api-and-platform/introduction/pagination)
- [OpenAPI](openapi/didomi-platform-api-openapi.yml)
- [JSON Schema — Consent Event](json-schema/didomi-consent-event-schema.json)
- [JSON Schema — Consent Notice](json-schema/didomi-consent-notice-schema.json)
- [JSON Schema — Privacy Request](json-schema/didomi-privacy-request-schema.json)
- [JSON Structure — Consent Event](json-structure/didomi-consent-event-structure.json)
- [Example — Consent Event](examples/didomi-consent-event-example.json)
- [Example — Consent Notice](examples/didomi-consent-notice-example.json)
- [Example — Privacy Request](examples/didomi-privacy-request-example.json)
- [Naftiko Capability — Sessions & Authentication](capabilities/sessions-authentication.yaml)
- [Naftiko Capability — Consents Events](capabilities/consents-events.yaml)
- [Naftiko Capability — Consents Proofs](capabilities/consents-proofs.yaml)
- [Naftiko Capability — Consents Users & Tokens](capabilities/consents-users.yaml)
- [Naftiko Capability — Widgets, Notices & Templates](capabilities/widgets-notices.yaml)
- [Naftiko Capability — Data Manager Vendors](capabilities/data-manager-vendors.yaml)
- [Naftiko Capability — Data Manager Purposes](capabilities/data-manager-purposes.yaml)
- [Naftiko Capability — Organizations, Members & SSO](capabilities/organizations.yaml)
- [Naftiko Capability — Keys, Secrets & Quotas](capabilities/keys-secrets.yaml)
- [Naftiko Capability — Domains & Cookies](capabilities/domains.yaml)

### Didomi Web SDK

Browser-side library that renders consent notices, preference centers, and privacy widgets, gates third-party tags on consent, and writes IAB TCF v2 / IAB GPP / Didomi consent strings. Programmatic API (`Didomi.getUserConsentStatus`, `Didomi.setUserAgreeToAll`, `Didomi.openPreferences`, etc.), typed event bus, and out-of-the-box integrations with GTM, Adobe Launch, Tealium, Prebid, Google Consent Mode v2, Salesforce DMP, Piano Analytics, and more.

**Human URL:** [https://developers.didomi.io/cmp/web-sdk](https://developers.didomi.io/cmp/web-sdk)

- [Documentation](https://developers.didomi.io/cmp/web-sdk)
- [Getting Started](https://developers.didomi.io/cmp/web-sdk/getting-started)
- [API Reference](https://developers.didomi.io/cmp/web-sdk/reference/api)
- [Events](https://developers.didomi.io/cmp/web-sdk/reference/events)
- [Versions](https://developers.didomi.io/cmp/web-sdk/reference/versions)
- [Performance](https://developers.didomi.io/cmp/web-sdk/performance)

### Didomi Android SDK

Native consent notices, preference popups, and TCF / GPP / Didomi consent-string generation for Android and Android TV apps in Java, Kotlin, and Jetpack Compose. Shares consent with WebViews and bridges to Google Consent Mode v2.

**Human URL:** [https://developers.didomi.io/cmp/mobile-sdk/android](https://developers.didomi.io/cmp/mobile-sdk/android)

- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/android)
- [Setup](https://developers.didomi.io/cmp/mobile-sdk/android/setup)
- [API Reference](https://developers.didomi.io/cmp/mobile-sdk/android/reference/api)
- [Events](https://developers.didomi.io/cmp/mobile-sdk/android/reference/events)
- [Versions](https://developers.didomi.io/cmp/mobile-sdk/android/versions)

### Didomi iOS SDK

iOS / tvOS / Mac Catalyst SDK rendering Didomi consent notices and preference centers natively in Swift and Objective-C apps. Coordinates Apple App Tracking Transparency (ATT) with consent, shares consent with WebViews, and emits TCF / GPP / Didomi consent strings. Distributed via Swift Package Manager and CocoaPods.

**Human URL:** [https://developers.didomi.io/cmp/mobile-sdk/ios](https://developers.didomi.io/cmp/mobile-sdk/ios)

- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/ios)
- [Setup](https://developers.didomi.io/cmp/mobile-sdk/ios/setup)
- [API Reference](https://developers.didomi.io/cmp/mobile-sdk/ios/reference/api)
- [App Tracking Transparency](https://developers.didomi.io/cmp/mobile-sdk/ios/app-tracking-transparency-ios-14)
- [Events](https://developers.didomi.io/cmp/mobile-sdk/ios/reference/events)
- [Versions](https://developers.didomi.io/cmp/mobile-sdk/ios/versions)

### Didomi Cross-Platform SDKs (React Native, Flutter, Unity, Vega OS, AMP)

First-party Didomi CMP plugins for React Native, Flutter, Unity (games and consoles), Vega OS (LG webOS smart TVs), and Google AMP. Each wraps notice rendering, consent storage, the event bus, and consent-string generation so cross-platform teams ship one consent UX across browser, native mobile, CTV, in-game, and AMP surfaces.

**Human URL:** [https://developers.didomi.io/cmp/mobile-sdk](https://developers.didomi.io/cmp/mobile-sdk)

- [React Native](https://developers.didomi.io/cmp/mobile-sdk/react-native)
- [Flutter](https://developers.didomi.io/cmp/mobile-sdk/flutter)
- [Unity](https://developers.didomi.io/cmp/mobile-sdk/unity-sdk)
- [Vega OS](https://developers.didomi.io/cmp/mobile-sdk/vega-os)
- [AMP](https://developers.didomi.io/cmp/amp)

### Didomi Consent String Toolkit

Open-source libraries published under `github.com/didomi` for encoding, decoding, and validating Didomi and IAB TCF v2 consent strings: TypeScript (`consent-string`, `consent-string-schema`), Rust with C/Java FFI (`consent-string-decoder-rust`), Go (`consent-string-golang`), and a fork of the official IAB tooling (`iabtcf-es`). Useful for server-side auditing and downstream ad-tech.

**Human URL:** [https://developers.didomi.io/cmp/didomi-consent-string](https://developers.didomi.io/cmp/didomi-consent-string)

- [Didomi Consent String](https://developers.didomi.io/cmp/didomi-consent-string)
- [Structure](https://developers.didomi.io/cmp/didomi-consent-string/didomi-consent-string-structure)
- [Examples](https://developers.didomi.io/cmp/didomi-consent-string/consent-string-examples)
- [consent-string (TypeScript)](https://github.com/didomi/consent-string)
- [consent-string-schema](https://github.com/didomi/consent-string-schema)
- [consent-string-decoder-rust](https://github.com/didomi/consent-string-decoder-rust)
- [consent-string-golang](https://github.com/didomi/consent-string-golang)
- [iabtcf-es](https://github.com/didomi/iabtcf-es)

## Common Properties

- [Portal — didomi.io](https://www.didomi.io)
- [Documentation — developers.didomi.io](https://developers.didomi.io/)
- [Getting Started](https://developers.didomi.io/cmp/web-sdk/getting-started)
- [Console](https://console.didomi.io)
- [SignUp / Contact Sales](https://www.didomi.io/contact-us)
- [Pricing / Offers](https://www.didomi.io/offers)
- [Status Page](https://status.didomi.io)
- [Blog](https://www.didomi.io/blog)
- [Support — Help Center](https://support.didomi.io)
- [Training — Didomi Academy](https://www.didomi.io/didomi-academy)
- [Terms of Service / Legal Notice](https://www.didomi.io/legal-notice)
- [Privacy Policy](https://www.didomi.io/privacy-policy)
- [Cookie Policy](https://www.didomi.io/cookie-policy)
- [LinkedIn](https://www.linkedin.com/company/didomi)
- [GitHub Organization](https://github.com/didomi)
- [SDK — React component (npm)](https://www.npmjs.com/package/@didomi/react)
- [SDK — React Native](https://github.com/didomi/react-native)
- [SDK — Flutter](https://github.com/didomi/flutter)
- [SDK — Unity](https://github.com/didomi/unity)
- [SDK — iOS (Swift Package)](https://github.com/didomi/didomi-ios-sdk-spm)
- [Tool — GTM template](https://github.com/didomi/gtm-template)
- [Tool — Magento 2 extension](https://github.com/didomi/magento)
- [Tool — mParticle JS kit](https://github.com/didomi/mparticle-javascript-integration-didomi)
- [Tool — Firebase Cloud Functions](https://github.com/didomi/firebase)
- [CodeExamples — Implementation samples](https://github.com/didomi/samples)
- [CodeExamples — Fastly reverse-proxy](https://github.com/didomi/boilerplate-fastly-reverse-proxy-didomi-cmp)
- [CodeExamples — CloudFront reverse-proxy](https://github.com/didomi/boilerplate-aws-cloudfront-reverse-proxy-didomi-cmp)
- [CodeExamples — Cloudflare reverse-proxy](https://github.com/didomi/boilerplate-cloudflare-reverse-proxy-didomi-cmp)

## Artifacts

Machine-readable specifications, schemas, and capabilities for the Didomi Platform.

### OpenAPI

- [Didomi Platform API](openapi/didomi-platform-api-openapi.yml)

### JSON Schema

- [Consent Event](json-schema/didomi-consent-event-schema.json)
- [Consent Notice](json-schema/didomi-consent-notice-schema.json)
- [Privacy Request](json-schema/didomi-privacy-request-schema.json)

### JSON Structure

- [Consent Event](json-structure/didomi-consent-event-structure.json)

### JSON-LD

- [Didomi Context](json-ld/didomi-context.jsonld)

### Examples

- [Consent Event](examples/didomi-consent-event-example.json)
- [Consent Notice](examples/didomi-consent-notice-example.json)
- [Privacy Request](examples/didomi-privacy-request-example.json)

### Spectral Rules

- [Didomi Rules](rules/didomi-rules.yml)

### Vocabulary

- [Didomi Vocabulary](vocabulary/didomi-vocabulary.yml)

### Capabilities (Naftiko)

- [Sessions & Authentication](capabilities/sessions-authentication.yaml)
- [Consents — Events](capabilities/consents-events.yaml)
- [Consents — Proofs](capabilities/consents-proofs.yaml)
- [Consents — Users & Tokens](capabilities/consents-users.yaml)
- [Widgets — Notices, Configs & Templates](capabilities/widgets-notices.yaml)
- [Data Manager — Vendors & Taxonomies](capabilities/data-manager-vendors.yaml)
- [Data Manager — Purposes & Groups](capabilities/data-manager-purposes.yaml)
- [Organizations, Members & SSO](capabilities/organizations.yaml)
- [Keys, Secrets & Quotas](capabilities/keys-secrets.yaml)
- [Domains & Cookies](capabilities/domains.yaml)

### Commercial artifacts

- [Plans / Pricing](plans/didomi-plans-pricing.yml)
- [Rate Limits](rate-limits/didomi-rate-limits.yml)
- [FinOps Definition](finops/didomi-finops.yml)

## Maintainers

**FN:** API Evangelist

**Email:** info@apievangelist.com
