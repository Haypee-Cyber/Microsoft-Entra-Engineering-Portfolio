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
