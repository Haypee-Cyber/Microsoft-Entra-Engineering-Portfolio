# Module 09 – Privileged Role & RBAC Management

## 1. Global Administrator Role Review

I reviewed the Global Administrator role to identify accounts holding the highest level of administrative access within the Microsoft Entra tenant.

The review confirmed the existing Global Administrator assignments and provided visibility of accounts with tenant-wide administrative privileges.

This demonstrates the importance of identifying and controlling standing privileged access within an enterprise identity environment.

### Evidence

<img width="1899" height="951" alt="M9-01-Global-Administrator-Assignments" src="https://github.com/user-attachments/assets/95f46f0e-f546-4d56-9e79-6d0405321920" />

## 2. Privileged Role Administrator Assessment

I reviewed the Privileged Role Administrator role to assess existing privileged access within the tenant.

This role provides authority to manage Microsoft Entra role assignments and is therefore considered a highly privileged administrative role.

The initial review confirmed that no users were assigned to the Privileged Role Administrator role before the lab assignment was performed.

### Evidence

<img width="1908" height="912" alt="M9-01-Privileged-Role-Administrator-Test-User" src="https://github.com/user-attachments/assets/f09db062-442c-4d05-8975-ea1d714e013c" />

## 3. Privileged Role Administrator Assignment

Following the privileged role assessment, I assigned the **Privileged Role Administrator** role to the dedicated **test user** account.

The assignment was performed at directory scope and then verified from the role assignment interface.

This provided a controlled method of validating how privileged Microsoft Entra roles are granted and prepared the account for subsequent testing of its role-management capabilities.

### Evidence

<img width="1914" height="988" alt="M9-02-Privileged-Role-Assignment-Capability" src="https://github.com/user-attachments/assets/194cca5b-98db-42ec-8893-1367018a5b3d" />

## 4. Privileged Role Capability Validation

After assigning the Privileged Role Administrator role, I signed in using the dedicated test account and validated the resulting administrative capability.

The test account was able to initiate the process for assigning the **Security Reader** Microsoft Entra role to another identity.

The assignment was deliberately not completed because the objective was to validate the administrative permission rather than introduce an unnecessary additional role assignment.

This confirmed that the Privileged Role Administrator assignment was effective and demonstrated practical validation of Microsoft Entra RBAC rather than relying solely on the configured role assignment.

### Evidence

<img width="1914" height="988" alt="M9-02-Privileged-Role-Assignment-Capability" src="https://github.com/user-attachments/assets/d738ffa6-5da5-4625-bba4-fb6ef35f97a1" />

## 5. Engineering Outcome

This module demonstrated the practical implementation and validation of privileged Microsoft Entra RBAC.

The exercise included reviewing existing highly privileged access, identifying an unassigned privileged role, granting that role to a controlled test identity, and validating that the resulting permissions operated as expected.

The lab also reinforced the principle of least privilege. Privileged role assignments should be limited to identities that require them, regularly reviewed, strongly authenticated, and monitored for inappropriate use.

In a production environment with Microsoft Entra P2 or Entra ID Governance licensing, Privileged Identity Management should be considered to replace unnecessary standing privilege with eligible, time-bound and auditable role activation.

**Status: Successfully implemented and validated**







