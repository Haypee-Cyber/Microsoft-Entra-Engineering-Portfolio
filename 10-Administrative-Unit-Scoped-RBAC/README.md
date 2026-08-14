# Module 10 – Administrative Unit Scoped RBAC

## 1. Scoped User Administrator Assignment

The objective of this exercise was to implement delegated administration using a Microsoft Entra Administrative Unit rather than granting tenant-wide administrative permissions.

The existing **London Office** Administrative Unit was used as the administrative boundary.

I assigned the **User Administrator** role to the dedicated **test user** from within the London Office Administrative Unit. This restricted the administrative role to resources within the London Office scope rather than granting User Administrator privileges across the entire directory.

The resulting role assignment displayed **This resource** as the scope, confirming that the administrative permission was scoped to the London Office Administrative Unit.

### Evidence

<img width="1903" height="959" alt="M10-01-London-Office-Scoped-User-Administrator" src="https://github.com/user-attachments/assets/8c9190da-5fdc-4c30-bd3f-0c33cc4d3245" />

## 2. Positive Scoped Administration Validation

After assigning the scoped User Administrator role, I signed in using the **test user** account to validate the delegated administrative permissions.

The **entraproject3** account, which is a member of the **London Office** Administrative Unit, was selected for testing.

The **Edit properties** control was available to the test administrator, confirming that the scoped User Administrator role provided the expected administrative capability for identities within the assigned Administrative Unit.

This validated that delegated administration was functioning correctly within the defined London Office boundary.

### Evidence

<img width="1909" height="955" alt="M10-02-Inside-AU-Administration-Allowed" src="https://github.com/user-attachments/assets/6ad61b18-cfb0-48f2-a91f-6bec40392af7" />

## 3. Negative Scoped Administration Validation

To verify that the delegated role did not provide unintended tenant-wide administrative access, I performed the same administration test against **Entra Project 1**, an identity outside the **London Office** Administrative Unit.

While signed in as the same test administrator, the **Edit properties** control was unavailable for this account.

This confirmed that the User Administrator permission was constrained by the Administrative Unit boundary and did not grant equivalent administrative capability over users elsewhere in the directory.

The positive and negative tests together validated that the delegated administration model enforced the intended scope.

### Evidence

<img width="1901" height="962" alt="M10-03-Outside-AU-Administration-Denied" src="https://github.com/user-attachments/assets/90f273f1-36f2-42d8-9eb5-033934d52e1c" />

## 4. Engineering Outcome

This module demonstrated the implementation and validation of scoped administrative access using Microsoft Entra Administrative Units.

Rather than granting the User Administrator role across the entire tenant, administrative privilege was delegated specifically to the **London Office** Administrative Unit.

The implementation was validated from both directions:

- A user inside the London Office scope could be administered successfully.
- A user outside the London Office scope could not be administered by the same delegated administrator.

This demonstrated practical application of **least privilege, delegated administration and scoped RBAC**, while reducing the security risk associated with unnecessary tenant-wide administrative permissions.

In a production environment, this model can be used to delegate identity administration to regional IT teams, business units or support teams while restricting their authority to the users they are responsible for.

**Status: Successfully implemented and validated**






