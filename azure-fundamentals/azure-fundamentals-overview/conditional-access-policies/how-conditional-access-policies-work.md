# How Conditional Access Policies Work

## **Overview:**

The following goes over how conditional access are evaluated and how they work. This section provides an example of a conditional access policy.

### **How Conditional Access Works**

When a user attempts to access an Azure AD-protected resource, Azure AD evaluates the sign-in attempt against the active Conditional Access policies. Based on the defined conditions, the policies will either allow access, block access, or require additional actions, such as MFA or device compliance.

The process generally works as follows:

1. **User attempts to sign in**: A user tries to sign in to a cloud app (e.g., Microsoft 365) or service protected by Azure AD.
2. **Conditional Access evaluates the request**: Azure AD evaluates the user's access request based on the policies configured. It checks the conditions, such as:
   * The user's identity and role.
   * The location of the sign-in.
   * The device's compliance with security policies.
   * The risk level associated with the sign-in attempt.
3. **Conditional Access enforces controls**: Based on the evaluation of conditions, Azure AD applies one or more controls. These may include:
   * Requiring MFA.
   * Blocking access.
   * Enforcing device compliance.
4. **User access is granted or denied**: Depending on whether the required conditions are met, the user is either granted access to the app or service, or access is denied.

### **Example Scenario:**

A Conditional Access policy can be configured to:

* Block access for any user who is attempting to sign in from outside the corporate network.
* Require MFA if the user is signing in from a risky location or an untrusted device.
* Deny access if the sign-in attempt is flagged as high risk by Azure AD Identity Protection.
