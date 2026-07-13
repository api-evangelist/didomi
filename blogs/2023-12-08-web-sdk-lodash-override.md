---
title: "Web SDK - lodash override"
url: "https://status.didomi.io/incidents/nsb0z4kjfwr3"
date: "2023-12-08"
feed_url: "https://status.didomi.io/history.atom"
---
Dec 8 , 06:00 UTC Resolved - From 12/7/2023 5:16pm UTC to 12/8/2023 10:50am UTC, the Didomi Web SDK included the latest version of the lodash library. This update may cause compatibility issues for clients who were using an earlier version of lodash that loaded prior to the instantiation of the Web SDK. In such cases, the Web SDK lodash version could override the website version, potentially leading to breaking changes in some of lodash's APIs and in some functionalities of websites.
