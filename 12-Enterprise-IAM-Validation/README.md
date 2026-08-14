# Module 12 – Enterprise IAM Validation and Project Close-Out

## 1. Conditional Access Security Baseline Validation

The final stage of the project began with a review of the Microsoft Entra Conditional Access environment to validate the identity security controls implemented throughout the lab.

The policy configuration was reviewed as a consolidated security baseline rather than assessing each policy in isolation.

The environment contained Conditional Access controls covering authentication requirements, phishing-resistant authentication, application access and network-aware access scenarios developed during the project.

This final review demonstrated how multiple identity controls can be combined to create a layered access security architecture rather than relying on a single authentication policy.

### Evidence

<img width="1904" height="950" alt="M12-01-Enterprise-Conditional-Access-Policies" src="https://github.com/user-attachments/assets/fccecb16-a2b6-4707-a3ed-84eff67a506a" />

## 2. Scoped Administrative Access Validation

The enterprise identity configuration was reviewed to confirm that administrative privileges were not unnecessarily granted at tenant-wide scope.

The **London Office** Administrative Unit demonstrated a delegated administration model where the **User Administrator** role was assigned specifically to the Administrative Unit.

The assignment displayed **This resource** as its scope, confirming that administrative authority was restricted to the intended organisational boundary.

This provides a practical least-privilege model for organisations that need to delegate identity administration to regional IT teams, departments or support functions without granting equivalent permissions across the entire tenant.

### Evidence

<img width="1909" height="955" alt="M12-02-Administrative-Unit-Scoped-RBAC" src="https://github.com/user-attachments/assets/3a18a591-529f-4e85-b93f-f9a6ed9f1c52" />

## 3. Authentication Methods Security Baseline

The tenant's Microsoft Entra authentication method policies were reviewed as part of the final identity security validation.

The assessment confirmed the authentication methods available within the environment, including the **Passkey (FIDO2)** capability configured and tested earlier in the project.

Reviewing authentication methods alongside Conditional Access is important because Conditional Access can define authentication requirements, while Authentication Methods policies determine which methods users are permitted to register and use.

This relationship was demonstrated during the project when Passkey availability was successfully traced to Authentication Methods policy scope and group membership.

### Evidence

<img width="1906" height="963" alt="M12-03-Authentication-Methods-Policies" src="https://github.com/user-attachments/assets/b989e26b-7723-4487-bbc3-acf94592106f" />

## 4. Live Sign-In and Conditional Access Validation

The final technical validation used Microsoft Entra sign-in logs to verify how the configured Conditional Access controls were evaluated during an actual authentication event.

A successful sign-in from the dedicated **test user** was reviewed and the Conditional Access results were examined to identify the policies evaluated during authentication.

This provided runtime validation of the identity security configuration rather than relying solely on policy settings.

The exercise demonstrated the importance of using sign-in telemetry when troubleshooting access decisions and validating that identity controls are operating as intended.

### Evidence

<img width="1904" height="960" alt="M12-04-Conditional-Access-Sign-In-Validation" src="https://github.com/user-attachments/assets/9e014a59-ad54-43b4-a5bb-965be0e2428d" />

## 5. Project Engineering Outcome

This final validation brought together the identity security controls implemented throughout the Microsoft Entra engineering project.

The environment demonstrated a layered identity security architecture combining authentication, access control, privileged administration, delegated administration and operational monitoring.

The completed project included practical implementation and validation of:

- Microsoft Entra user, group and administrative identity management
- Enterprise application integration and Single Sign-On
- Application access and authentication flows
- Conditional Access policy design and deployment
- Trusted network and location-aware access controls
- Phishing-resistant authentication using Passkey (FIDO2)
- Authentication Methods policy targeting
- Emergency access and administrative lockout protection
- Conditional Access What If analysis
- Sign-in log investigation and policy decision analysis
- Microsoft Entra RBAC and privileged role management
- Administrative Unit scoped delegation
- Positive and negative least-privilege validation
- Identity Protection capability assessment
- Identity Governance and PIM capability assessment

The project also identified capabilities that could not be fully implemented because of tenant licensing. These limitations were investigated and documented rather than represented as completed technical implementations.

The resulting environment demonstrates an identity engineering approach based on **Zero Trust, least privilege, strong authentication, controlled administrative access, operational resilience and evidence-based validation**.

Rather than treating configuration as proof of success, controls were tested through user authentication, sign-in telemetry, policy simulation, permission testing and both positive and negative access scenarios.

## Project Status

**Microsoft Entra Engineering Portfolio – Completed**

The lab provides practical evidence of designing, implementing, troubleshooting and validating Microsoft Entra identity and access controls in an enterprise-style environment.

