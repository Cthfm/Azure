# Risk and Privacy Management

### **What is Risk and Privacy Management in Microsoft Purview?**

**Risk and Privacy Management** in Microsoft Purview focuses on:

> **Identifying, assessing, and mitigating internal risks and protecting individual privacy rights.**

It covers two major areas:

* **Risk Management**: Detecting risky user behavior (like insider threats, data leaks, or policy violations).
* **Privacy Management**: Protecting personal data (PII) and ensuring compliance with data privacy regulations (GDPR, CCPA).

**Key Idea:**

> Protect your organization from internal risks **and** protect individuals' rights at the same time.

***

### **Why Risk and Privacy Management Matters**

| Area                   | Example                                                                         |
| ---------------------- | ------------------------------------------------------------------------------- |
| **Risk Management**    | Detecting an employee downloading hundreds of sensitive files before resigning. |
| **Privacy Management** | Handling a GDPR Subject Rights Request (SRR) for a customer's personal data.    |

Both help organizations:

* Prevent data breaches
* Minimize regulatory fines
* Protect customer trust
* Build a privacy-respecting culture

***

### **Risk Management in Microsoft Purview**

Risk management is primarily handled through **Insider Risk Management**, which you learned about earlier.

It helps you:

* **Detect risky activities**: Unusual file movements, external sharing, risky communication.
* **Prioritize alerts**: Focus investigations on the highest-risk behaviors.
* **Take actions**: Launch investigations, alert managers, apply DLP policies.

Purview uses **machine learning** to detect patterns — not just single events — making it smarter over time.

***

### **Privacy Management in Microsoft Purview**

**Privacy Management** helps organizations **discover, protect, and govern personal data** (also called PII — Personally Identifiable Information).

It provides tools to:

* **Identify** personal data across Microsoft 365 (Exchange, SharePoint, OneDrive, Teams).
* **Manage subject rights requests (SRRs)** under GDPR, CCPA, and similar laws.
* **Monitor privacy risks**, such as oversharing of PII.
* **Automate responses** to privacy inquiries and incidents.

**Key Regulations Covered:**

* **GDPR** (Europe)
* **CCPA** (California)
* **LGPD** (Brazil)
* **HIPAA** (US Healthcare)

***

### **Subject Rights Requests (SRRs)**

A **Subject Rights Request (SRR)** is when an individual asks:

* What personal data you have about them (Data Subject Access Request, or DSAR)
* To delete their data (Right to Erasure)
* To correct their data (Right to Rectification)

Microsoft Purview **streamlines SRRs** by:

1. Searching across Microsoft 365 for personal data tied to the user.
2. Collecting the results automatically.
3. Packaging the data into a report.
4. Allowing privacy teams to review and respond efficiently.

> **Important:**\
> Under GDPR, you must respond to SRRs within **30 days**.

***

### **Privacy Risk Management Features**

| Feature                     | What It Does                                                       |
| --------------------------- | ------------------------------------------------------------------ |
| **Personal Data Discovery** | Automatically finds and maps personal data across cloud locations. |
| **Data Insights**           | Visualize where personal data is stored and how it flows.          |
| **Risk Detection**          | Alerts when personal data is overshared, mishandled, or at risk.   |
| **Policy Enforcement**      | Create policies to minimize data sharing risks (similar to DLP).   |
| **Automated Responses**     | Streamline SRR workflows and incident management.                  |

***

### **How Privacy Management Works**

1. **Discover Personal Data**\
   Purview scans Exchange, SharePoint, OneDrive, Teams for PII.
2. **Assess Risks**\
   Identify locations where PII is shared externally or broadly within the organization.
3. **Respond to Requests**\
   Fulfill subject rights requests easily using prebuilt workflows.
4. **Protect Privacy**\
   Create policies that automatically warn or block risky behavior involving personal data.

***

### **Example Privacy Risks Detected**

| Risk Type               | Example                                                                  |
| ----------------------- | ------------------------------------------------------------------------ |
| **Oversharing**         | A file with 1,000 employee SSNs is shared with “Everyone” in SharePoint. |
| **External Sharing**    | Personal data is shared with external vendors without encryption.        |
| **Shadow Data Storage** | Sensitive files with personal data stored in unauthorized locations.     |
| **Unauthorized Access** | Internal users accessing customer health records without approval.       |

***

### **Hands-On Lab: Submit a Subject Rights Request**

**Objective:**\
Submit and fulfill a Subject Rights Request (SRR) in Purview.

#### Step 1: Create a Subject Rights Request

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **Privacy Management** → **Subject Rights Requests**.
3. Click **+ New Request**.

#### Step 2: Configure Request

* Choose request type (e.g., Access, Deletion).
* Enter the user's name and email.

#### Step 3: Review and Fulfill

* Let Purview discover relevant content.
* Review the collected data.
* Redact sensitive content if needed.
* Export the report to share with the data subject.

***

### **Best Practices for Risk and Privacy Management**

| Practice                                    | Why It Matters                                       |
| ------------------------------------------- | ---------------------------------------------------- |
| **Set up Insider Risk Management policies** | Detect internal risks proactively.                   |
| **Automate Personal Data Discovery**        | Save time and avoid missing critical data.           |
| **Train Staff on Privacy Obligations**      | Build a privacy-aware culture.                       |
| **Respond Promptly to SRRs**                | Avoid fines and reputational damage under GDPR/CCPA. |
| **Monitor Privacy Risk Reports Regularly**  | Catch new risks early.                               |

***

### **Summary**

* **Risk Management** detects risky behaviors like insider threats and data leaks.
* **Privacy Management** protects personal data and ensures compliance with privacy laws (GDPR, CCPA, HIPAA).
* Microsoft Purview automates the discovery of personal data and simplifies subject rights request (SRR) workflows.
* Organizations must continuously **monitor**, **protect**, and **respond** to internal risks and privacy incidents.
