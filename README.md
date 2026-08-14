# Microsoft Entra Engineering Portfolio

A hands-on Microsoft Entra engineering portfolio demonstrating identity architecture, application integration, authentication security, Conditional Access, privileged access, delegated administration, identity protection, governance assessment, troubleshooting and operational validation.

This portfolio was built as an enterprise-style lab rather than a collection of isolated configuration exercises. Each module follows a practical engineering workflow: design, implementation, validation, troubleshooting and evidence.

## Portfolio Objectives

The project demonstrates practical capability across:

- Microsoft Entra user and group administration
- Enterprise applications and Single Sign-On
- Application identity and OIDC integration
- Conditional Access design and validation
- Trusted network and location-aware access
- Passkey and phishing-resistant authentication
- Authentication Methods policy management
- Emergency access and administrative lockout protection
- Identity Protection assessment
- Microsoft Entra RBAC
- Privileged role administration
- Administrative Unit scoped delegation
- Access Reviews and governance capability assessment
- Sign-in investigation and policy decision analysis
- Zero Trust and least-privilege identity design

## Engineering Approach

The portfolio was developed around real operational questions rather than simple portal navigation.

Controls were validated using:

- Live authentication events
- Microsoft Entra sign-in logs
- Conditional Access policy evaluation
- What If simulation
- Positive and negative access testing
- Authentication method registration behaviour
- Role-assignment capability testing
- Administrative Unit scope validation
- Licensing and capability assessment

Where tenant licensing prevented full implementation of a feature, the limitation was investigated and documented rather than represented as a successful deployment.

## Modules

### [02 – Application Identity](02-Application-Identity)

Application identity fundamentals, application registrations and Microsoft Entra identity objects.

### [03 – Enterprise Applications](03-Enterprise-Applications)

Enterprise application management, service principals and SAML Single Sign-On configuration.

### [04 – OIDC and Conditional Access](04-OIDC-Conditional-Access)

OpenID Connect authentication, application access and Conditional Access integration.

### [05 – Passwordless Authentication](05-Passwordless-Authentication)

Passkey and phishing-resistant authentication design, registration and validation.

### [06 – Conditional Access Security Engineering](06-Conditional-Access-Security)

Location-aware Conditional Access, trusted network design, Report-only validation, emergency access resilience, What If testing and sign-in investigation.

### [07 – Identity Protection and Risk Management](07-Identity-Protection-Risk-Management)

Microsoft Entra Identity Protection assessment, risky sign-in analysis and risk-based Conditional Access capability review.

### [09 – Privileged Role and RBAC Management](09-Privileged-Role-RBAC)

Privileged directory-role assessment, Privileged Role Administrator assignment and validation of resulting role-management capability.

### [10 – Administrative Unit Scoped RBAC](10-Administrative-Unit-Scoped-RBAC)

Delegated administration using Administrative Units, including positive and negative validation of scoped User Administrator permissions.

### [11 – Access Reviews and Identity Governance](11-Access-Reviews-Governance)

Identity Governance and Access Reviews capability assessment, licensing investigation and production governance design.

### [12 – Enterprise IAM Validation](12-Enterprise-IAM-Validation)

Final validation of Conditional Access, authentication methods, scoped RBAC and live sign-in policy evaluation across the completed environment.

## Key Engineering Scenarios

### Emergency Access Resilience

A dedicated emergency access identity was created and validated to reduce the risk of administrative lockout caused by Conditional Access or authentication failures.

### Phishing-Resistant Authentication

Passkey (FIDO2) authentication was deployed through controlled policy scope and validated against real sign-in activity.

### Conditional Access Investigation

Conditional Access decisions were examined through sign-in telemetry to determine why policies were applied, not applied or satisfied.

### Scoped Delegated Administration

The User Administrator role was restricted to the London Office Administrative Unit.

Testing confirmed that the delegated administrator could manage a user inside the Administrative Unit while the same action was unavailable for a user outside the scope.

### Privileged Access Validation

Privileged Entra roles were reviewed and a controlled test account was assigned Privileged Role Administrator.

The resulting permissions were validated by confirming that the identity could initiate Microsoft Entra role assignment operations.

## Security Principles Demonstrated

The engineering decisions throughout this project were guided by:

- Zero Trust
- Least privilege
- Strong authentication
- Privileged-access control
- Administrative separation
- Controlled policy deployment
- Emergency access resilience
- Evidence-based validation
- Identity governance
- Security monitoring and investigation

## Technology Areas

Microsoft Entra ID  
Conditional Access  
Microsoft Entra RBAC  
Administrative Units  
Enterprise Applications  
Application Registrations  
SAML  
OpenID Connect  
Passkey / FIDO2  
Identity Protection  
Identity Governance  
Privileged Identity Management assessment  
Access Reviews assessment  
Microsoft Entra sign-in logs

## Project Status

**Completed**

The portfolio demonstrates practical Microsoft Entra identity engineering across architecture, implementation, troubleshooting, access control, authentication security and operational validation.
