# Conditional Access Policies

### **Defining Conditional Access**

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p><a href="https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview">https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview</a></p></figcaption></figure>

Conditional Access is a security capability in Azure Active Directory (Azure AD) that automates access control decisions based on specific conditions. It allows organizations to define policies that enforce security requirements, ensuring that access to applications, services, and data is only granted if certain conditions are met.

The purpose of Conditional Access is to provide additional protection beyond basic identity and access management (IAM) controls by considering user behaviors and environmental factors, such as:

* **Location**: Where the user is attempting to sign in from.
* **Device**: The state of the device being used for access (e.g., compliant or non-compliant).
* **Risk level**: The sign-in risk, which is determined by Azure AD Identity Protection.

Conditional Access policies combine these conditions with specific controls, allowing you to:

* Grant or deny access to apps and services.
* Enforce security measures, such as multifactor authentication (MFA), based on dynamic risk assessments.

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
