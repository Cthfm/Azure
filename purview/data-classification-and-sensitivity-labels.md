# Data Classification and Sensitivity Labels

## **Data Classification and Sensitivity Labels**

***

### **What is Data Classification?**

**Data classification** is the process of identifying, organizing, and tagging data based on its **sensitivity**, **value**, and **regulatory requirements**.

In simple terms:

> **It’s how you understand what your data is and how sensitive it is.**

Classification is critical because it lets you **apply protections** based on the **risk** the data carries.

For example:

* Public documents may require no protection.
* Internal financial reports may need encryption and restricted sharing.
* Health records (HIPAA) must be tightly controlled.

***

### **Why Does Data Classification Matter?**

| Reason                    | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| **Regulatory Compliance** | Meet requirements like GDPR, HIPAA, PCI-DSS.            |
| **Risk Reduction**        | Protect high-value and sensitive information.           |
| **Business Continuity**   | Ensure only authorized people can access critical data. |
| **Incident Response**     | Identify the type of data compromised during a breach.  |

Without classification, it’s impossible to enforce **Data Loss Prevention (DLP)**, **Insider Risk Management**, or **Retention** effectively.

***

### **Sensitive Information Types (SITs)**

Microsoft Purview uses **Sensitive Information Types (SITs)** to **automatically detect** sensitive data within files, emails, chats, and databases.

**Examples of built-in SITs:**

* Credit Card Numbers
* U.S. Social Security Numbers
* Health Insurance Claim Numbers (HICNs)
* EU Passport Numbers
* ABA Routing Numbers

Each SIT uses **patterns**, **keywords**, and **checksums** to recognize real-world sensitive information.

> **Important:**\
> You can also create **custom sensitive information types** to meet unique business needs.

***

### **What are Sensitivity Labels?**

A **Sensitivity Label** is a **tag** that you apply to data that _classifies_ and _protects_ it at the same time.

A label can:

* **Classify** the data (e.g., “Confidential” or “Highly Confidential”)
* **Protect** the data using **encryption** and **rights management**
* **Control** actions (e.g., block sharing outside your organization)
* **Apply watermarks** or **headers/footers** on documents

**Example:**

| Label Name       | Actions Taken                            |
| ---------------- | ---------------------------------------- |
| **Confidential** | Encrypt document, block external sharing |
| **Public**       | No encryption, allow sharing             |

***

### **How Sensitivity Labels Work**

When you apply a label:

1. It attaches **metadata** to the file or email.
2. The label can **travel with the data** even if it leaves your network.
3. The label can **trigger automatic protections** like encryption or DLP policies.

Microsoft 365 apps like Word, Excel, Outlook, and Teams are **label-aware**.\
This means users can manually label content, or Purview can **auto-label** based on policy.

***

### **Automatic vs Manual Labeling**

| Approach               | How It Works                                                                | Example                                                                 |
| ---------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Manual Labeling**    | The user selects the label themselves.                                      | When drafting an email, a user marks it as "Confidential."              |
| **Automatic Labeling** | Purview automatically applies a label based on sensitive information types. | Purview detects a Credit Card Number and applies "Highly Confidential." |

> **Tip:**\
> You can force users to apply a label or recommend one using policy settings.

***

### **Unified Labeling in Microsoft Purview**

Microsoft **unified** labeling so that **Sensitivity Labels** are:

* Available across **Microsoft 365** (Exchange, SharePoint, OneDrive, Teams)
* Applied consistently across **Windows devices**, **iOS**, **Android**, **Mac**, and **web apps**
* Managed from a single place: **Microsoft Purview Compliance Portal**

**Benefits of Unified Labeling:**

* Centralized management
* Seamless end-user experience
* Consistent enforcement across all services
