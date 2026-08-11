# Module 04 - OIDC and Conditional Access Evidence

This folder contains implementation and validation evidence from the Microsoft Entra ID OIDC and Conditional Access lab.

The lab demonstrates OIDC application configuration, Microsoft Graph delegated permissions, application roles, token claims, role-based authorization, Conditional Access MFA enforcement, and authentication validation.

## Evidence Register

| Evidence | What it demonstrates |
|---|---|
| M3-01-OIDC-App-Registration-Overview.png | Microsoft Entra OIDC application registration and core application configuration |
| M3-02-OIDC-Web-Redirect-URI-Configured.png | Web platform and redirect URI configuration used by the OIDC authentication flow |
| M3-03-OIDC-ID-token-optional-claims.png | Configuration of optional claims within ID tokens |
| M3-04-Microsoft-Graph-delegated-API-permissions.png | Microsoft Graph delegated API permissions configured for the application |
| M3-05-application-owner-assigned.png | Application ownership assignment for administrative accountability |
| M3-06-standard-user-app-role-created.png | Creation of an application role for standard-user authorization |
| M3-S6-Role-Removal-Token-Validation.png | Token validation following removal of an application role assignment |
| M3-S7-Conditional-Access-MFA-Enforcement-Success.png | Successful enforcement of the Conditional Access MFA requirement |
| M3-S7-Conditional-Access-Report-Only-Success.png | Conditional Access policy validation in Report-only mode before enforcement |
| M3-S7-OIDC-MFA-Challenge.png | Interactive MFA challenge triggered during OIDC authentication |
| M3-S7-OIDC-MFA-Fresh-Authentication-Validation.png | Validation of a fresh MFA authentication event |
| M3-S7-OIDC-MFA-Previously-Satisfied.png | Authentication behaviour where an existing MFA claim satisfied the access requirement |
| M3-S7-OIDC-Post-MFA-Token-Validation.png | OIDC token validation after successful MFA authentication |
| Manifest.png | Application manifest configuration used for application roles and token behaviour |
| Microsoft Graph permission types Delegated vs Application.png | Validation and comparison of delegated and application Microsoft Graph permission models |
| OIDC_Admin_Role_ID_Token_Validation.png | ID token validation for a user assigned the administrator application role |
| OIDC_Admin_Role_JWT_Claims.png | Decoded JWT showing identity and administrator role claims |
| OIDC_Admin_Role_Token_Claim.png | Validation of the administrator application role claim within the issued token |
| OIDC_App_Role_Assignment_Comparison.png | Comparison of application role assignments used to validate role-based authorization behaviour |

## Engineering Outcomes

The implementation demonstrates the ability to:

- Configure an application to use OpenID Connect authentication with Microsoft Entra ID
- Configure redirect URIs, token claims and Microsoft Graph permissions
- Design and assign application roles
- Inspect and validate JWT and ID token claims
- Test changes to authorization by modifying role assignments
- Configure Conditional Access initially in Report-only mode
- Enforce MFA through Conditional Access
- Validate fresh and previously satisfied MFA authentication
- Verify authentication and authorization behaviour through token analysis

## Validation

Testing confirmed that identity, role and authentication state were represented within issued tokens and that changes to role assignments affected subsequent authorization claims.

Conditional Access was validated before enforcement and subsequently tested with MFA enabled. Post-authentication token inspection was used to confirm the resulting authentication state.
