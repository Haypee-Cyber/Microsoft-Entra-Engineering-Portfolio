# Module 11 – Access Reviews and Identity Governance

## 1. Access Reviews Capability Assessment

The objective of this exercise was to evaluate Microsoft Entra Access Reviews as a governance control for periodically reviewing and removing unnecessary access.

I attempted to access the **Access Reviews** capability through Microsoft Entra Identity Governance. The portal returned an access restriction, preventing the creation of an access review in the current lab environment.

Rather than treating the failure as a configuration issue, the tenant licensing was investigated to determine whether the required Identity Governance capability was available.

### Evidence
<img width="1906" height="981" alt="M11-01-Access-Reviews-Permission-Restriction" src="https://github.com/user-attachments/assets/c7c6f239-2360-4c9a-92cd-2f6b23e20c2d" />

## 2. Identity Governance Licensing Investigation

Following the Access Reviews restriction, I reviewed the Microsoft Entra tenant's assigned products to determine whether the required governance licensing was available.

The tenant was licensed with **Microsoft 365 Business Premium** and **Microsoft 365 E5 Insider Risk Management**, but did not have **Microsoft Entra ID P2** or **Microsoft Entra ID Governance** licensing required for the planned Access Reviews implementation.

This established that the limitation was caused by the capabilities available within the lab environment rather than an Access Reviews configuration failure.

Identifying licensing dependencies before designing or deploying identity governance controls is important in enterprise environments because licensing directly affects which security and governance capabilities can be implemented.

## 3. Production Access Reviews Design

Although Access Reviews could not be configured in the lab tenant, I defined how the capability would be implemented in a production Microsoft Entra environment with the required Identity Governance licensing.

Access Reviews would be used to periodically verify whether users still require access to security groups, Microsoft 365 groups, applications and privileged resources.

A production implementation would include:

- Defining the users, groups or applications requiring periodic review
- Selecting appropriate reviewers such as resource owners or managers
- Configuring recurring review schedules
- Requiring reviewers to approve or deny continued access
- Providing justification and relevant decision context
- Automatically removing access where a review results in denial
- Defining appropriate handling for users who are not reviewed
- Monitoring review completion and maintaining an auditable governance record

This would reduce access accumulation and help ensure that permissions remain aligned with current business requirements.

## 4. Engineering Outcome

This module demonstrated the assessment and design process required before deploying Microsoft Entra identity governance controls.

The Access Reviews capability was assessed, the implementation restriction was investigated, and the tenant licensing was identified as the limiting factor.

Rather than representing an unavailable capability as successfully implemented, the constraint was documented and the required production design was established.

This exercise reinforced an important identity engineering principle: effective governance requires not only technical configuration but also an understanding of licensing, review ownership, access lifecycle requirements and remediation decisions.

**Status: Design completed – implementation constrained by tenant licensing**


