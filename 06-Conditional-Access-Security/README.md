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

---

## 9. Emergency Access and Conditional Access Resilience

The Conditional Access design was extended to address the risk of administrative lockout.

A dedicated emergency access account, **Emergency Access 01**, was configured to provide a recovery path if normal administrative access becomes unavailable because of authentication failure, Conditional Access misconfiguration, or another identity access issue.

The account was deliberately separated from normal user access so that emergency recovery would not depend entirely on the same controls it may be required to recover.

### Evidence
<img width="1912" height="954" alt="M6-ADV-01-Emergency-Access-Account" src="https://github.com/user-attachments/assets/4b7988c0-5453-4a14-bf05-94161e51feb5" />

---

## 10. Emergency Access Administrative Privilege

The emergency access account was assigned the **Global Administrator** role to ensure that it could be used to recover administrative access during a tenant-wide identity or Conditional Access failure.

This privilege gives the recovery identity sufficient authority to investigate and correct configurations that could otherwise prevent administrators from accessing the tenant.

Because of the sensitivity of the role, the account is intended strictly for emergency recovery rather than routine administrative activity.

### Evidence

<img width="1911" height="951" alt="M6-ADV-02-Emergency-Access-Global-Administrator-Role" src="https://github.com/user-attachments/assets/a08502d4-e955-4efd-b068-28ea695179d5" />

---

## 11. Emergency Access Conditional Access Exclusion

The Conditional Access configuration was updated to explicitly exclude **Emergency Access 01** from the policy protecting access outside the trusted corporate network.

This exclusion provides a controlled recovery path if the policy is misconfigured or if normal administrators are unable to satisfy its authentication requirements.

The exclusion was deliberately limited to the dedicated emergency identity rather than weakening the policy for standard users.

### Evidence
<img width="1905" height="941" alt="M6-ADV-03-Emergency-Access-Conditional-Access-Exclusion" src="https://github.com/user-attachments/assets/2caaf4df-5bfc-481d-adf1-8d962aefb60c" />

---

## 12. Emergency Access Conditional Access Validation

The emergency access configuration was validated using Microsoft Entra sign-in logs to confirm how Conditional Access evaluated the recovery identity during authentication.

The Conditional Access details showed that policies targeting other users did not apply to **Emergency Access 01**, while applicable tenant-wide controls were evaluated independently.

This validation confirmed that Conditional Access decisions could be traced to individual policy assignments and provided evidence that the emergency access design behaved as expected during an actual sign-in.

### Evidence

<img width="1915" height="955" alt="M6-ADV-08-Conditional-Access-Multiple-Policy-Evaluation" src="https://github.com/user-attachments/assets/afc00f93-54ec-411b-a4d3-ce2e7edab991" />

---

## 13. Detailed Conditional Access Policy Decision Analysis

Individual Conditional Access policy results were examined to determine why specific controls were applied or skipped during authentication.

The policy details exposed the evaluation of the user assignment and target resource, allowing the policy decision to be traced back to its configured scope.

This demonstrated an important troubleshooting capability: a policy appearing in the Conditional Access evaluation does not necessarily mean that it controlled the sign-in. The underlying assignment and condition results must be examined to determine why the policy was applied or excluded.

### Evidence
<img width="1909" height="946" alt="M6-ADV-09-Conditional-Access-Not-Applied-User-Scope-Mismatch" src="https://github.com/user-attachments/assets/d7ecc053-c415-4ee5-8c46-f1d9b1ca371a" />
---

## 14. Conditional Access What If Simulation

The Microsoft Entra **What If** tool was used to simulate Conditional Access evaluation before relying on live authentication testing.

The simulation reproduced a defined sign-in scenario using the selected identity, application, Windows device platform, browser client, source IP address and geographic location.

The results identified which Conditional Access policies would apply and, importantly, which policies would not apply together with the reason for exclusion.

This provided a controlled method of validating policy scope and troubleshooting unexpected Conditional Access behaviour without changing the production-style policy configuration.

