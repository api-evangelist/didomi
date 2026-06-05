# Didomi (didomi)

Didomi is a Paris-based consent and preference management platform (CMP/PMP) that helps publishers, advertisers, retailers, and large enterprises collect, manage, and act on user privacy choices across web, mobile, CTV, and AMP surfaces. The platform covers GDPR, CCPA and the wider US state-law landscape, IAB TCF v2.x, Google Consent Mode v2, the IAB GPP, GPC, the EU DMA, Chilean Law 25, Australian privacy law, and other regulations through a single multi-regulation configuration model. Didomi exposes a JSON REST API (https://api.didomi.io/v1/) plus first-party SDKs for Web, iOS/tvOS, Android/Android TV, Unity, React Native, Flutter, Vega OS, and AMP, alongside IAB-compliant consent string tooling and reverse-proxy boilerplates for Fastly, CloudFront, and Cloudflare.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/didomi/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/didomi/refs/heads/main/apis.yml)

## Scope

- **Access:** 3rd-Party

## Tags

- Advertising
- AdTech
- CCPA
- CMP
- Consent
- Consent Management
- DSAR
- Data Privacy
- GDPR
- IAB TCF
- MarTech
- Preference Management
- Privacy
- Privacy Requests
- Regulatory Compliance

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## APIs

### Didomi Platform API

The Didomi Platform REST API at https://api.didomi.io/v1/ is the machine-facing surface for the entire Didomi CMP/PMP. It exposes 80+ operations across consents events / proofs / tokens / users, widgets (notices, configs, deployments, SDK configs, templates), data manager metadata (vendors, purposes, partners, taxonomies, regulations), and administration (organizations, members, keys, secrets, domains, SSO connections, premium features). Authentication is JWT bearer — clients POST API key + secret to /v1/sessions and reuse the returned access_token for one hour. Default rate limit is 100 requests per 15 seconds per organization (the /consents/* high-volume routes are exempt). Standard JSON request / response, cursor and offset pagination, structured error envelope.

- **Human URL:** [https://developers.didomi.io/api-and-platform/introduction](https://developers.didomi.io/api-and-platform/introduction)
- **Base URL:** `https://api.didomi.io/v1`

#### Tags

- Consent Management
- Data Manager
- Privacy
- Vendors
- Widgets

#### Properties

- [Documentation](https://developers.didomi.io/api-and-platform/introduction)
- [Authentication](https://developers.didomi.io/api-and-platform/introduction/authentication)
- [Rate Limits](https://developers.didomi.io/api-and-platform/introduction/rate-limiting)
- [Errors](https://developers.didomi.io/api-and-platform/introduction/errors)
- [Pagination](https://developers.didomi.io/api-and-platform/introduction/pagination)
- [OpenAPI](openapi/didomi-platform-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/didomi-consent-event-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/didomi-consent-notice-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/didomi-privacy-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/didomi-consent-event-structure.json)
- [Example](examples/didomi-consent-event-example.json)
- [Example](examples/didomi-consent-notice-example.json)
- [Example](examples/didomi-privacy-request-example.json)

### Didomi Web SDK

The Didomi Web SDK is the browser-side library that renders consent notices, preference centers, and privacy widgets, gates third-party tags on user consent, and writes IAB TCF v2 / GPP / Didomi consent strings to storage. It exposes a programmatic API (Didomi.getUserConsentStatus, Didomi.setUserAgreeToAll, Didomi.openPreferences, etc.), a typed event bus, and integrations with Google Tag Manager, Adobe Launch, Tealium, Prebid, Google Consent Mode v2, Salesforce DMP, Piano Analytics and other tag managers and SSPs.

- **Human URL:** [https://developers.didomi.io/cmp/web-sdk](https://developers.didomi.io/cmp/web-sdk)

#### Tags

- Consent
- JavaScript
- SDK
- Web

#### Properties

- [Documentation](https://developers.didomi.io/cmp/web-sdk)
- [Getting Started](https://developers.didomi.io/cmp/web-sdk/getting-started)
- [API Reference](https://developers.didomi.io/cmp/web-sdk/reference/api)
- [Events](https://developers.didomi.io/cmp/web-sdk/reference/events)
- [Versioning](https://developers.didomi.io/cmp/web-sdk/reference/versions)
- [Performance](https://developers.didomi.io/cmp/web-sdk/performance)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Didomi Android SDK

Didomi's Android and Android TV SDK delivers native consent notices, preference popups, and TCF / GPP / Didomi consent string generation in Java / Kotlin / Jetpack Compose apps. It shares consent with WebViews, bridges to Google Consent Mode v2, and ships with sample apps in Java, Kotlin, and Compose.

- **Human URL:** [https://developers.didomi.io/cmp/mobile-sdk/android](https://developers.didomi.io/cmp/mobile-sdk/android)

#### Tags

- Android
- Android TV
- Consent
- Mobile
- SDK

#### Properties

- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/android)
- [Getting Started](https://developers.didomi.io/cmp/mobile-sdk/android/setup)
- [API Reference](https://developers.didomi.io/cmp/mobile-sdk/android/reference/api)
- [Events](https://developers.didomi.io/cmp/mobile-sdk/android/reference/events)
- [Versioning](https://developers.didomi.io/cmp/mobile-sdk/android/versions)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Didomi iOS SDK

The iOS / tvOS / Mac Catalyst SDK renders Didomi consent notices and preference centers natively in Swift and Objective-C apps, coordinates Apple's App Tracking Transparency (ATT) prompt with consent, shares consent with WebViews, and emits TCF / GPP / Didomi consent strings. Distributed via Swift Package Manager (github.com/didomi/didomi-ios-sdk-spm) and CocoaPods.

- **Human URL:** [https://developers.didomi.io/cmp/mobile-sdk/ios](https://developers.didomi.io/cmp/mobile-sdk/ios)

#### Tags

- Consent
- iOS
- Mobile
- SDK
- tvOS

#### Properties

- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/ios)
- [Getting Started](https://developers.didomi.io/cmp/mobile-sdk/ios/setup)
- [API Reference](https://developers.didomi.io/cmp/mobile-sdk/ios/reference/api)
- [Events](https://developers.didomi.io/cmp/mobile-sdk/ios/reference/events)
- [Versioning](https://developers.didomi.io/cmp/mobile-sdk/ios/versions)
- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/ios/app-tracking-transparency-ios-14)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Didomi Cross-Platform SDKs (React Native, Flutter, Unity, Vega OS, AMP)

Didomi maintains first-party CMP plugins for React Native, Flutter, Unity (games and game consoles), Vega OS (LG webOS smart TVs), and Google AMP. Each wraps the platform's notice rendering, consent storage, event bus, and consent-string generation so cross-platform teams ship one consent UX across browser, native mobile, CTV, in-game, and AMP surfaces.

- **Human URL:** [https://developers.didomi.io/cmp/mobile-sdk](https://developers.didomi.io/cmp/mobile-sdk)

#### Tags

- AMP
- Consent
- Cross-Platform
- Flutter
- React Native
- SDK
- Unity
- Vega OS

#### Properties

- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/react-native)
- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/flutter)
- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/unity-sdk)
- [Documentation](https://developers.didomi.io/cmp/mobile-sdk/vega-os)
- [Documentation](https://developers.didomi.io/cmp/amp)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Didomi Consent String Toolkit

Open-source libraries published under github.com/didomi for encoding, decoding, and validating the Didomi consent string and the IAB TCF v2 consent string. Includes TypeScript (`consent-string`, `consent-string-schema`), Rust with C/Java FFI (`consent-string-decoder-rust`), Go (`consent-string-golang`), and a fork of the official IAB tooling (`iabtcf-es`). Useful for server-side auditing, downstream ad-tech reading consent state, and offline analysis.

- **Human URL:** [https://developers.didomi.io/cmp/didomi-consent-string](https://developers.didomi.io/cmp/didomi-consent-string)

#### Tags

- Consent String
- Decoder
- Encoder
- IAB TCF
- Toolkit

#### Properties

- [Documentation](https://developers.didomi.io/cmp/didomi-consent-string)
- [Documentation](https://developers.didomi.io/cmp/didomi-consent-string/didomi-consent-string-structure)
- [Documentation](https://developers.didomi.io/cmp/didomi-consent-string/consent-string-examples)
- [GitHub Repository](https://github.com/didomi/consent-string)
- [GitHub Repository](https://github.com/didomi/consent-string-schema)
- [GitHub Repository](https://github.com/didomi/consent-string-decoder-rust)
- [GitHub Repository](https://github.com/didomi/consent-string-golang)
- [GitHub Repository](https://github.com/didomi/iabtcf-es)
- [Postman Collection](collections/didomi-platform-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/didomi-platform-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Arazzo Workflows](arazzo/) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Portal](https://www.didomi.io)
- [Documentation](https://developers.didomi.io/)
- [Documentation](https://developers.didomi.io/readme)
- [Getting Started](https://developers.didomi.io/cmp/web-sdk/getting-started)
- [Console](https://console.didomi.io)
- [Sign Up](https://www.didomi.io/contact-us)
- [Pricing](https://www.didomi.io/offers)
- [Terms of Service](https://www.didomi.io/legal-notice)
- [Privacy Policy](https://www.didomi.io/privacy-policy)
- [Cookie Policy](https://www.didomi.io/cookie-policy)
- [Status Page](https://status.didomi.io)
- [Blog](https://www.didomi.io/blog)
- [Support](https://support.didomi.io)
- [Training](https://www.didomi.io/didomi-academy)
- [LinkedIn](https://www.linkedin.com/company/didomi)
- [GitHub Organization](https://github.com/didomi)
- [SDK](https://www.npmjs.com/package/@didomi/react)
- [SDK](https://github.com/didomi/react-native)
- [SDK](https://github.com/didomi/flutter)
- [SDK](https://github.com/didomi/unity)
- [SDK](https://github.com/didomi/didomi-ios-sdk-spm)
- [Tool](https://github.com/didomi/gtm-template)
- [Tool](https://github.com/didomi/magento)
- [Tool](https://github.com/didomi/mparticle-javascript-integration-didomi)
- [Tool](https://github.com/didomi/firebase)
- [Code Examples](https://github.com/didomi/samples)
- [Code Examples](https://github.com/didomi/boilerplate-fastly-reverse-proxy-didomi-cmp)
- [Code Examples](https://github.com/didomi/boilerplate-aws-cloudfront-reverse-proxy-didomi-cmp)
- [Code Examples](https://github.com/didomi/boilerplate-cloudflare-reverse-proxy-didomi-cmp)
- [JSON-LD](json-ld/didomi-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Spectral Rules](rules/didomi-rules.yml)
- [Vocabulary](vocabulary/didomi-vocabulary.yml)
- [Plans](plans/didomi-plans-pricing.yml)
- [Rate Limits](rate-limits/didomi-rate-limits.yml)
- [Fin Ops](finops/didomi-finops.yml)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [Solutions](undefined)

## Maintainers

**FN:** API Evangelist
**Email:** info@apievangelist.com
**URL:** https://apievangelist.com
