# Microsoft Entra Engineering Portfolio Overview

## Project Purpose

This portfolio demonstrates the design, implementation, testing and troubleshooting of Microsoft Entra identity and access controls within an enterprise-style lab environment.

The project focuses on practical identity engineering rather than isolated configuration exercises. Security controls were implemented and then validated through authentication testing, sign-in telemetry, permission testing and positive and negative access scenarios.

## Core Engineering Areas

The portfolio covers:

- Application identities and enterprise applications
- SAML and OpenID Connect authentication
- Conditional Access architecture
- Passwordless and phishing-resistant authentication
- Authentication Methods policies
- Emergency access design
- Identity Protection and risk assessment
- Microsoft Entra RBAC
- Privileged role administration
- Administrative Unit scoped delegation
- Identity Governance capability assessment
- Access Reviews design
- Sign-in monitoring and troubleshooting
- Zero Trust and least-privilege implementation

## Validation Approach

Configuration alone was not treated as proof that a control worked.

Where possible, implementations were validated using:

- Live user authentication
- Microsoft Entra sign-in logs
- Conditional Access evaluation
- What If analysis
- Positive access testing
- Negative access testing
- Role and permission validation
- Administrative scope testing

Where Microsoft Entra licensing prevented implementation of a capability, the restriction was investigated and documented together with the intended production design.

## Module Numbering

The portfolio retains its original engineering workstream numbering.

Module 08 was reserved for a Privileged Identity Management implementation. The available lab licensing did not support the planned PIM workflow, so a separate implementation module was not created.

Privileged access capability assessment was incorporated into the subsequent RBAC and governance work rather than presenting an unimplemented feature as completed engineering work.

## Engineering Principles

The project applies:

- Zero Trust
- Least privilege
- Strong authentication
- Separation of administrative privileges
- Scoped delegation
- Emergency access resilience
- Evidence-based validation
- Identity governance
- Operational troubleshooting

## Project Status

**Completed**

The repository contains implementation documentation and supporting evidence for each completed engineering workstream.
