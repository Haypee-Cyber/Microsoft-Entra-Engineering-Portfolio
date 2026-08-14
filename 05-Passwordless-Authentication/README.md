# Module 05 – Passwordless Authentication

## Overview

This module demonstrates the implementation and validation of passwordless authentication in Microsoft Entra ID using Temporary Access Pass (TAP), passkeys, authentication strengths, Conditional Access, sign-in logs, and audit logs.

The lab follows the authentication lifecycle from initial user bootstrap through passkey registration and passwordless sign-in, followed by policy validation and credential lifecycle investigation.

## Objectives

- Configure Temporary Access Pass for secure user bootstrap
- Register a passkey for a test user
- Authenticate to Microsoft Entra ID using the passkey
- Verify the authentication method through Entra sign-in logs
- Configure a passkey-focused authentication strength
- Apply the authentication strength through Conditional Access
- Validate the Conditional Access policy in Report-only mode
- Investigate authentication credential lifecycle events using Entra audit logs

---

## 1. Temporary Access Pass – Passwordless Bootstrap
A Temporary Access Pass (TAP) was provisioned for the test user to provide a time-limited authentication method for bootstrapping passwordless authentication.

The TAP allowed the user to authenticate securely and register a passkey without relying on their existing password as the onboarding credential.

### Evidence
<img width="1640" height="906" alt="M5-TAP-Authentication-Details-Success" src="https://github.com/user-attachments/assets/263eb790-dd92-4163-b1a1-e952383a6616" />
---

## 2. Passkey Registration

After the initial bootstrap authentication, the test user registered a passkey as a passwordless authentication method.

The registration process created a FIDO2-based credential associated with the user, providing a phishing-resistant authentication method without requiring the user's password during subsequent sign-ins.

### Evidence
<img width="1646" height="787" alt="M5-S2-07-Passkey-Created-Successfully" src="https://github.com/user-attachments/assets/6b02d120-9f32-4e38-a46c-4a2ac2fee908" />
---

## 3. Verify Passkey Registration

After registration, the user's Security Info was reviewed to confirm that the passkey had been successfully added as an available authentication method.

This validation confirmed that the credential was associated with the test user's account and available for passwordless authentication.

### Evidence
<img width="1746" height="686" alt="M5-S2-08-Passkey-Registered-Security-Info" src="https://github.com/user-attachments/assets/3ab7c901-c9f5-4469-9ef8-2aed4136c598" />
---

## 4. Passwordless Sign-In

The registered passkey was then used to authenticate the test user without entering the account password.

The sign-in used the device authentication mechanism associated with the passkey, demonstrating passwordless access to Microsoft Entra ID.

### Evidence
<img width="1881" height="950" alt="M5-04-Passkey-Passwordless-SignIn-PIN" src="https://github.com/user-attachments/assets/30a5dda8-2229-4867-8c84-ddcf3d73a5c5" />
---

## 5. Verify Passkey Authentication in Sign-In Logs

Microsoft Entra sign-in logs were reviewed after the passwordless authentication test to verify which authentication method was actually used.

The Authentication Details showed **Passkey (synced)** with a successful result. This provides administrative evidence that Microsoft Entra ID processed the sign-in using the registered passkey.

### Evidence
<img width="985" height="400" alt="M5-S2-09-Passkey-SignIn-Authentication-Details" src="https://github.com/user-attachments/assets/75bbf818-a320-4443-b2d0-2165e50d5cd6" />
---

## 6. Configure Passkey Authentication Strength

A dedicated authentication strength was configured in Microsoft Entra ID to restrict authentication to passkey-based methods.

This authentication strength was designed for use with Conditional Access so that access could be evaluated against a stronger, phishing-resistant authentication requirement.

### Evidence
<img width="1903" height="965" alt="M5-Custom-Authentication-Strength-Passkey-Only" src="https://github.com/user-attachments/assets/1d794d42-ee12-4cb6-9bef-f2e2dce14cdd" />
---

## 7. Apply Authentication Strength through Conditional Access

A Conditional Access policy named **LAB - Require Passkey Authentication** was configured for the passwordless pilot.

The policy targeted the lab application and used the custom **Passwordless-Passkey-Only** authentication strength as its Grant requirement.

The policy was initially maintained in **Report-only** mode to validate its potential impact before enforcement.

### Evidence
<img width="1903" height="965" alt="M5-Custom-Authentication-Strength-Passkey-Only" src="https://github.com/user-attachments/assets/b6bdb7b8-94a5-442d-9cb4-86ca3bd4bb03" />
---

## 8. Temporary Access Pass Lifecycle

The Temporary Access Pass was configured as a short-lived bootstrap credential rather than a permanent authentication method.

After its configured lifetime expired, Entra ID marked the TAP as no longer usable. This demonstrates the temporary credential lifecycle and reduces the risk associated with leaving bootstrap credentials active after onboarding.

### Evidence
<img width="1647" height="916" alt="M5-TAP-Expired-Lifecycle" src="https://github.com/user-attachments/assets/4d16d062-3fe0-4b89-acc4-a034a50c0a50" />
---

## 9. Passkey Credential Lifecycle and Audit Investigation

The passkey credential lifecycle was also investigated using Microsoft Entra audit logs.

A **Delete platform credential** event was identified and the Modified Properties were reviewed. The audit data showed the previous FIDO credential value and the resulting empty value after deletion.

This demonstrates how authentication credential changes can be traced through Entra audit telemetry during identity administration or security investigations.

### Evidence
<img width="852" height="767" alt="M5-Passkey-Deletion-Audit-Modified-Properties" src="https://github.com/user-attachments/assets/fdac2bfe-182d-4962-8c23-f6ea8514f1c8" />
---

## 10. Engineering Outcomes

This module demonstrated an end-to-end passwordless authentication implementation in Microsoft Entra ID.

The implementation included:

- Creating a controlled passwordless pilot group
- Enabling Passkey (FIDO2) authentication for selected users
- Using Temporary Access Pass for secure authentication bootstrap
- Registering and validating a synced passkey
- Performing passwordless authentication
- Verifying Passkey (synced) authentication through Entra sign-in logs
- Configuring a custom passkey authentication strength
- Applying the authentication strength through Conditional Access
- Using Report-only mode to validate Conditional Access before enforcement
- Validating the expiration and removal of temporary authentication credentials
- Investigating passkey credential deletion through Microsoft Entra audit logs

## Key Security Considerations

Passwordless authentication reduces reliance on reusable passwords and can provide stronger resistance to credential phishing.

Temporary Access Pass provides a controlled mechanism for bootstrapping strong authentication methods, while Authentication Strengths and Conditional Access allow organisations to specify which authentication methods are acceptable for sensitive access scenarios.

The lab also demonstrated the importance of sign-in and audit telemetry for validating authentication behaviour and investigating credential lifecycle changes.

---

## Module Status

**Completed**
