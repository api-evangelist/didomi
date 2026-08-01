---
title: "Elevated API and Console errors"
url: "https://status.didomi.io/incidents/kdv2283kyqmt"
date: "2026-07-21"
feed_url: "https://status.didomi.io/history.atom"
---
Jul 21 , 20:00 UTC Resolved - Between 19:38 and 20:13 UTC on July 21, 2026, some requests to our Admin API and REST API returned 5xx errors, and the Didomi Console was intermittently unavailable. The cause was a short-lived spike in traffic from a single integration that temporarily saturated shared capacity. Our real-time Consents API continued to operate normally throughout.
