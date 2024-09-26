# Conditions for Conditional Access

## **What Are Conditional Access Conditions?**

Conditions in Conditional Access policies define **when** the policy should be enforced. They help ensure that access control decisions are based on contextual factors, such as the user’s location, device state, or sign-in risk. By configuring conditions, you can precisely tailor policies to specific situations, ensuring stronger security while minimizing disruptions for users.

Each condition allows you to control access based on factors like **who** is signing in, **where** they are signing in from, and the **state** of their device.

### **Types of Conditional Access Conditions**

Azure AD Conditional Access supports several types of conditions that help define the context of access. These conditions include:

* **User or Group Membership**
* **Cloud Applications**
* **Sign-in Risk**
* **Device Platforms**
* **Location**
* **Client Applications**
* **Device State**

### **User or Group Membership**

This condition allows you to target specific users or groups in your Conditional Access policy.

**How It Works:**

* **Targeting All Users**: You can apply a policy to all users in your organization. For example, you may want to require MFA for all employees accessing sensitive applications like Microsoft 365.
* **Targeting Specific Groups**: You can apply policies to specific Azure AD groups, such as admins, HR, or contractors. For example, you might enforce stricter controls on high-privilege roles (e.g., Global Admins).
* **Excluding Users**: You can exclude users from policies, such as break-glass or emergency access accounts, which should not be restricted by Conditional Access.

**Example Use Case:**

A Conditional Access policy could be applied to the **Global Administrators** group, requiring MFA for any admin actions.

### **Cloud Applications**

This condition allows you to apply Conditional Access policies to specific cloud applications. Instead of applying security controls across all apps, you can target particular apps that handle sensitive data or have higher security requirements.

**How It Works:**

* **All Cloud Apps**: You can apply a Conditional Access policy to all cloud applications within your Azure AD tenant.
* **Select Specific Apps**: You can target individual applications, such as **Microsoft 365**, **Salesforce**, or a custom enterprise app, for stricter access controls.

**Example Use Case:**

An organization may want to apply Conditional Access policies to ensure that users must complete MFA before accessing a sensitive app like **Azure Management** or **Microsoft 365**.

### **Sign-in Risk**

The **Sign-in Risk** condition is based on the evaluation of a user’s sign-in behavior. Azure AD Identity Protection analyzes sign-in patterns to detect potentially risky or unusual behavior and categorizes the risk into low, medium, and high.

**Risk Categories:**

* **Low Risk**: Typically a normal sign-in attempt with no detected anomalies.
* **Medium Risk**: Behavior that could indicate an attack, such as signing in from a new device or location.
* **High Risk**: Clear signs of a compromised account, such as a known data breach associated with the user’s credentials.

**How It Works:**

You can configure Conditional Access to apply stricter controls based on the risk level:

* **Low Risk**: No additional controls might be required.
* **Medium Risk**: Require MFA to confirm the user's identity.
* **High Risk**: Block access or require a password reset.

**Example Use Case:**

A Conditional Access policy could block access or require a password reset if the sign-in risk is determined to be high. This is often used to prevent compromised accounts from accessing sensitive resources.

### **Device Platforms**

This condition allows you to specify which types of devices (based on operating system) can trigger the policy.

**Supported Device Platforms:**

* **Windows**
* **macOS**
* **iOS**
* **Android**
* **Linux**

**How It Works:**

* You can apply Conditional Access policies to specific device platforms. For example, you might allow access to corporate resources only from **Windows** and **macOS** devices but block access from **Android** and **iOS** devices unless they meet certain compliance requirements.

**Example Use Case:**

An organization may create a Conditional Access policy that blocks access to corporate resources from **Linux** devices, as they are not part of the company’s managed device ecosystem.

### **Location**

Location-based conditions allow you to apply different security measures based on the geographical location or network from which users are signing in. This is commonly used to restrict access from risky or untrusted locations.

**How It Works:**

* **Named Locations**: You can define **trusted locations** (e.g., your corporate office or VPN) using IP address ranges. Policies can then be applied to allow or block access based on these named locations.
* **Country/Region**: You can block or allow access based on the country from which users are attempting to sign in. This is useful for blocking access from regions associated with high levels of cyberattacks.

**Example Use Case:**

An organization might require MFA only for users who are signing in from outside the trusted corporate network, reducing friction for users signing in from the office.

### **Client Applications**

The **Client Apps** condition allows you to enforce policies based on the type of application a user is using to access resources. Azure AD recognizes several types of client applications, including:

* **Browser** (e.g., users accessing apps through a web browser).
* **Mobile apps and desktop clients** (e.g., Outlook mobile or the Teams desktop app).
* **Legacy Authentication** (e.g., apps that don’t support modern authentication like IMAP or POP).

**How It Works:**

You can create Conditional Access policies that require additional security measures for specific client applications:

* For example, you might require MFA for users accessing sensitive data through **browser-based apps** but block access for **legacy authentication protocols** to prevent password spraying attacks.

**Example Use Case:**

A policy could block legacy authentication protocols like IMAP or POP, which are often vulnerable to brute force attacks, while allowing access from modern authentication protocols.

### **Device State**

Device state conditions allow you to require that users access resources only from trusted or compliant devices. This is often done in conjunction with Microsoft Intune or other mobile device management (MDM) solutions.

**How It Works:**

* **Compliant Devices**: Require that devices meet certain security requirements (e.g., encryption, up-to-date security patches).
* **Hybrid Azure AD Joined**: Ensure that devices accessing resources are joined to Azure AD or managed by the organization’s Active Directory.

**Example Use Case:**

An organization might configure a Conditional Access policy that allows access to corporate data only from **compliant devices** that meet internal security policies (e.g., devices managed by Intune).

### **Combining Conditions for Granular Control**

You can combine multiple conditions to create granular and highly customized Conditional Access policies. For example, you might create a policy that applies to:

* **Users in the Global Administrators group** (user condition).
* Who are accessing **Azure Management** (cloud app condition).
* From an **untrusted location** (location condition).
* Using a **non-compliant device** (device state condition).

In this scenario, you might enforce MFA and require device compliance for admins accessing the Azure portal from outside the corporate network.
