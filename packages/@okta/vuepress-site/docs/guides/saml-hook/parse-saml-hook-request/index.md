---
title: Parse the SAML Assertion Inline Hook request
---

The external service in this scenario requires code to handle the SAML Assertion Inline Hook request from the Okta org. Use the Glitch example to either build or copy the code (re-mix on Glitch) that parses the SAML Assertion Inline Hook call.

> **Note:** Make sure to have the required default code and packages in your Glitch project. See [Common Hook Set-up Steps](/docs/guides/common-hook-set-up-steps/nodejs/overview).

From the SAML Assertion Inline Hook request, the code retrieves the name of the user, who is authenticating, from the `data.context.user` object.

<StackSelector snippet="parse"/>

<NextSectionLink/>