# Basic vs Advanced Security Auditing

## **Overview**

**Basic vs. Advanced Security Auditing** in Windows refers to the granularity and control over which events are logged. Let’s break down both types, their differences, and which Windows versions they apply to based on the official Microsoft documentation and other relevant insights.

### **1. Basic Security Auditing**

* **Scope:** High-level or general security events such as successful/failed logins, account changes, policy changes, etc.
* **Categories:** Basic auditing focuses on **broad actions** and **event categories**:
  * Account logon events (e.g., user login success/failure)
  * Logon/logoff events
  * Object access attempts (e.g., access to files, folders)
  * Policy change events
* **Use Case:**
  * Useful when monitoring overall system security with less detailed logging.
  * Easier to configure and generate fewer logs, which is helpful in environments that need to conserve storage or avoid overwhelming security teams.
* **Configuration:** Enabled through the Local Security Policy (GPO), under `Security Settings` > `Local Policies` > `Audit Policy`.
* **Windows Versions Supported:** Available on **Windows Server and client editions**, such as Windows 10/11, Server 2012 R2, Server 2016, and later versions.

### **2. Advanced Security Auditing**

* **Scope:** Provides **more detailed control** over the types of events that are audited, allowing organizations to track specific activities.
* **Categories:** Introduced additional audit settings beyond basic ones, with granular **subcategories** such as:
  * **Process tracking:** Detailed events on process creation and termination.
  * **Logon events:** Extra details such as interactive vs. remote logins.
  * **Directory service access:** Deep insights into changes and queries in Active Directory.
  * **Detailed Object Access:** Logs fine-grained access control attempts on files or objects, including access control list (ACL) information.
* **Use Case:**
  * Recommended for **high-security environments** that require precise tracking, such as financial institutions or military setups.
  * Helps correlate **specific activities** (like a process injection attempt) with user actions or suspicious access patterns.
* **Configuration:** Available via **Advanced Audit Policy Configuration** in Group Policy:
  * Found under:\
    `Computer Configuration` > `Windows Settings` > `Security Settings` > `Advanced Audit Policy Configuration` > `Audit Policies`.
  * Allows enabling or disabling individual **subcategories** of audit events to avoid excess noise in logs.
* **Windows Versions Supported:** Advanced auditing applies to **Windows Server (2012 R2 and later)** and **client OSes (Windows 7/8/10/11)**. It provides more control compared to the basic audit policy settings available on older systems like **Windows XP** or **Server 2003**.

### **Comparison Chart: Basic vs. Advanced Auditing**

| **Feature**              | **Basic Auditing**          | **Advanced Security Auditing**                |
| ------------------------ | --------------------------- | --------------------------------------------- |
| **Level of Granularity** | General categories          | Fine-tuned, per-event logging                 |
| **Control**              | Limited to broad actions    | Specific event subcategories                  |
| **Noise (Log Volume)**   | Lower (fewer events)        | Higher (more detailed logs)                   |
| **Use Case**             | General monitoring          | Detailed forensic tracking and threat hunting |
| **Configuration Method** | Local Policy > Audit Policy | GPO > Advanced Audit Policy Configuration     |
| **Supported Systems**    | Windows 7+, Server 2008+    | Windows 7+, Server 2012 R2+                   |

### Which Auditing Should I Use?

* **Basic Auditing** is useful when you need **quick, lightweight monitoring**.
* **Advanced Auditing** gives organizations **granular visibility** over system activities, making it ideal for environments with **specific compliance** or security needs.

Both auditing types can be applied to **Windows Server and client editions**, and the right choice depends on the need for granularity. For security teams focused on detailed incident response, **advanced auditing** offers better flexibility and control.

## Basic Auditing

{% embed url="https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/basic-security-audit-policies" %}

## Advanced Auditing

{% embed url="https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/advanced-security-auditing" %}

