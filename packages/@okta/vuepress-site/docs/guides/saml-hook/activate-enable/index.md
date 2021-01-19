---
title: Activate and enable the SAML Assertion Inline Hook
---

The SAML Assertion Inline Hook must be activated and enabled within your Okta Admin Console.

Activating the SAML Assertion Inline Hook registers the hook with the Okta org and associates it with your external service. Enabling the SAML Assertion Inline Hook associates the hook with your SAML application.

To set up and activate the SAML Assertion Inline Hook:

1. Navigate to the **Workflow** > **Inline Hooks** page.

2. Click **Add Inline Hook** and select **SAML** from the drop-down menu.

3. Add a name for the hook (in this example, "Patient SAML Hook").

4. Add your external service URL, including the endpoint. For example, use your Glitch project name with the endpoint: `https://your-glitch-projectname.glitch.me/SAMLHook`.

5. Include authentication field and secret. In this example:

    - **Authentication field** = `authorization`
    - **Authentication secret** = `Basic YWRtaW46c3VwZXJzZWNyZXQ=`

6. Click **Save**.

The SAML Assertion Inline Hook is now set up with a status of active.

To enable the SAML Assertion Inline Hook:

1. Navigate to **Applications** and select your SAML application (in this example, "Spring Book DB/SAML").

2. Click the **General** tab.

3. From the **SAML Settings** tile, click **Edit**.

4. Click **Next** to get to the **Configure SAML** tab.

5. From the **SAML Settings**, **General** heading, click **Show Advanced Settings**.

6. In the **Assertion Inline Hook** field, select your registered Inline Hook (in this example, "Patient SAML Hook").

The SAML Assertion Inline Hook is now ready for triggering when a user authenticates through the SAML application.

<NextSectionLink/>