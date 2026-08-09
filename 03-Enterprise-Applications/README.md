# Microsoft Entra Enterprise Applications

## Overview

This project demonstrates the implementation, security, governance and troubleshooting of Enterprise Applications in Microsoft Entra ID.

The lab covers application onboarding, SAML-based Single Sign-On, user and group assignment, SCIM provisioning, application permissions, monitoring and investigation of common Enterprise Application incidents.

## Business Scenario

An organisation is onboarding GitHub Enterprise Cloud into Microsoft Entra ID. Developers require secure Single Sign-On using their corporate identities, centrally managed access, automated identity lifecycle management and appropriate monitoring.

The implementation must follow least privilege principles and provide sufficient logging to support troubleshooting, security investigations and governance.
---

## Technical Implementation

### 1. Enterprise Application Onboarding

GitHub Enterprise Cloud was onboarded through the Microsoft Entra Enterprise Application Gallery.

The Enterprise Application creates a service principal within the tenant, allowing the organisation to manage how GitHub is accessed and governed.

Key configuration areas reviewed:

- Properties
- Owners
- Users and Groups
- Single Sign-On
- Provisioning
- Permissions
- Conditional Access
- Sign-in Logs
- Audit Logs
- Provisioning Logs

### 2. Single Sign-On

SAML was selected as the Single Sign-On protocol between Microsoft Entra ID and GitHub Enterprise Cloud.

The following SAML components were reviewed and configured:

| Component | Purpose |
|---|---|
| Entity ID | Uniquely identifies the service provider/application |
| Reply URL (ACS URL) | Endpoint where Entra sends the SAML authentication response |
| Attributes and Claims | Provides identity information required by the application |
| Token Signing Certificate | Allows the application to verify the authenticity and integrity of SAML assertions |

Microsoft Entra acts as the Identity Provider (IdP), while GitHub Enterprise Cloud acts as the Service Provider (SP).

### 3. User and Group Assignment

Application access should be managed using security groups rather than individual user assignments wherever practical.

Example:

`Developers Security Group → GitHub Enterprise Cloud`

This approach provides:

- Centralised access management
- Simplified onboarding and offboarding
- Reduced administrative overhead
- Consistent access assignment
- Improved governance and auditability

### 4. SCIM Provisioning

SCIM provisioning can automate the identity lifecycle between Microsoft Entra ID and supported SaaS applications.

The provisioning lifecycle includes:

`Joiner → Provision Account`

`Mover → Update Account`

`Leaver → Deprovision Account`

Typical attributes exchanged during provisioning include:

- Username
- Display name
- Given name
- Family name
- Email address

Provisioning logs should be reviewed when automated account creation, updates or deprovisioning fail.

### 5. Permissions and Admin Consent

High-privilege permissions must not be approved solely because an application requests them.

Before granting Admin Consent:

1. Verify the application and publisher.
2. Confirm the business requirement.
3. Determine whether the permission is Delegated or Application.
4. Assess the requested permission against least privilege.
5. Identify whether a narrower permission can satisfy the requirement.
6. Confirm the appropriate approval/change process has been followed.

Permissions such as `Directory.ReadWrite.All` require additional scrutiny because compromise of the application could expose or allow modification of directory resources.
