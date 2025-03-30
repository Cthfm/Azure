# Defensive Strategies

### **1.** Defending Against Automated Collection (T1119)

Attackers leverage Azure Automation Accounts, Runbooks, and Logic Apps to collect and exfiltrate data.

#### **Defensive Techniques:**

✅ **Monitor Automation Runbooks and Logic Apps Execution**

* Enable Azure Monitor Logs to track changes in Automation Accounts, Logic Apps, and Runbooks.
* Use Microsoft Defender for Cloud to detect suspicious automation activity.

✅ **Restrict Permissions on Automation Services**

* Apply least privilege access (e.g., restrict `Contributor` roles to only necessary users).
* Use Privileged Identity Management (PIM) for just-in-time access control.

✅ **Disable Unused Automation Accounts**

* Regularly audit unused Automation Accounts and disable or delete them.

✅ **Deploy Conditional Access Policies**

* Prevent automation execution from untrusted locations by enforcing MFA and device compliance policies.

### **2.** Defending Against Data from Cloud Storage (T1530)

Adversaries may target Azure Storage Accounts, Blobs, or File Shares to extract sensitive data.

#### **Defensive Techniques:**

✅ **Enforce Azure Storage Firewall Rules**

* Restrict Storage Account access to specific IP ranges or Virtual Networks.
* Use Private Endpoints to limit exposure to public networks.

✅ **Rotate and Restrict Access to Storage Keys & SAS Tokens**

* Disable account keys and enforce Azure Entra ID authentication for access.
* Set short-lived SAS tokens and revoke old ones when no longer needed.

✅ **Enable Azure Defender for Storage**

* Detect unusual access patterns (e.g., sudden data access from a new location).

✅ **Enable Immutable Storage and Soft Deletes**

* Prevent unauthorized data modifications or deletions by using Blob versioning and retention policies.

### **3.** Defending Against Data from Information Repositories (T1213)

Attackers target Azure DevOps, SQL Databases, and Table Storage for sensitive information.

#### **Defensive Techniques:**

✅ **Audit & Harden Azure DevOps Repositories**

* Use Azure DevOps Access Policies to enforce:
  * MFA for all repository access
  * Branch protection rules to prevent unauthorized code modifications
  * Secret scanning tools (e.g., Microsoft Defender for DevOps).

✅ **Monitor SQL Database Queries & Access**

* Enable SQL Auditing and Threat Detection to log suspicious queries (e.g., `SELECT * FROM users`).
* Restrict public network access and enforce Private Link connections.

✅ **Enforce Role-Based Access Control (RBAC) on Storage Services**

* Avoid using Owner or Contributor roles for general users.
* Assign minimum necessary privileges (e.g., `Storage Blob Data Reader` instead of `Storage Account Contributor`).

✅ **Enable Logging for Information Repositories**

* Use Azure Monitor & Sentinel to detect access spikes or abnormal API calls.

### **4.** Defending Against Data Staged & Remote Data Staging (T1074.002)

Attackers may stage stolen data in temporary storage before exfiltrating it.

#### **Defensive Techniques:**

✅ **Monitor Data Transfers & Enable Anomaly Detection**

* Use Azure Security Center to monitor bulk data movement.
* Enable Azure Sentinel to alert on unusual storage access patterns.

✅ **Prevent Unauthorized Cloud Sync & Third-Party Integrations**

* Disable unauthorized data sync apps (e.g., Dropbox, Google Drive) via Microsoft Defender for Endpoint policies.
* Restrict Azure DevOps Pipelines to trusted IP ranges.

✅ **Audit & Restrict Data Transfer Permissions**

* Enforce DLP (Data Loss Prevention) policies to block unauthorized file uploads.
* Use Conditional Access policies to restrict high-risk data access.

✅ **Block External Data Movement**

* Disable public access to Azure Storage and File Shares.
* Use Defender for Cloud Apps to detect shadow IT data transfers.
