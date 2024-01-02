---
title: "Set up Single Sign On (SSO) for Azure Active Directory"
description: "Configure an Azure Active Directory Enterprise Application for SAML-based Single Sign-On."
ispublished: false 
---

Description of the document:
- This document describes how to set up SSO into Skillable with an Active Directory Enterprise Application using SAML

## In this Article

- [Required Permissions](#required-permissions)
- [Set up Single Sign On (SSO) for Azure Active Directory](#set-up-single-sign-on-sso-for-azure-active-directory)
    - [Create an Azure Active Directory Enterprise App](#create-an-azure-active-directory-enterprise-app)
    - [Modify Application Configuration for Single Sign On with SAML](#modify-application-configuration-for-single-sign-on-with-saml)
        - [Basic SAML Configuration](#basic-saml-configuration)
        - [User Attributes and Claims](#user-attributes-and-claims)
    - [Application Setup with Skillable](#application-setup-with-skillable)
- [Best Practices](#best-practices) 
- [Next Steps](#next-steps)

## Required Permissions

To setup SSO to Skillable using Active Directory, you must have access to your Active Directory Enterprise Application account, and at least a **Basic User** role in your Organization's Skillable account. 

## Set Up Single Sign On (SSO) for Azure Active Directory
**Note**: While this document describes the steps to configure Azure AD to support SSO authentication via SAML, any SAML Identity Provider should be able to be configured using the steps described. 

SAML is an open standard that allows Identity Providers (IdP) and Service Providers (SP) to send authorization credentials to each other, to authenticate a user. This allows using one set of credentials to log in to multiple services and/or websites.

### Create an Azure Active Directory Enterprise App

If your Identity Provider is Azure, you must create an Enterprise Application in Azure Active Directory.

1. In Azure, **navigate to the Enterprise Applications** section. You can get to this by searching for Enterprise Application in the top search bar in Azure.

2. Select **New application** in the upper-left corner of the page.

3. Select **Create your own application.**

4. Provide a **name** for your application.

5. Select the option to **Integrate any other application you don't find in the gallery (non-gallery).**

6. Select **Create.**

### Modify Application Configuration for Single Sign On with SAML

1. **Navigate to your application**, if you are not there already.

2. Select **Set up single sign on.**

3. Select **SAML.**

#### Basic SAML Configuration

1. Select the **Edit** button on the **Basic SAML Configuration** section.

2. **Add** the following Configuration values for each platform.

<blockquote class="note">
Replace the following information in the URL before configuring these values:

**Skillable Studio**
- Sign on URL: replace {customer} with your customer name.

**Training Management System:**
- Sign on URL: replace {TMS-Site} with your TMS site.
- Logout URL: replace {TMS-Site} with your TMS site.

**Insights:**
- Sign on URL: replace {customer} with your customer name.
</blockquote>

### Skillable Studio
<table>
    <thead>
        <tr>
            <th style="text-align:left;">Name</th>
            <th style="text-align:left;">Description</th>
            <th style="text-align:left;">Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="text-align:left;">Unique Identifier (Entity ID)</td>
            <td style=text-align:left;">This value must be unique across all applications in your Azure Active Directory tenant.</td>
            <td style="text-align:left;">"https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_portal"</td>
        </tr>
        <tr>
            <td style="text-align:left;">Reply URL (Asserstion Consumer Service URL)</td>
            <td style="text-align:left;">The reply URL is where the application expects to receive the authentication token. This is also referred to as the "Assertion Consumer Service" (ACS) in SAML.</td>
            <td style="text-align:left;">https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_TMS/samlp/sso/assertionconsumer</td>
        </tr>
        <tr>
            <td style="text-align:left;"> Sign on URL</td>
            <td style="text-align:left;"> This URL contains the sign-in page for this application that will perform the service provider-initiated single sing-on.</td>
            <td style="text-align:left;"> https://portal.learnondemandsystems.com/Authentication/SamlIdpRedirect?idp=B2C_1A_signup_signin_TMS_SAML-PROD-{Customer}</td>
        </tr>
        <tr>
            <td style="text-align:left;"> Relay State</td>
            <td style="text-align:left;"> Leave this blank. Configuring Relay State is not neccessary for this configuration.</td>
            <td style="text-align:left;">N/A</td>
        </tr>
        <tr>
            <td style="text-align:left;">Logout URL</td>
            <td style="text-align:left;">This URL is used to send the SAML Logout response back to the application.</td>
            <td style="text-align:left;">https://portal.learnondemandsystems.com/Authentication/LogOut</td>
        </tr>
    </tbody>
</table>

### Training Management System (TMS)

<table>
<thead>
<tr>
<th style="text-align:left;">Name</th>
<th style="text-align:left;">Description</th>
<th style="text-align:left;">Example</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">Unique Identifier (Entity ID)</td>
<td style="text-align:left;">This value must be unique across all applications in your Azure Active Directory tenant.</td>
<td style="text-align:left;">https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_TMS</td>
</tr>
<tr>
<td style="text-align:left;">Reply URL (Assertion Consumer Service URL)</td>
<td style="text-align:left;">The reply URL is where the application expects to receive the authentication token. This is also referred to as the "Assertion Consumer Service" (ACS) in SAML.</td>
<td style="text-align:left;">https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_TMS/samlp/sso/assertionconsumer</td>
</tr>
<tr>
<td style="text-align:left;">Sign on URL</td>
<td style="text-align:left;">This URL contains the sign-in page for this application that will perform the service provider-initiated single sing-on.</td>
<td style="text-align:left;">https://{TMS-Site}.learnondemand.net/User/CurrentTraining (or any designated landing page)</td>
</tr>
<tr>
<td style="text-align:left;">Relay State</td>
<td style="text-align:left;">Leave this blank. Configuring Relay State is not neccessary for this configuration.</td>
<td style="text-align:left;">N/A</td>
</tr>
<tr>
<td style="text-align:left;">Logout Url</td>
<td style="text-align:left;">This URL is used to send the SAML Logout response back to the application.</td>
<td style="text-align:left;">https://{TMS-Site}.learnondemand.net/User/Logout</td>
</tr>
</tbody>
</table>

### Insights

<table>
<thead>
<tr>
<th style="text-align:left;">Name</th>
<th style="text-align:left;">Description</th>
<th style="text-align:left;">Example</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">Unique Identifier (Entity ID)</td>
<td style="text-align:left;">This value must be unique across all applications in your Azure Active Directory tenant.</td>
<td style="text-align:left;">https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_portal</td>
</tr>
<tr>
<td style="text-align:left;">Reply URL (Assertion Consumer Service URL)</td>
<td style="text-align:left;">The reply URL is where the application expects to receive the authentication token. This is also referred to as the "Assertion Consumer Service" (ACS) in SAML.</td>
<td style="text-align:left;">https://learnondemandsystemsb2c.b2clogin.com/learnondemandsystemsb2c.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions_TMS/samlp/sso/assertionconsumer</td>
</tr>
<tr>
<td style="text-align:left;">Sign on URL</td>
<td style="text-align:left;">This URL contains the sign-in page for this application that will perform the service provider-initiated single sing-on.</td>
<td style="text-align:left;">https://portal.learnondemandsystems.com/Authentication/SamlIdpRedirect?idp=B2C_1A_signup_signin_TMS_SAML-PROD-{Customer}</td>
</tr>
<tr>
<td style="text-align:left;">Relay State</td>
<td style="text-align:left;">Leave this blank. Configuring Relay State is not neccessary for this configuration.</td>
<td style="text-align:left;">N/A</td>
</tr>
<tr>
<td style="text-align:left;">Logout Url</td>
<td style="text-align:left;">This URL is used to send the SAML Logout response back to the application.</td>
<td style="text-align:left;">https://portal.learnondemandsystems.com/Authentication/LogOut</td>
</tr>
</tbody>
</table>

### User Attributes and Claims
1. Ensure the following **User Attributes are configured.**

<table>
<thead>
<tr>
<th>Attribute Name</th>
<th style="text-align:left;">Attribute Syntax</th>
</tr>
</thead>
<tbody>
<tr>
<td>Givenname</td>
<td style="text-align:left;"><code title="Copy to clipboard" class="prettyprint">user.givenname</code></td>
</tr>
<tr>
<td>Surname</td>
<td style="text-align:left;"><code title="Copy to clipboard" class="prettyprint">user.surname</code></td>
</tr>
<tr>
<td>Emailaddress</td>
<td style="text-align:left;"><code title="Copy to clipboard" class="prettyprint">user.mail</code></td>
</tr>
<tr>
<td>Name</td>
<td style="text-align:left;"><code title="Copy to clipboard" class="prettyprint">user.userprincipalname</code></td>
</tr>
<tr>
<td>Unique User Identifier</td>
<td style="text-align:left;"><code title="Copy to clipboard" class="prettyprint">user.userprincipalname</code></td>
</tr>
</tbody>
</table>

2. If these are not configured, selecte the **Edit** button on the **User Attributes and Claims** section, and modify each value.

### Application Setup with Skillable

1. **Open a support ticket and provide Skillable with the following URLs** The values in these URLs will vary. The following is an example of how these may look. 
<table>
<thead>
<tr>
<th>Value Name</th>
<th style="text-align:left;">Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>SAML Single Sign-On Service URL</td>
<td style="text-align:left;">https://login.microsoftonline.com/{Tenant ID}/saml2</td>
</tr>
<tr>
<td>SAML Entity ID</td>
<td style="text-align:left;">https://sts.windows.net/{Tenant ID}/</td>
</tr>
<tr>
<td>Sign-Out URL</td>
<td style="text-align:left;">https://login.microsoftonline.com/{Tenant ID}/saml2</td>
</tr>
</tbody>
</table>

## Best Practices

Single sign-on (SSO) is not just about convenience, it’s also about security. An enterprise owns its employees identities in the cloud apps it uses and the enterprise should be able to effectively manage those identities.

For example, if a user leaves your organization, you may want to disable their ability to access Skillable labs, a few settings in your Azure Active Directory Enterprise Application can achieve this.

- Disallow password resets

Prevent a user from changing or resetting their password via email

- Disallow email address change

Don't let a user change their email address to a personal one.

## Next Steps





        



