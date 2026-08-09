# Microsoft Entra Enterprise Applications

## Overview

This project demonstrates the implementation, security, governance and troubleshooting of Enterprise Applications in Microsoft Entra ID.

The lab covers application onboarding, SAML-based Single Sign-On, user and group assignment, application permissions, monitoring and investigation of common Enterprise Application incidents. SCIM provisioning is also examined as an identity lifecycle management capability.

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

SCIM provisioning was reviewed as part of the Enterprise Application identity lifecycle design. It was not configured end-to-end during this lab.

SCIM can automate identity lifecycle management between Microsoft Entra ID and supported SaaS applications.

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

In a production environment, Provisioning Logs would be reviewed when automated account creation, updates or deprovisioning fail.

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
---

## Monitoring and Troubleshooting

### Microsoft Entra Logs

| Log | Primary Use |
|---|---|
| Sign-in Logs | Investigate authentication attempts, failures and Conditional Access results |
| Audit Logs | Identify configuration changes, who performed them and when |
| Provisioning Logs | Investigate automated user provisioning and deprovisioning |

### Troubleshooting Principle

The scope of an issue helps determine the investigation path:

| Impact | Initial Investigation |
|---|---|
| Single user | User assignment, group membership, attributes and sign-in logs |
| Small group of users | Group assignment, policies and shared user attributes |
| All users | SSO configuration, certificates, Enterprise Application configuration and service health |

---

## Scenario 1 – SAML SSO Outage
> **Scenario:** The following simulated production incident demonstrates a structured approach to investigating and resolving a SAML SSO configuration failure.
### Incident

Approximately 200 developers were unable to access GitHub Enterprise Cloud through SSO following a configuration change.

### Investigation

1. Reviewed Microsoft Entra Audit Logs.
2. Identified a change to the SAML Basic Configuration.
3. Confirmed that the Reply URL (ACS URL) had been modified.
4. Compared the new value against the expected GitHub ACS URL.
5. Confirmed that the previous Reply URL was correct.

### Root Cause

An incorrect Reply URL was entered during an approved configuration change.

### Resolution

The validated Reply URL was restored and SSO was tested successfully.

### Evidence

- Audit Log showing the SAML configuration change
- Corrected SAML configuration
- Successful post-change Sign-in Logs
- User confirmation of restored GitHub access

### Preventive Controls

- Peer review SAML configuration changes before implementation.
- Perform SSO validation immediately after changes.
- Maintain appropriate change and rollback procedures.

---

## Scenario 2 – Excessive Application Permission

### Incident

An unknown third-party application was discovered with `Directory.ReadWrite.All` and no documented business justification.
> **Scenario:** The following simulated security incident demonstrates an investigation and containment approach for an application holding excessive Microsoft Entra ID permissions.
### Investigation

The investigation should establish:

- Application and publisher identity
- Application owner
- Permission type
- Administrator who granted consent
- Time of consent
- Related Audit Log activity
- Service Principal sign-in activity
- Directory objects accessed or modified

### Containment

Where activity is confirmed as unauthorised:

1. Contain the compromised administrator identity.
2. Disable the malicious or compromised service principal where appropriate.
3. Revoke unauthorised permissions and consent.
4. Revoke affected sessions and credentials as required.
5. Investigate directory changes made while the permission was available.

### Security Principle

Application identities must be treated as security principals. Disabling a compromised administrator does not automatically stop an application operating with previously granted Application permissions.

---

## Lessons Learned

- Enterprise Applications represent service principals within the tenant.
- App Registrations primarily define application identity and authentication configuration, while Enterprise Applications manage how the application operates within the tenant.
- Group-based assignment provides more scalable access management than individual assignments.
- SAML configuration requires a valid trust relationship between the Identity Provider and Service Provider.
- SCIM supports automated Joiner-Mover-Leaver identity lifecycle management.
- High-privilege API permissions require business justification and least-privilege review.
- Sign-in, Audit and Provisioning logs provide different evidence and should be selected according to the incident being investigated.
- Troubleshooting should begin with evidence and the scope of impact rather than assumptions.
