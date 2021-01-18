---
title: Preview and test the SAML Assertion Inline Hook
---

The SAML Assertion Inline Hook is ready for preview and testing. You now have the following applications configured:

- The SAML application (okta-spring-security-saml-db-example) is ready to sign in and authenticate users using your Okta org as an IdP.
- The external service (Glitch.com project) is ready with code to receive and respond to an Okta SAML Assertion Inline Hook call.
- The Okta org is setup to call the external service when a SAML Assertion Inline Hook is triggered by a user sign-in from the SAML application, and is ready to receive a response.

## Preview

To preview the SAML Assertion Inline Hook:

1. Navigate to Inline Hooks (**Workflow** > **Inline Hooks**) in your Admin Console.
2. Click on the SAML Assertion Inline Hook name (in this example, "Patient SAML Hook").
3. Click the **Preview** tab.
4. Select a user assigned to your SAML application in the first block titled **Configure Inline Hook request**; that is, a value for the `data.userProfile` field.
5. Select your SAML Application by searching in the **Select a SAML app** field (in this example, "Spring Book DB/SAML").
6. From the **Preview example Inline Hook request"** block, click **Generate Request**.
    You should see the user's request information in JSON format that is sent to the external service.
    
    > **Note:** You can also **Edit** this call for testing purposes.
7. From the **View service's response** block, click **View Response**.
    You will see the response from your external service in JSON format, which either adds a claim to the SAML assertion or not.

## Test

To run a test of your SAML Assertion Inline Hook:

1. Start your SAML Application (`> mvn spring-boot:run` in your project folder `okta-spring-security-saml-db-example >`).

2. Navigate to your sample application (`http:/localhost:8080`).

3. Navigate to your Glitch.com project to make sure it is listening for requests; open the Console Logs window (**Tools** > **Logs**).

4. Return to your SAML application and sign in with an Okta user who is NOT in the Patients data store.

    The user should sign in as normal; only the user name should appear in the Glitch log window.
5. Sign out of the sample application and now sign in with an Okta user who IS in the Patients data store.

    The user should sign in as normal; however, this user should have a patient ID displayed in the Glitch console output, as well as a successful implementation record of the SAML Assertion Inline Hook, available for review in your Okta org's System Log (**Reports** > **System Log**).

> **Note:** Review the [Troubleshooting hook implementations](/data/guides/common-hook-set-up-steps/troubleshooting) section for information on any difficulties.

<!-- <StackSelector snippet="preview"/> -->