# Application Identity
# Executive Summary

Application Identity enables applications to securely authenticate with Microsoft Entra ID and access protected Microsoft resources such as Microsoft Graph, Exchange Online, SharePoint Online and Microsoft Teams.

Microsoft Entra App Registrations provide each application with a unique identity, enabling secure authentication, authorisation and lifecycle management. Correct implementation supports Zero Trust principles by enforcing strong authentication, least privilege and controlled access to organisational resources.

Application Identity is a core capability for Microsoft Entra Engineers responsible for enterprise application integration, governance, security and operational support.

---

# Business Requirement

Modern organisations use hundreds or thousands of internal and third-party applications that require secure access to Microsoft services and organisational data.

Without a central identity platform, applications may use inconsistent authentication methods, excessive permissions and unmanaged credentials, increasing the risk of unauthorised access and security breaches.

Microsoft Entra ID provides a centralised identity platform that enables organisations to securely register, authenticate, authorise and govern applications throughout their lifecycle.
---

# Microsoft Solution

Microsoft Entra ID provides App Registrations to establish a trusted identity for applications.

Each App Registration receives a globally unique Application (Client) ID and is associated with a Microsoft Entra tenant. The application can then authenticate using a Client Secret, Certificate or Managed Identity and request access to protected resources through Microsoft Graph or other APIs.

Application permissions, Redirect URIs, authentication settings and token configuration are centrally managed to support secure application integration and governance.
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


## Security Assessment

### User.Read

✅ Approved

Reason:

- Meets the stated business requirement.
- Allows the application to read only the signed-in user's profile.
- Follows the Principle of Least Privilege.

---
# Operational Responsibilities

A Microsoft Entra Engineer responsible for Application Identity may perform the following activities:

## Application Onboarding

- Create App Registrations.
- Configure Redirect URIs.
- Configure authentication settings.
- Configure API permissions.
- Configure Client Secrets or Certificates.

## Governance

- Review Microsoft Graph permissions.
- Apply the Principle of Least Privilege.
- Review Admin Consent requests.
- Assess business justification for privileged permissions.
- Participate in Change Advisory Board (CAB) reviews.

## Security

- Rotate Client Secrets.
- Replace Client Secrets with Certificates where appropriate.
- Review Microsoft Entra Audit Logs.
- Investigate suspicious application changes.
- Review authentication failures.

## Operations

- Troubleshoot application authentication.
- Support developers integrating Microsoft Entra ID.
- Maintain implementation documentation.
- Review application lifecycle and ownership.
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
# Implementation Evidence

The following screenshots demonstrate the successful implementation of Application Identity within the Microsoft Entra home lab.

| Configuration | Evidence |
|---------------|----------|
| App Registration | See `images/app-registration-overview.png` |
| Authentication | See `images/authentication.png` |
| Client Secret | See `images/certificates-and-secrets.png` |
| API Permissions | See `images/api-permissions.png` |
| Token Configuration | See `images/token-configuration.png` |
| Expose an API | See `images/expose-api.png` |
| Manifest | See `images/manifest.png` |
# Security Review

## Security Principles

Application Identity should be implemented in accordance with the following principles:

- Least Privilege
- Zero Trust
- Secure by Default
- Defence in Depth

## Security Controls

- Use Certificates where appropriate instead of long-lived Client Secrets.
- Configure only trusted Redirect URIs.
- Review Microsoft Graph permissions regularly.
- Enable audit logging.
- Rotate credentials regularly.
- Review Admin Consent before approval.

## Risks

| Risk | Mitigation |
|------|------------|
| Excessive API permissions | Apply Least Privilege |
| Client Secret compromise | Rotate secrets and prefer Certificates |
| Redirect URI misuse | Configure only approved domains |
| Unauthorised Admin Consent | Governance and approval workflow |
# Governance

## Governance Objectives

Application Identity should be governed throughout its lifecycle to ensure secure, compliant and auditable access to organisational resources.

## Governance Activities

- Review all new App Registration requests.
- Validate business justification before implementation.
- Apply the Principle of Least Privilege.
- Review and approve Microsoft Graph permissions.
- Review Admin Consent requests.
- Define application ownership.
- Review application permissions periodically.
- Rotate Client Secrets in accordance with organisational policy.
- Remove unused App Registrations.
- Maintain implementation documentation.

## Change Management

Any of the following changes should follow the organisation's change management process:

- New App Registration
- Redirect URI changes
- Client Secret creation or renewal
- Certificate replacement
- API permission changes
- Admin Consent approval

## Governance Checklist

| Activity | Status |
|----------|--------|
| Business justification reviewed | ✓ |
| Least Privilege applied | ✓ |
| Application owner identified | ✓ |
| Security review completed | ✓ |
| Change approved | ✓ |
| Documentation updated | ✓ |
# Troubleshooting

## Common Issues

| Issue | Possible Cause | Resolution |
|------|----------------|------------|
| Application sign-in fails | Incorrect Redirect URI | Verify the Redirect URI matches the application configuration. |
| Invalid client secret | Expired or incorrect Client Secret | Generate a new Client Secret and update the application. |
| Access denied to Microsoft Graph | Missing API permissions or Admin Consent | Review API permissions and grant Admin Consent where appropriate. |
| Users unable to sign in | Incorrect supported account type | Verify the App Registration account type configuration. |
| Authentication succeeds but API calls fail | Insufficient Microsoft Graph permissions | Review delegated or application permissions and apply Least Privilege. |
| Application authentication suddenly stops | Certificate or Client Secret expired | Replace the expired credential and validate authentication. |

## Investigation Checklist

When investigating an Application Identity issue:

- Review Microsoft Entra Audit Logs.
- Review Sign-in Logs.
- Verify the App Registration configuration.
- Review Redirect URI configuration.
- Validate API permissions.
- Confirm Admin Consent status.
- Verify Client Secret or Certificate validity.
- Confirm the application owner.
- Review recent configuration changes.
# Lessons Learned

- Every application requires a unique identity before it can authenticate with Microsoft Entra ID.
- Redirect URIs are a security control and should only reference trusted endpoints.
- Client Secrets should be treated as sensitive credentials and rotated regularly.
- Certificates are generally preferred over long-lived Client Secrets for production environments.
- Microsoft Graph permissions should always follow the Principle of Least Privilege.
- App Registration changes should be governed through change management and documented.
- Audit Logs and Sign-in Logs are essential when investigating Application Identity incidents.
