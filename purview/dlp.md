# DLP

### **What is Data Loss Prevention (DLP)?**

**Data Loss Prevention (DLP)** is a set of tools and processes that:

> **Detect and prevent the unauthorized sharing, transmission, or use of sensitive information.**

In other words, DLP ensures sensitive information like **credit card numbers**, **financial data**, or **personal health information** **does not leave** your organization **accidentally** or **intentionally**.

**Microsoft Purview DLP** helps you automatically monitor and control this across:

* **Emails** (Exchange Online)
* **Files and Documents** (SharePoint, OneDrive)
* **Chats** (Microsoft Teams)
* **Endpoints** (Windows 10/11 devices)

***

### **Why Is DLP Important?**

| Reason                            | Example                                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| **Prevent Data Breaches**         | Block emails containing credit card numbers from leaving the company.                     |
| **Meet Compliance Requirements**  | Enforce policies to comply with GDPR, HIPAA, PCI-DSS.                                     |
| **Protect Intellectual Property** | Stop proprietary designs or trade secrets from being shared externally.                   |
| **Reduce Insider Risks**          | Detect and stop risky behavior like employees sending sensitive files to personal emails. |

Without DLP, organizations are vulnerable to **accidental leaks** and **intentional data theft**.

***

### **How DLP Works in Microsoft Purview**

A **DLP policy** defines:

* **What to protect**: Sensitive information (e.g., financial data, health records).
* **Where to protect it**: Emails, files, chats, endpoints.
* **What actions to take**: Block, warn, encrypt, or log when a rule is triggered.

**Typical DLP Workflow:**

```
rustCopyEditCreate Policy --> Define Rules --> Apply Policy --> Monitor --> Respond
```

Each DLP policy contains:

* **Conditions**: What should trigger the policy (e.g., email contains SSN).
* **Actions**: What happens when the condition is met (e.g., block the email).
* **User notifications**: Alert users and educate them before or after a violation.
* **Incident reports**: Notify admins or compliance officers about policy matches.

***

### **DLP Policy Templates**

Microsoft Purview provides **ready-to-use templates** for common scenarios:

| Template Name               | Description                                                      |
| --------------------------- | ---------------------------------------------------------------- |
| **U.S. Financial Data**     | Protect credit card, ABA routing, and U.S. bank account numbers. |
| **U.S. Health Information** | Protect personal health information (PHI) under HIPAA.           |
| **GDPR Data**               | Protect personal data under GDPR regulations.                    |
| **Custom Policies**         | Create your own based on organizational needs.                   |

Templates make it easy to **quickly deploy** DLP without starting from scratch.

***

### **DLP Locations: Where You Can Protect Data**

| Location                        | Protection Scope                                               |
| ------------------------------- | -------------------------------------------------------------- |
| **Exchange Online**             | Emails and attachments.                                        |
| **SharePoint Online**           | Documents and metadata.                                        |
| **OneDrive for Business**       | Personal documents.                                            |
| **Microsoft Teams**             | Chats and shared files.                                        |
| **Endpoints (Windows Devices)** | Local files copied to USB, printed, or uploaded to cloud apps. |

You can target **one or more locations** in a single policy depending on your needs.

***

### **DLP Actions and User Notifications**

When a DLP policy is triggered, you can:

| Action      | Description                                                           |
| ----------- | --------------------------------------------------------------------- |
| **Block**   | Prevent the user from completing the action (e.g., sending an email). |
| **Warn**    | Allow the user to override the block with justification.              |
| **Encrypt** | Automatically encrypt the content.                                    |
| **Notify**  | Send a policy tip to the user and/or an alert to admins.              |

**Policy tips** are critical because they:

* Educate users **in real-time**.
* Reduce the number of false positives.
* Promote a **culture of security awareness**.

***

### **Monitoring DLP Events**

Once DLP policies are active, you can monitor:

* **Matches**: How many times the policy was triggered.
* **Incidents**: Details about each violation.
* **Reports**: Trends, locations, users, and severity of violations.

Reports help you fine-tune your policies over time.
