# DLM

### **What is Data Lifecycle Management (DLM)?**

**Data Lifecycle Management (DLM)** in Microsoft Purview is the process of:

> **Controlling the creation, storage, use, retention, and secure disposal of information over time — automatically and systematically.**

In simple terms, DLM ensures that **data is kept for as long as needed** (for business or legal reasons) and **then securely deleted** when it’s no longer required.

DLM helps organizations **reduce risk**, **optimize storage costs**, and **comply with regulations**.

***

### **Why is DLM Important?**

| Reason                         | Example                                                     |
| ------------------------------ | ----------------------------------------------------------- |
| **Regulatory Compliance**      | Keep financial records for 7 years (SOX compliance).        |
| **Legal Protection**           | Retain emails that might be needed for litigation.          |
| **Reduce Storage Costs**       | Automatically delete obsolete documents and emails.         |
| **Minimize Data Breach Risks** | Remove unnecessary old sensitive data that could be leaked. |

Without DLM, organizations often **keep too much data** — exposing themselves to **unnecessary legal, financial, and security risks**.

***

### **Core Principles of Data Lifecycle Management**

| Stage      | Description                                                |
| ---------- | ---------------------------------------------------------- |
| **Create** | Data is created or received (emails, files, chats).        |
| **Store**  | Data is saved in cloud apps, servers, or devices.          |
| **Use**    | Data is actively used for business operations.             |
| **Retain** | Data is preserved based on legal or business requirements. |
| **Delete** | Data is securely deleted when no longer needed.            |

**DLM automates this process** using retention and deletion policies.

***

### **Retention Policies vs Retention Labels (Quick Review)**

| Feature              | Retention Policy                                | Retention Label                                    |
| -------------------- | ----------------------------------------------- | -------------------------------------------------- |
| **Scope**            | Applied broadly to locations (mailboxes, sites) | Applied to specific items (emails, documents)      |
| **User Interaction** | Invisible to users                              | Can be visible to users                            |
| **Granularity**      | Broad                                           | Fine-tuned, item-level control                     |
| **Use Case**         | General email/file retention                    | Special handling for sensitive or critical content |

**Important:**

* **Retention Policies** = Big, broad strokes.
* **Retention Labels** = Fine-grained, specific control.

***

### **Where Can You Apply DLM Policies?**

Microsoft Purview DLM supports applying policies to:

| Service/Application       | Data Types                             |
| ------------------------- | -------------------------------------- |
| **Exchange Online**       | Emails, Calendar items, Tasks          |
| **SharePoint Online**     | Documents, Lists                       |
| **OneDrive for Business** | Personal files                         |
| **Microsoft Teams**       | Chat messages, Channel messages, Files |
| **Yammer**                | Messages, Posts                        |

You can **configure different retention settings** for each workload depending on business needs.

***

### **DLM Settings Explained**

When creating a retention policy or label, you can specify:

| Setting                                | What It Means                                                                                    |
| -------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Retain content for a specific time** | Preserve content for a minimum number of days/years.                                             |
| **Start retention based on event**     | Trigger retention based on creation, modification, or custom events (e.g., employment end date). |
| **Delete content after retention**     | Automatically delete content after the retention period ends.                                    |
| **Retain content forever**             | Keep content indefinitely until manually deleted.                                                |

You can **mix and match** settings based on regulations or business needs.

***

### **Event-Based Retention**

In addition to regular time-based retention, Microsoft Purview supports **event-based retention**.

Examples of events:

* Employee leaves the company
* Project closes
* Contract expires

Event-based retention ensures you **start the clock** based on a **real-world event**, not just the creation date of the document or email.

***

### **Hands-On Lab: Create a Retention Policy for Email**

**Objective:**\
Create a policy that retains all emails for **7 years**, then automatically deletes them.

#### Step 1: Create a Retention Policy

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **Data Lifecycle Management** → **Microsoft 365** → **Retention Policies**.
3. Click **+ Create**.

#### Step 2: Configure the Policy

* **Name**: **7-Year Email Retention**
* **Locations**: Select **Exchange email**.
* **Retention Settings**:
  * Retain items for **7 years**.
  * After 7 years, **delete items automatically**.
* **Publish** the policy.

#### Step 3: Verify

* Go to an Exchange mailbox.
* Check that the mailbox now shows retention settings under Compliance tags.

***

### **Monitoring and Reporting DLM Policies**

After deploying DLM policies:

* **Reports** in Purview show how many items are being retained or deleted.
* **Audit logs** track changes to retention policies.
* You can **simulate** policies before deploying them live to ensure they behave correctly.

> **Tip:**\
> Always **test retention policies** in a lab or test group before rolling them out organization-wide!

***

### **Summary**

* **Data Lifecycle Management (DLM)** automates the retention and deletion of data across Microsoft 365 services.
* Use **Retention Policies** for broad application and **Retention Labels** for specific, item-level control.
* DLM ensures regulatory compliance, reduces storage costs, and minimizes breach risks.
* Event-based retention allows more precise control triggered by real-world business events.
* Monitoring and testing retention settings are crucial for avoiding accidental data loss.
