# Token Protection: Conditional Access (Public Preview)

## Overview

Token protection is a Conditional Access feature currently in public preview in Microsoft Entra ID, also known as token binding. Its main purpose is to reduce the impact of token theft attacks by ensuring that a token can only be used by the device it was intended for. Token theft can occur through hijacking or replay attacks, where an attacker gains access to the token and can impersonate the victim until the token either expires or is revoked. Although token theft is relatively uncommon, the damage it can cause is significant, which makes preventive measures like token protection crucial.

### **How Token Protection Works:**&#x20;

Token protection uses a cryptographically secure mechanism to bind a token to a specific device, creating what is called a client secret. When a device, such as one running Windows 10 or later, is registered with Microsoft Entra ID, its primary identity is bound to the device itself. This ensures that only the tokens that are tied to the device, known as Primary Refresh Tokens (PRTs), can be used by applications to access resources. The client secret is essential—without it, the token becomes useless. Essentially, this prevents attackers from using stolen tokens on other devices, as they would need access to the original device's client secret.

### **Preview Status and Availability**

Token protection is currently in public preview, which means it is available for testing but may still be subject to changes before its general availability. As part of the preview, administrators have the ability to create Conditional Access policies that require token protection for sign-in tokens (refresh tokens) specifically for some Microsoft 365 services, such as Exchange Online and SharePoint Online. This feature is available for use in desktop applications on Windows devices.

### **Recent Changes to Token Protection**

As part of the public preview, several changes have been made since its initial release. In late June 2023, the terminology used in sign-in logs was updated—specifically, the string used for "enforcedSessionControls" and "sessionControlsNotSatisfied" was changed from "Binding" to "SignInTokenProtection." This change affects queries on sign-in log data, which need to be updated accordingly to reflect the new terminology.

### **Requirements for Token Protection**

To use token protection with Conditional Access, there are certain requirements for both devices and applications. The supported configurations include:

* **Windows 10 or newer devices** that are either Microsoft Entra joined, hybrid joined, or Microsoft Entra registered.
* Specific versions of key client applications are also required, including:
  * **OneDrive sync client** version 22.217 or later.
  * **Teams native client** version 1.6.00.1331 or later.
  * **Power BI desktop** version 2.117.841.0 or later.
  * **Visual Studio 2022 or newer** when using the "Windows authentication broker" for sign-in.
  * **Office Perpetual clients** are not supported.

### **Known Limitations**&#x20;

There are a number of known limitations for token protection in this preview:

* **External users** (e.g., Microsoft Entra B2B users) are not supported and should not be included in Conditional Access policies requiring token protection.
* Certain applications do not support signing in using token protection, which will result in users being blocked when trying to access Exchange Online or SharePoint Online. Examples include:
  * **PowerShell modules** that access Exchange, SharePoint, or Microsoft Graph scopes managed by Exchange or SharePoint.
  * **PowerQuery extension for Excel**.
  * **Extensions to Visual Studio Code** that access Exchange or SharePoint.
  * **The new Teams 2.1 preview client** has a known bug that causes it to be blocked after sign-out, which will be fixed in a future update.
* **Unsupported Windows client devices** include Windows Server, Surface Hub, and Windows-based Microsoft Teams Rooms (MTR) systems.

### **Licensing Requirements**

To use token protection, an organization must have **Microsoft Entra ID P2 licenses**. This feature is part of Microsoft Entra ID Protection and will remain tied to the P2 license once it becomes generally available. For more information, organizations can compare available features of Microsoft Entra ID to determine the right licensing for their needs.

### **Deployment Recommendations**

Deploying token protection should be smooth for users when they are using compatible devices and applications. However, to avoid disruptions due to incompatibility, Microsoft recommends the following deployment approach:

1. **Start with a pilot group**: Begin with a smaller group of users to verify compatibility and functionality.
2. **Report-only mode**: Initially create a Conditional Access policy in report-only mode, which allows administrators to monitor its impact without enforcement.
3. **Log monitoring**: Capture both interactive and non-interactive sign-in logs, and analyze them for a sufficient period to identify any potential issues.
4. **Expand gradually**: Once the pilot is successful, expand the scope of the policy to include additional users.
5. **Known good users**: Add users that have been verified for compatibility to the enforcement policy to ensure minimal issues.

This incremental approach helps to mitigate the risk of any application or device incompatibility when enforcing token protection.

### **Creating a Conditional Access Policy**

To create a Conditional Access policy that enforces token protection for Exchange Online and SharePoint Online on Windows devices:

1. Sign in to the **Microsoft Entra admin center** as a Conditional Access Administrator.
2. Navigate to **Protection > Conditional Access > Policies**.
3. Select **New policy** and give it a meaningful name. Microsoft recommends creating a naming standard for policies for better management.
4. Under **Assignments**, specify which users or groups the policy applies to, and explicitly exclude emergency access accounts (e.g., "break-glass" accounts).
5. Under **Target resources**, select **Office 365 Exchange Online** and **Office 365 SharePoint Online**. Do not select the broader Office 365 application group, as this may result in unintended failures.
6. Configure conditions for **Device platforms** to apply the policy to Windows devices and set **Client apps** to only apply to mobile apps and desktop clients.
7. Under **Access controls**, select **Require token protection for sign-in sessions** and save the policy in **report-only mode**.
8. Once confident with the results of report-only mode, administrators can move the policy to **enabled** mode to start enforcement.

### **Monitoring and Enforcement**

After deploying a Conditional Access policy with token protection, it is essential to monitor its enforcement:

* Use the **Microsoft Entra sign-in logs** to verify if the token protection policy is being applied as intended. Navigate to **Identity > Monitoring & health > Sign-in logs** in the Microsoft Entra admin center, and look for specific entries to confirm that the policy requirements have been satisfied.
* Use **Log Analytics** to perform more advanced queries on interactive and non-interactive sign-in logs, which helps identify blocked requests and ensure that legitimate users are not impacted.
  * For example, queries can be used to examine blocked versus allowed requests based on the **application** or by individual **users**.
  * The syntax for these queries includes selecting specific log data, filtering by the applications (e.g., Exchange Online and SharePoint Online), and extending session control attributes to determine whether the policy requirements were met.

Administrators are encouraged to run these monitoring activities before and after the policy is enforced to assess its impact on users and applications.
