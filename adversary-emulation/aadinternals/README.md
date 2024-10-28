# AADInternals

## Overview

AADInternals is a powerful PowerShell toolkit created by Dr. Nestori Syynimaa that focuses on Azure Active Directory (AAD) and Microsoft Entra ID. It is widely used by red teamers, penetration testers, and security researchers for attack simulation, tenant enumeration, and privilege escalation within Microsoft 365 environments. Below are key aspects of AADInternals and how it can assist in security testing:

### **Key Features of AADInternals**

* **Tenant Enumeration and Reconnaissance**:
  * Retrieve tenant information, including domain names, object IDs, and tenant IDs.
  * Identify federated domains (useful for password spraying and MFA bypass).
* **Authentication and Password Spray Attacks**:
  * Perform **password spray** attacks on cloud identities.
  * Verify credentials across tenants without triggering excessive alerts.
* **Token Extraction and Manipulation**:
  * Extract **OAuth tokens** for authenticated users.
  * Impersonate users by manipulating tokens for various services, such as Microsoft Graph.
* **Privilege Escalation**:
  * Exploit misconfigurations like **OAuth applications with overly broad permissions**.
  * Utilize **admin consent flows** to escalate privileges stealthily.
* **MFA Bypass Techniques**:
  * Identify **federated domains** that are not protected by Conditional Access policies.
  * Exploit misconfigurations in federated domains to bypass MFA.
* **Service Principal Attacks**:
  * Enumerate **service principals** and assess their role assignments.
  * Retrieve credentials and secrets for service principals.
* **Backdoor Creation in Azure AD**:
  * Create **persistent backdoors** using application registrations with consented permissions.
  * Register applications with tokens that allow long-term access to resources.
* **Incident Response and Forensics**:
  * Monitor and investigate **AAD activities** by pulling logs and tokens.
  * Retrieve information about Conditional Access policies and user roles.

### AADInternal Github

{% embed url="https://github.com/Gerenios/AADInternals" %}
