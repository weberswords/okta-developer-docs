---
title: Overview
---

The SAML Assertion Inline Hook can be used to customize the authentication workflow that occurs between an application and the Okta org, which functions as the Identity Provider (IdP).

This guide provides an end-to-end scenario using a SAML-authenticated application and an Okta org, and includes example code for an external service to respond to calls from a SAML Assertion Inline Hook triggered during the authentication workflow.

In the following scenario, the external service code parses a request from Okta, evaluates the user name against a simple patient data store, and, if the user is part of the patient store, responds to Okta with a command to add a patient ID claim to the SAML assertion. If the user name is not part of the data store, no action is taken.

At a high-level, the following workflow occurs:

- A user logs into an application authenticated by SAML, which uses the Okta org as an Identity Provider (IdP).
- The Okta org authenticates the user.
- At this point in the workflow, the Okta SAML Assertion Inline Hook triggers and sends a request to an external service.
- The external service evaluates the request, and if the user is a patient, adds a patient ID claim to the SAML assertion.
- The user is logged in to the application with the additional claim in the SAML assertion.

To implement this example, you also need to have a SAML-authenticated application. Set up the following [Spring Security + SAML and Database Authentication](https://github.com/oktadeveloper/okta-spring-security-saml-db-example) project. (See the next section for further details on this set up.)

This guide also uses the website Glitch.com to act as an external service and to implement the SAML Inline hook with an Okta org. See the following Glitch project to copy working code that implements the following example, or build your own using the code snippets:

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 420px; width: 100%;">
  <iframe
    src="https://glitch.com/embed/#!/embed/okta-inlinehook-samlhook?path=README.md&previewSize=0"
    title="okta-inlinehook-samlhook on Glitch"
    allow="geolocation; microphone; camera; midi; vr; encrypted-media"
    style="height: 100%; width: 100%; border: 0; padding-bottom: 35px">
  </iframe>
</div>

For further reference data on the SAML Inline Hook, see the [SAML Assertion Inline Hook Reference](/docs/reference/saml-hook/).

## Support

If you need help or have an issue, post a question in our [Developer Forum](https://devforum.okta.com).

<NextSectionLink/>