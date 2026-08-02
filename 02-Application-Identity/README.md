# Application Identity

## Executive Summary

Application Identity is the process of creating and managing an application's identity in Microsoft Entra ID.

An App Registration enables Microsoft Entra to uniquely identify an application, authenticate it, and authorise it to access protected Microsoft resources securely.

---

## Business Problem

Modern enterprise applications require secure access to Microsoft 365 services such as Microsoft Graph, Exchange Online, SharePoint Online and Teams.

Without a trusted identity, applications cannot securely authenticate or request permissions.

---

## Technical Solution

Microsoft Entra ID provides App Registrations which create an identity for applications.

Each App Registration receives:

- Application (Client) ID
- Object ID
- Directory (Tenant) ID

These identities enable secure authentication using Client Secrets or Certificates together with Microsoft Entra authentication.

---

## Skills Demonstrated

- App Registration
- Application Identity
- Client Secret Management
- Redirect URI Configuration
- API Permissions
- Microsoft Graph
- Least Privilege
- OAuth 2.0
- OpenID Connect
---

# Architecture

## Components

Application Identity consists of:

- App Registration
- Enterprise Application (Service Principal)
- Microsoft Entra ID
- Microsoft Graph
- OAuth 2.0 / OpenID Connect
- Client Secret or Certificate

---

## Authentication Flow

```text
Application
      │
      │ Requests authentication
      ▼
Microsoft Entra ID
      │
      │ Verifies identity
      ▼
Issues ID Token / Access Token
      │
      ▼
Application gains access to Microsoft Graph
```
---

# Home Lab Implementation

## Objective

Create and configure a Microsoft Entra App Registration to understand how applications authenticate and securely access Microsoft resources.

## Lab Activities Completed

- Created an App Registration
- Reviewed Application (Client) ID
- Reviewed Object ID
- Reviewed Directory (Tenant) ID
- Configured Redirect URI
- Created a Client Secret
- Reviewed API Permissions
- Reviewed Token Configuration
- Reviewed Expose an API
- Reviewed Manifest

## Skills Gained

- Creating App Registrations
- Understanding Application Identity
- Configuring Redirect URIs
- Managing Client Secrets
- Reviewing Microsoft Graph Permissions
- Applying Least Privilege
---

# Daily Contractor Tasks

A Microsoft Entra Engineer working with Application Identity may be responsible for:

- Reviewing new App Registration requests.
- Creating App Registrations for internal applications.
- Configuring Redirect URIs.
- Creating and rotating Client Secrets.
- Replacing Client Secrets with Certificates where appropriate.
- Reviewing Microsoft Graph API permissions.
- Applying the Principle of Least Privilege.
- Reviewing Admin Consent requests.
- Investigating failed application authentication.
- Troubleshooting OAuth and OpenID Connect issues.
- Reviewing Audit Logs for application changes.
- Supporting application onboarding to Microsoft Entra ID.
- Producing technical documentation.
- Supporting CAB (Change Advisory Board) reviews.
- Advising developers on secure authentication design.

---

# Business Value

Application Identity enables organisations to securely integrate internal and third-party applications with Microsoft Entra ID while maintaining strong authentication, authorisation and governance controls.

Correct implementation reduces security risk, supports Zero Trust principles and improves operational efficiency.
