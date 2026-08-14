# Module 06 – Conditional Access Security Engineering

## Overview

This module demonstrates the design, implementation, testing, and investigation of a Microsoft Entra Conditional Access control based on network trust.

The scenario models an organisation where access originating from the trusted corporate network is treated differently from access originating from external networks.

A named trusted network was configured and a Conditional Access policy was designed to require phishing-resistant authentication when the test user accessed organisational resources from outside that trusted network.

The policy was deployed in Report-only mode first, allowing its impact to be evaluated safely before enforcement.

## Security Scenario

A user authenticates to Microsoft Entra ID from a network outside the organisation's trusted corporate network.

The objective is to:

- Identify the source network and location
- Determine whether the sign-in falls outside the trusted network
- Evaluate the applicable Conditional Access policy
- Require phishing-resistant authentication for the external sign-in
- Validate the control using Report-only mode
- Investigate the resulting Entra sign-in telemetry

---

## 1. Trusted Corporate Network

A named location was created to represent the organisation's trusted corporate network.

This provides a network trust boundary that can be referenced by Conditional Access policies.

### Evidence
<img width="1910" height="946" alt="M6-S1-01-Trusted-Corporate-Named-Location" src="https://github.com/user-attachments/assets/ee7f7fd4-b02a-42be-9e60-eba00912e9cb" />

---

## 2. Conditional Access Policy for External Network Access

A Conditional Access policy was configured to protect access originating outside the trusted corporate network.

The policy targets the test user and organisational resources while excluding the configured trusted corporate network.

Phishing-resistant MFA was selected as the grant control. The policy was initially deployed in Report-only mode to validate its behaviour before enforcement.

### Evidence
<img width="1905" height="957" alt="M6-02-Conditional-Access-Outside-Trusted-Network-Report-Only" src="https://github.com/user-attachments/assets/105d5118-af4b-4268-bd6d-3ba4e0e0d410" />
The configuration demonstrates a location-aware Zero Trust access control where network location contributes to the access decision, while strong authentication provides protection when the user connects externally.

---

## 3. Report-Only Policy Validation

The Conditional Access policy was evaluated in Report-only mode before enforcement.

A test sign-in was generated from outside the configured trusted corporate network. Microsoft Entra evaluated the sign-in against the policy without actively blocking or interrupting the user session.

The test confirmed that the user, target resource and external network conditions matched the policy and that the configured grant control was satisfied.

### Evidence
<img width="1899" height="876" alt="M6-03-Conditional-Access-Policy-Created-Report-Only" src="https://github.com/user-attachments/assets/6fcfd109-5c66-4e80-b70a-ee2b18801161" />

The policy was successfully created in Report-only mode, providing a safe method of assessing the expected impact before production enforcement.

<img width="1906" height="958" alt="M6-03-Outside-Trusted-Network-Report-Only-Success" src="https://github.com/user-attachments/assets/9d150880-c597-4364-9b9b-45dc59cea9b5" />

The sign-in evaluation returned Report-only: Success. The test user, Azure Resource Manager resource and external network location matched the policy conditions, confirming that the Conditional Access design operated as intended.

---

## 4. Security Investigation of External Sign-In

Following successful policy validation, the external sign-in was investigated using Microsoft Entra sign-in telemetry.

The investigation reviewed the authentication result, user identity, source network, geographic location and Conditional Access evaluation to determine whether the activity was appropriately protected.

### Evidence
<img width="1908" height="947" alt="M6-04-Untrusted-Network-Policy-Report-Only-Evaluation" src="https://github.com/user-attachments/assets/8c0afb3a-a287-4056-8d88-03d85359abfe" />

The Conditional Access evaluation was reviewed to determine how the external sign-in was processed and whether the configured security controls applied to the session.

<img width="858" height="917" alt="M6-04-Untrusted-SignIn-Investigation-Basic-Info" src="https://github.com/user-attachments/assets/268d6680-18e3-4662-b8a7-b3f421756190" />

The sign-in event was successful and required multifactor authentication. The event also provided request and correlation identifiers that could be used for further investigation and log correlation.

---

## 5. Source Network and Location Investigation

The source of the authentication was examined to establish whether the connection originated from the organisation's trusted network.

### Evidence

<img width="840" height="368" alt="M6-05-Untrusted-SignIn-Source-IP-Location" src="https://github.com/user-attachments/assets/c3766131-a291-4123-bc41-25a472533d64" />

The sign-in originated from IP address 86.20.231.147 in Reading, GB. The address was not associated with the configured trusted corporate named location, supporting the Conditional Access policy evaluation of the session as external network access.

---

## 6. Phishing-Resistant Authentication Validation

The authentication details for the external sign-in were reviewed to confirm that the authentication requirements associated with the Conditional Access evaluation were satisfied.

The sign-in telemetry showed that Conditional Access was applied and that the phishing-resistant authentication requirement was successfully satisfied.

### Evidence

<img width="856" height="391" alt="M6-06-Phishing-Resistant-MFA-Authentication-Details" src="https://github.com/user-attachments/assets/01af2892-f7d1-4c4e-985b-e898f70bb69e" />

The authentication stages succeeded and the sign-in record identified phishing-resistant authentication as the required authentication strength.
The existing authentication state satisfied the requirement, demonstrating how Microsoft Entra can evaluate previously established strong authentication when making a Conditional Access decision.

---

## 7. Troubleshooting Conditional Access Evaluation

During initial testing, the Conditional Access policy returned a Report-only result of "Not applied."

The sign-in telemetry was investigated rather than assuming that the policy configuration was functioning correctly.

### Evidence

<img width="1919" height="949" alt="M6-05-Conditional-Access-Policy-Not-Applied-Resource-Mismatch" src="https://github.com/user-attachments/assets/4acf82d0-fb8a-4e61-a2b6-30ec99f6bd49" />

Investigation of the policy evaluation identified that the target resource did not match the policy assignment.

The policy configuration was reviewed and the target resource scope was corrected. A new authentication test was then performed.

The subsequent sign-in successfully matched the user, resource and external network conditions, confirming that the issue had been resolved.

---

## 8. Security Engineering Conclusion

This scenario demonstrated the implementation and investigation of location-aware Conditional Access in Microsoft Entra ID.

A trusted corporate network boundary was defined and external access was evaluated against a Conditional Access policy requiring phishing-resistant authentication.

The policy was initially deployed in Report-only mode to assess its impact safely. Sign-in telemetry was then used to validate policy matching, investigate the source IP and location, verify authentication requirements, and troubleshoot an initial resource-scoping issue.

The final test confirmed that the user, target resource and external network conditions matched successfully and that the required authentication control was satisfied.

### Security Outcome

The design provides a Zero Trust approach in which access is evaluated dynamically based on identity, resource, network context and authentication strength rather than assuming that a successful username and password authentication is sufficient.






















