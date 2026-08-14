# Module 07 – Identity Protection and Risk Management

## Overview

This module assesses Microsoft Entra ID Protection as a control for identifying and responding to identity-based risk.

The lab focused on reviewing the tenant's Identity Protection posture and determining whether risk-based Conditional Access could be implemented to automatically respond to risky authentication activity.

During the assessment, a licensing dependency was identified that prevented the full risk-based Conditional Access workflow from being implemented in the lab tenant.

## 1. Identity Protection Assessment

Microsoft Entra ID Protection was reviewed to establish the current identity risk posture of the tenant and understand the available monitoring and remediation capabilities.

The dashboard was used to assess protected users, detected attacks, risky identities and remediation activity. No active identity risk requiring remediation was present during the assessment.

### Evidence

<img width="1889" height="952" alt="M7-01-ID-Protection-Dashboard" src="https://github.com/user-attachments/assets/e7e5f794-ccd8-4db6-9799-2dcd4ef5b98c" />


The dashboard provides the baseline identity risk assessment for the lab environment and confirms that no active risk events were available for investigation or remediation during testing.

## 2. Risk-Based Conditional Access Assessment

Following the Identity Protection review, the next objective was to design a Conditional Access control that could respond automatically when Microsoft Entra identifies a risky sign-in.

The intended control was to use **sign-in risk** as the Conditional Access signal and require MFA when elevated authentication risk is detected.

During configuration, the lab tenant's licensing level prevented the sign-in risk condition from being used. The environment provides Microsoft Entra ID P1 capabilities, while risk-based Conditional Access using Identity Protection risk signals requires Microsoft Entra ID P2.

This prevented the policy from being implemented and tested end-to-end in the current lab environment.

### Evidence

<img width="1892" height="967" alt="M7-05-Sign-In-Risk-Condition-Unavailable-P1" src="https://github.com/user-attachments/assets/20b4833a-13eb-4325-8bbc-018589d529a3" />


The Conditional Access configuration demonstrates that the required sign-in risk capability was unavailable under the lab tenant's current licensing. This dependency was identified before attempting to deploy an incomplete risk-based security control.

## 3. Production Risk Remediation Design

Although the lab licensing prevented implementation of the complete risk-based workflow, the assessment established how the control would be deployed in a Microsoft Entra ID P2 environment.

For a production implementation, Identity Protection risk signals would feed into Conditional Access so that authentication controls could respond dynamically to the assessed risk of a sign-in.

A production design would include:

- Monitoring Identity Protection risk detections and risky sign-ins.
- Using sign-in risk as a Conditional Access condition.
- Requiring MFA for sign-ins assessed as elevated risk.
- Investigating risky users and associated authentication activity before administrative remediation.
- Using remediation actions such as password reset, confirming the user as compromised or confirming the user as safe where appropriate.
- Initially deploying new risk-based Conditional Access policies in Report-only mode to validate their impact before enforcement.

This approach moves identity protection beyond static access rules by allowing authentication requirements to respond to Microsoft's calculated identity risk.

## Engineering Outcome

The assessment demonstrated both the operational use of Microsoft Entra ID Protection and an important deployment dependency.

The tenant's existing licensing supports Conditional Access but does not provide the P2 Identity Protection capabilities required for the intended risk-based Conditional Access workflow. This limitation was identified during implementation rather than representing the control as successfully deployed.

In a P2-enabled environment, the proposed design could be implemented and validated through risky sign-in investigation, Conditional Access evaluation and subsequent identity remediation.
## Skills Demonstrated

- Microsoft Entra ID Protection assessment
- Identity risk monitoring
- Risk-based Conditional Access design
- Sign-in risk analysis
- MFA-based risk response design
- Conditional Access Report-only deployment strategy
- Identity risk remediation planning
- Microsoft Entra licensing dependency assessment

---

## Lab Result

**Status:** Partially implemented due to licensing constraint

The Identity Protection environment was successfully assessed and a risk-based Conditional Access response was designed. Full implementation and validation could not be completed because the lab tenant does not provide the Microsoft Entra ID P2 capabilities required for sign-in risk-based Conditional Access.

The licensing limitation and the required production implementation approach were documented as part of the engineering assessment.