### Evidence
<img width="1652" height="902" alt="M6-Emergency-Access-WhatIf-Validation" src="https://github.com/user-attachments/assets/b9d3ca7f-1a42-4f4a-aa13-8c7580c75971" />
---

## 15. Authentication Method Policy Scope Investigation

The emergency access account was reviewed to determine whether phishing-resistant Passkey (FIDO2) authentication was available for registration.

Although Passkey (FIDO2) was enabled in the tenant, the method was scoped only to the **GRP-Passwordless-Pilot** group. The emergency access account was not a member of this group and therefore was not initially eligible to register a passkey.

This demonstrated that enabling an authentication method at tenant level does not automatically make it available to every user. Authentication method policy targeting must also include the identity.

### Evidence
<img width="1910" height="912" alt="M6-ADV-04-Emergency-Account-Not-In-Passkey-Pilot-Group" src="https://github.com/user-attachments/assets/cb0ed99e-bfc6-4e3c-b7e2-f9ad85dfdf2a" />

---

## 16. Authentication Method Scope Validation

To validate the identified policy-scoping issue, **Emergency Access 01** was temporarily added to the **GRP-Passwordless-Pilot** group.

This placed the account within scope of the Passkey (FIDO2) authentication method policy and provided a controlled test of whether group membership was responsible for the method's availability.

### Evidence
<img width="1899" height="918" alt="M6-ADV-05-Emergency-Account-Added-To-Passkey-Pilot-Group" src="https://github.com/user-attachments/assets/6958e6db-1031-4817-821d-1acbe3a89c50" />

---

## 17. Passkey Eligibility Validation

After the emergency account was added to the passwordless pilot group, its Security Info registration options were reviewed again.

Passkey registration was now available to **Emergency Access 01**, confirming that the earlier registration limitation was caused by Authentication Methods policy targeting rather than a technical failure with the account.

This validated the relationship between authentication method policy scope, group membership and end-user registration capability.

### Evidence
<img width="1520" height="873" alt="M6-ADV-06-Emergency-Account-Passkey-Eligibility-Validated" src="https://github.com/user-attachments/assets/91943653-e063-4ca7-a2af-979239394ce6" />
---

## 18. Restore Emergency Access Separation

After validating the Passkey policy scope, **Emergency Access 01** was removed from the **GRP-Passwordless-Pilot** group.

This restored the intended separation between the passwordless pilot population and the emergency recovery identity.

The temporary scope change was therefore used only to validate the root cause and was removed once testing was complete, demonstrating controlled change and rollback rather than leaving unnecessary access in place.

### Evidence
<img width="1912" height="949" alt="M6-ADV-07-Emergency-Account-Removed-From-Passkey-Pilot-Group" src="https://github.com/user-attachments/assets/a160d6b8-db92-4158-a943-cd1922602a86" />

---

## 19. Engineering Outcome and Contractor Takeaways

The advanced Conditional Access exercise extended the original location-based security implementation into a more resilient enterprise access design.

The work demonstrated:

- Design and configuration of a dedicated emergency access identity
- Assignment of sufficient administrative privilege for tenant recovery
- Conditional Access exclusions to reduce the risk of administrative lockout
- Validation of policy behaviour using live sign-in telemetry
- Conditional Access troubleshooting using individual policy evaluation results
- Pre-deployment policy analysis using the What If simulator
- Investigation of Authentication Methods policy scope
- Troubleshooting Passkey eligibility through group-based policy targeting
- Controlled testing of configuration changes
- Rollback of temporary access changes after successful validation

A key engineering lesson from the exercise was that Conditional Access configuration should not be considered complete simply because a policy has been created.

Effective identity security requires policy scoping, safe deployment, emergency access planning, runtime validation, troubleshooting and a tested recovery path.

The exercise also demonstrated the distinction between **Conditional Access policy scope** and **Authentication Methods policy scope**. An identity can be excluded from a Conditional Access policy while still being independently included or excluded from authentication method availability.

Overall, the implementation demonstrates a Zero Trust approach in which access controls are validated against real authentication behaviour while maintaining operational resilience and administrative recovery capability.

---







