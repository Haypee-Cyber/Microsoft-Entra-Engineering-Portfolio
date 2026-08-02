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
---

# Enterprise Scenario

## Scenario

A software vendor requests the following Microsoft Graph permissions for a new HR application:

- User.Read
- User.Read.All
- Directory.ReadWrite.All

Business justification provided:

> "The application only needs to display the signed-in user's profile."

---

## Security Assessment

### User.Read

✅ Approved

Reason:

- Meets the stated business requirement.
- Allows the application to read only the signed-in user's profile.
- Follows the Principle of Least Privilege.

---

### User.Read.All

⚠️ Not approved immediately.

Reason:

- Grants access to every user's profile.
- Exceeds the stated business requirement.
- Additional technical and business justification required.

---

### Directory.ReadWrite.All

❌ Not approved.

Reason:

- Provides highly privileged access to the Microsoft Entra directory.
- No evidence that write access is required.
- Represents unnecessary risk if compromised.

---

## Recommendation

Approve only **User.Read**.

Request further justification for any additional permissions before approval.
---

# SOC Investigation Scenario

## Alert

A Microsoft Entra audit log generates the following events:

- A new Client Secret was created.
- A new Redirect URI was added.
- Directory.ReadWrite.All permission was granted.

---

## Investigation Process

### 1. Review Audit Logs

Identify:

- Who performed the changes.
- When the changes occurred.
- Which application was modified.

---

### 2. Review Sign-in Logs

Verify:

- Source IP Address
- Geographic location
- Device information
- User authentication method

---

### 3. Validate User Privileges

Determine:

- Was the user authorised to make the changes?
- Was Privileged Identity Management (PIM) used?
- Was the role activated legitimately?

---

### 4. Review Change Management

Confirm:

- CAB approval
- RFC or Change Request
- Business justification
- Expected maintenance window

---

### 5. Assess Risk

Determine whether:

- The Redirect URI points to a trusted domain.
- The Client Secret creation was expected.
- The granted permissions follow the Principle of Least Privilege.

---

## Outcome

If the changes are not supported by an approved business requirement, treat the activity as potentially suspicious, revoke unnecessary permissions, rotate exposed secrets if required, and escalate according to the organisation's incident response process.
---

# Common Misconfigurations

## 1. Excessive Microsoft Graph Permissions

### Problem

Applications request more Microsoft Graph permissions than required.

### Risk

Violates the Principle of Least Privilege and increases the impact if the application is compromised.

### Recommendation

Approve only the minimum permissions required to meet the business requirement.

---

## 2. Redirect URI Misconfiguration

### Problem

Redirect URI points to an incorrect or untrusted domain.

### Risk

May allow authentication responses to be redirected to an unintended location.

### Recommendation

Only configure Redirect URIs that belong to trusted and approved domains.

---

## 3. Long-Lived Client Secrets

### Problem

Client Secrets are created with unnecessarily long expiry periods.

### Risk

If exposed, the secret remains valid for an extended period, increasing organisational risk.

### Recommendation

Use the shortest practical lifetime and rotate secrets regularly. Where possible, use Certificates instead of Client Secrets.

---

## 4. Overuse of Directory.ReadWrite.All

### Problem

Applications request Directory.ReadWrite.All without a valid business requirement.

### Risk

Provides highly privileged access to Microsoft Entra ID.

### Recommendation

Challenge the requirement and approve only if a documented business need exists.

---

## 5. Failure to Review Admin Consent

### Problem

Admin Consent is granted without verifying the application's purpose or requested permissions.

### Risk

Applications may receive unnecessary access to organisational data.

### Recommendation

Always validate the business justification, publisher, requested permissions and apply the Principle of Least Privilege.
