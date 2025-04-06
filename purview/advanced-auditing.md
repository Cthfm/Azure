# Advanced Auditing

### **What is Advanced Auditing in Microsoft Purview?**

**Advanced Auditing** in Microsoft Purview gives organizations:

> **Deeper visibility, longer retention, and faster investigation capabilities for security, compliance, and insider risk investigations.**

Compared to **Standard Auditing** (which is available in Microsoft 365 E3 and similar licenses), **Advanced Auditing** unlocks **critical investigation features**.

**Think of it like this:**\
Standard Auditing = Basic logging for common activities\
Advanced Auditing = **Extended logs, more detail, longer retention, faster access**

***

### **Why Advanced Auditing Matters**

| Reason                                          | Example                                                    |
| ----------------------------------------------- | ---------------------------------------------------------- |
| **Investigate Security Incidents**              | Track exactly what files a compromised account accessed.   |
| **Support Legal and Compliance Investigations** | Retain and retrieve audit logs for months or years.        |
| **Detect Insider Threats**                      | Find unauthorized access to sensitive files or mailboxes.  |
| **Respond Faster**                              | Search large audit datasets instantly without long delays. |

Without advanced auditing, critical investigation data could **expire** too soon — or never be captured at all.

***

### **Key Features of Advanced Auditing**

| Feature                          | Description                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Extended Audit Log Retention** | Keep audit logs for up to **10 years** (instead of 90 days).                                      |
| **Mailbox Access Auditing**      | Detailed logs of who accessed which mailboxes and what actions they performed.                    |
| **Audit Insights**               | Pre-built views to highlight risky or suspicious activity.                                        |
| **High-Value Audit Events**      | Automatically captures critical events (e.g., file downloads, role changes) without manual setup. |
| **Faster Search Performance**    | Optimized for quick searches across millions of audit records.                                    |
| **Customization**                | Create custom retention policies for specific types of audit logs.                                |

***

### **What Gets Captured in Audit Logs?**

Some examples of activities recorded:

| Category                     | Examples                                                                 |
| ---------------------------- | ------------------------------------------------------------------------ |
| **User Activity**            | Logins, file views, file downloads, file deletions.                      |
| **Admin Activity**           | Changes to Exchange settings, Azure AD roles, SharePoint configurations. |
| **Mailbox Access**           | Viewing emails, moving/deleting emails, sending-as another user.         |
| **Data Access**              | Accessing OneDrive or SharePoint files, sharing files externally.        |
| **Role Assignments**         | Adding/removing admin privileges in Azure AD.                            |
| **Compliance Configuration** | Creating DLP policies, editing sensitivity labels.                       |

**Important:**\
Some critical activities (e.g., accessing another user’s mailbox) are only captured with Advanced Auditing.

***

### **Audit Log Retention Tiers**

| License Type                                                             | Retention Period |
| ------------------------------------------------------------------------ | ---------------- |
| **Microsoft 365 E3 / Business Premium (Standard Auditing)**              | 90 days          |
| **Microsoft 365 E5 / E5 Compliance / E5 eDiscovery (Advanced Auditing)** | 1 year           |
| **Custom Retention (with add-on)**                                       | Up to 10 years   |

You can **configure custom audit log retention policies** if you have a 10-year add-on license.

***

### **High-Value Audit Events**

**High-value events** are automatically captured and include:

* Access to sensitive files
* Changes to compliance policies
* Admin role assignments
* Mailbox permission changes
* Data loss prevention (DLP) violations

You **do not need to manually enable** auditing for these events — Purview captures them by default in Advanced Auditing.

***

### **How to Perform an Audit Search**

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **Audit** → **Audit Search**.
3. Set your **search criteria**:
   * Date range
   * Users
   * Activities (e.g., file accessed, mailbox accessed)
4. Run the search.
5. Review and export results if needed.

**Tip:**\
Use **filters** to quickly narrow down large datasets.

***

### **Creating Custom Retention Policies for Audit Logs**

You can create **custom audit log retention policies** to:

* Keep audit logs for specific users or groups longer than the default.
* Retain audit data tied to specific activities (e.g., SharePoint file downloads) longer.

**Steps:**

1. Go to **Audit** → **Audit Retention Policies**.
2. Click **+ Create a policy**.
3. Define:
   * Who the policy applies to (users, groups).
   * What activities it applies to (file downloads, mailbox access).
   * How long to retain logs (1 year, 5 years, 10 years).

***

### **Hands-On Lab: Perform an Audit Search for Sensitive File Access**

**Objective:**\
Search audit logs to see who accessed a sensitive SharePoint file.

#### Step 1: Audit Search

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **Audit** → **Audit Search**.
3. Enter the name of a sensitive file.
4. Set a date range (last 30 days).
5. Filter for **FileAccessed** events.

#### Step 2: Review Results

* See who accessed the file.
* Export the results to CSV for reporting or further investigation.

***

### **Best Practices for Using Advanced Auditing**

| Practice                                       | Why It Matters                                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Enable auditing early**                      | Capture activities from day one to build historical records.                                |
| **Regularly review audit settings**            | Ensure you are capturing the right activities.                                              |
| **Use custom retention**                       | Extend retention for critical users (executives, legal teams).                              |
| **Combine auditing with DLP and Insider Risk** | Create a complete view of potential risks.                                                  |
| **Train investigators**                        | Make sure your security and compliance teams know how to search and interpret logs quickly. |

***

### **Summary**

* **Advanced Auditing** provides deeper, longer, faster audit capabilities compared to standard auditing.
* It captures high-value events automatically — including sensitive file access and role changes.
* **Audit logs can be retained for up to 10 years** with the right licenses.
* **Custom retention policies** allow more precise control over how long specific audit data is kept.
* Advanced Auditing is critical for **security investigations**, **compliance reporting**, and **legal hold readiness**.
