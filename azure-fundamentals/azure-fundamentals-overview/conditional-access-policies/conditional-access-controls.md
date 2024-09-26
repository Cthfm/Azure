# Conditional Access Controls

## **What Are Conditional Access Controls?**

Conditional Access **controls** specify the security actions that must be taken when the defined conditions in the policy are met. While conditions determine **when** the policy should be applied, controls define **what happens** once the policy is triggered.

There are two main types of controls:

* **Grant Controls**: Define the actions that must be satisfied to allow access.
* **Session Controls**: Define what happens during the session once access is granted, such as monitoring or limiting actions within the session.

## **Grant Controls**

**Grant Controls** are the actions required to allow access to the requested resource. These controls enable you to implement various security measures such as requiring MFA, device compliance, or blocking access altogether.

Here’s an overview of the most common Grant Controls:

### **Require Multi-Factor Authentication (MFA)**

MFA adds an additional layer of security by requiring users to verify their identity through more than one method (e.g., phone app, SMS, biometrics). Requiring MFA reduces the risk of compromised credentials being used to access resources.

**How It Works:**

* Users are prompted to provide a second form of verification when signing in.
* Common MFA methods include authentication apps, text messages, or hardware tokens.

**Use Case:**

For users signing in from untrusted locations or high-risk sessions, MFA can be enforced before granting access to sensitive applications like Microsoft 365 or financial systems.

### **Require Device to Be Marked as Compliant**

This control ensures that only devices that meet your organization’s security standards (such as being managed and compliant through Intune) are allowed to access specific resources.

**How It Works:**

* Devices must be enrolled in Intune (or another MDM) and meet compliance policies (e.g., have antivirus software, use encryption, or be up to date with security patches).

**Use Case:**

An organization can apply this control to ensure that corporate resources are only accessed from devices that are compliant with internal security policies, protecting against potential risks from untrusted or unmanaged devices.

### **Require Hybrid Azure AD Joined Device**

This control ensures that only devices joined to both Azure AD and an on-premises Active Directory can access certain resources.

**How It Works:**

* Hybrid Azure AD joined devices are those that are registered with both the organization’s on-prem Active Directory and Azure AD.

**Use Case:**

An organization might require that internal applications, such as finance or HR systems, are only accessible from devices that are hybrid joined, ensuring that only corporate-controlled devices are allowed access.

### **Require Approved Client App**

This control restricts access to cloud resources based on whether the user is accessing them through approved client applications, such as specific versions of Microsoft Outlook or Teams.

**How It Works:**

* Only apps that are listed as approved can be used to access certain resources.

**Use Case:**

An organization might enforce this control to ensure that only trusted apps, such as the Microsoft Authenticator app or managed versions of Outlook, can be used to access corporate data.

### **Require Password Change**

This control forces users to change their password if there is a suspicion of account compromise or a high-risk sign-in.

**How It Works:**

* If a user’s account is flagged for suspicious activity, this control requires the user to reset their password before they can regain access to resources.

**Use Case:**

For high-risk sign-ins, such as when a user’s credentials appear in a known data breach or if Azure Identity Protection detects an unusual sign-in, this control can mitigate risk by requiring a password reset.

### **Block Controls**

While Grant Controls allow access under certain conditions, **Block Controls** are designed to deny access entirely. Block Controls are useful when certain users or devices should never access particular resources or applications.

**How It Works:**

* When the conditions in the policy are met, the system blocks the user from accessing the specified application or resource.

**Use Case:**

An organization might block all users from signing in from specific regions known for malicious activity or block access from devices that do not meet minimum security requirements (e.g., outdated operating systems).

### **Session Controls**

**Session Controls** define actions that are applied during the session after access is granted. These controls can restrict the user’s behavior within the session, such as limiting downloads or requiring re-authentication based on certain triggers.

**Types of Session Controls:**

1.  **Application Enforced Restrictions**: This control allows the application itself to enforce limitations during the session. For example, you can configure Microsoft 365 apps to limit access to certain data, prevent downloads, or disable certain features (like sharing) when access is from untrusted devices or locations.

    **Use Case:**

    For a user accessing corporate documents on a personal device, the organization can limit the ability to download or print sensitive documents to reduce the risk of data leakage.
2.  **Sign-in Frequency**: This control defines how often a user must reauthenticate during an active session. You can set specific intervals that require users to sign in again to maintain access.

    **Use Case:**

    For highly sensitive applications, such as a financial system, an organization might require users to reauthenticate every 30 minutes to ensure the session remains secure.
3.  **Persistent Browser Session**: This control determines whether a user’s session stays active across multiple browser sessions. If disabled, users will have to sign in again every time they close their browser or after a certain time period.

    **Use Case:**

    For corporate networks, an organization might choose to keep browser sessions persistent for trusted locations to reduce user friction, while requiring frequent reauthentication for untrusted locations.

### **Combining Grant and Block Controls for Security**

Organizations often combine Grant and Block Controls to fine-tune access based on user context. For instance, you could:

* Require MFA and compliant devices for users accessing sensitive apps, but block access entirely for users from untrusted locations.
* Require a password change for users flagged with high-risk sign-ins and block access for users from non-compliant devices.

By layering different controls, you can ensure that access is restricted unless multiple security measures are met, significantly reducing the risk of unauthorized access.

### **Best Practices for Configuring Controls**

**1. Start with Grant Controls Before Blocking Access:**

In most cases, it’s best to implement Grant Controls (e.g., MFA, device compliance) before blocking access outright. This gives users a chance to meet security requirements without being unnecessarily denied access.

**2. Test Session Controls:**

Before enforcing session controls like sign-in frequency, test them with a small user group to ensure that they don’t cause disruptions or unnecessary friction.

**3. Monitor Sign-in Logs:**

Always monitor Azure AD sign-in logs to ensure that the correct controls are being triggered. This helps you spot any misconfigurations or user issues early on.

**4. Use Report-Only Mode:**

When rolling out new Conditional Access policies, use **Report-only mode** to test the impact of your controls before fully enforcing them. This helps ensure that legitimate users are not unintentionally blocked from accessing resources.
