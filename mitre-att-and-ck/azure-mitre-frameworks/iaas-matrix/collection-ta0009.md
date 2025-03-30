---
hidden: true
---

# Collection TA0009

#### MITRE ATT\&CK Collection Techniques in Azure

The **Collection** tactic in the MITRE ATT\&CK framework focuses on adversaries gathering data of interest from a compromised system or cloud environment. Here’s how different sub-techniques under this category apply to Azure:

***

#### **1. Automated Collection (T1119)**

In Azure, adversaries can leverage automation services such as **Azure Automation Accounts**, **Logic Apps**, or **Runbooks** to execute scripts that collect sensitive data.

* **Example:** Attackers may configure a malicious **Runbook** to execute PowerShell commands that extract credentials or files from Azure Storage.
* **Azure Security Tip:** Monitor Automation Accounts and review executed scripts regularly to detect unauthorized collection activities​.

***

#### **2. Data from Cloud Storage**

Azure Storage accounts are often used to store application data, logs, and even virtual hard disks (VHDs). Attackers who gain access to these storage accounts can extract sensitive data.

* **Attack Methods:**
  * **Enumerating Storage Blobs:** Attackers use tools like `Invoke-EnumerateAzureBlobs.ps1` to list available storage containers and extract files​.
  * **Extracting VHDs:** If attackers gain access to an Azure VM's storage account, they can download the **virtual hard disk (VHD)** file, mount it locally, and extract credentials​.
  * **Stealing Shared Access Signature (SAS) Tokens:** These provide time-limited access to Azure Storage and can be abused if not properly restricted​.
* **Azure Security Tip:** Use **Azure Key Vault** for storing sensitive data and limit access to **Storage Accounts** with strict IAM policies​.

***

#### **3. Data from Information Repositories**

Many Azure services store structured or unstructured data in repositories like:

* **Azure SQL Databases** (used for applications, logging, and analytics)
* **Azure Table Storage** (stores semi-structured data, such as logs and telemetry)
* **Azure DevOps Repositories** (can contain API keys and credentials)
* **Attack Methods:**
  * **Extracting SQL Databases:** Attackers with access to an Azure SQL database can dump tables containing sensitive information.
  * **Targeting Git Repositories in Azure DevOps:** Attackers can use `git clone` commands to pull sensitive configuration files or API keys from repositories​.
* **Azure Security Tip:** Regularly audit **role-based access control (RBAC)** permissions and enable **Azure Defender for SQL** to detect anomalous database access.

***

#### **4. Data Staged & Remote Data Staging**

Adversaries often **stage** collected data in a temporary location before exfiltrating it.

* **Attack Scenario in Azure:**
  * Attackers may stage stolen data in **Azure Storage Blobs** or use **OneDrive for Business** to temporarily store exfiltrated data before transferring it externally​.
  * **Cloud Sync Abuse:** Attackers could leverage services like **Azure DevOps Pipelines**, **Dropbox**, or **Bitbucket** to stage and sync stolen data.
* **Azure Security Tip:** Implement **conditional access policies** to restrict data movement and audit logs for unexpected bulk data transfers.

***

#### **Conclusion**

Azure environments introduce unique collection techniques that adversaries can exploit. Key defensive measures include:

* **Implementing strong IAM policies** to restrict access to storage and databases.
* **Enforcing logging and monitoring** with **Microsoft Defender for Cloud** and **Azure Security Center**.
* **Reviewing automation accounts, scripts, and runbooks** for suspicious activities.
* **Auditing API keys and credentials** stored in repositories like Azure DevOps.

Would you like a deeper dive into securing Azure against these techniques? 🚀

**You said:**

Can you write defensive techinques?

**ChatGPT said:**

#### **Defensive Techniques for MITRE ATT\&CK Collection Techniques in Azure**

Defending against **Collection techniques** in Azure requires **visibility, access control, anomaly detection, and proactive monitoring**. Below are defensive measures for each sub-technique.

***

### **1. Defending Against Automated Collection (T1119)**

💡 **Attackers leverage Azure Automation Accounts, Runbooks, and Logic Apps to collect and exfiltrate data.**

#### **Defensive Techniques:**

✅ **Monitor Automation Runbooks and Logic Apps Execution**

* Enable **Azure Monitor Logs** to track changes in **Automation Accounts, Logic Apps, and Runbooks**.
* Use **Microsoft Defender for Cloud** to detect suspicious automation activity.

✅ **Restrict Permissions on Automation Services**

* Apply **least privilege access** (e.g., restrict `Contributor` roles to only necessary users).
* Use **Privileged Identity Management (PIM)** for just-in-time access control.

✅ **Disable Unused Automation Accounts**

* Regularly audit **unused Automation Accounts** and disable or delete them.

✅ **Deploy Conditional Access Policies**

* Prevent automation execution from **untrusted locations** by enforcing MFA and **device compliance policies**.

***

### **2. Defending Against Data from Cloud Storage**

💡 **Adversaries may target Azure Storage Accounts, Blobs, or File Shares to extract sensitive data.**

#### **Defensive Techniques:**

✅ **Enforce Azure Storage Firewall Rules**

* Restrict **Storage Account access** to specific **IP ranges or Virtual Networks**.
* Use **Private Endpoints** to limit exposure to public networks.

✅ **Rotate and Restrict Access to Storage Keys & SAS Tokens**

* **Disable account keys** and enforce **Azure AD authentication** for access.
* Set **short-lived SAS tokens** and revoke old ones when no longer needed.

✅ **Enable Azure Defender for Storage**

* Detect unusual access patterns (e.g., **sudden data access from a new location**).

✅ **Enable Immutable Storage and Soft Deletes**

* Prevent unauthorized data modifications or deletions by using **Blob versioning and retention policies**.

***

### **3. Defending Against Data from Information Repositories**

💡 **Attackers target Azure DevOps, SQL Databases, and Table Storage for sensitive information.**

#### **Defensive Techniques:**

✅ **Audit & Harden Azure DevOps Repositories**

* Use **Azure DevOps Access Policies** to enforce:
  * **MFA for all repository access**
  * **Branch protection rules** to prevent unauthorized code modifications
  * **Secret scanning tools** (e.g., **Microsoft Defender for DevOps**).

✅ **Monitor SQL Database Queries & Access**

* Enable **SQL Auditing and Threat Detection** to log suspicious queries (e.g., `SELECT * FROM users`).
* Restrict **public network access** and enforce **Private Link connections**.

✅ **Enforce Role-Based Access Control (RBAC) on Storage Services**

* Avoid using **Owner or Contributor** roles for general users.
* Assign **minimum necessary privileges** (e.g., `Storage Blob Data Reader` instead of `Storage Account Contributor`).

✅ **Enable Logging for Information Repositories**

* Use **Azure Monitor & Sentinel** to detect access spikes or abnormal API calls.

***

### **4. Defending Against Data Staged & Remote Data Staging**

💡 **Attackers may stage stolen data in temporary storage before exfiltrating it.**

#### **Defensive Techniques:**

✅ **Monitor Data Transfers & Enable Anomaly Detection**

* Use **Azure Security Center** to monitor bulk data movement.
* Enable **Azure Sentinel** to alert on unusual storage access patterns.

✅ **Prevent Unauthorized Cloud Sync & Third-Party Integrations**

* Disable **unauthorized data sync apps** (e.g., Dropbox, Google Drive) via **Microsoft Defender for Endpoint policies**.
* Restrict **Azure DevOps Pipelines** to trusted IP ranges.

✅ **Audit & Restrict Data Transfer Permissions**

* Enforce **DLP (Data Loss Prevention) policies** to block unauthorized file uploads.
* Use **Conditional Access policies** to restrict high-risk data access.

✅ **Block External Data Movement**

* Disable **public access** to **Azure Storage and File Shares**.
* Use **Defender for Cloud Apps** to detect **shadow IT data transfers**.

***

#### **🚀 Proactive Security Measures**

🔹 **Deploy Microsoft Defender for Cloud:** Provides **real-time alerts** for **suspicious activities** across Azure.\
🔹 **Enable Azure Sentinel Threat Hunting:** Detect **anomalous access attempts** and automate response.\
🔹 **Enforce Strong Access Controls:** Implement **Just-in-Time (JIT) access, MFA, and RBAC policies**.\
🔹 **Use Azure Policy & Compliance Controls:** Prevent **misconfigurations** that could expose data.\
🔹 **Regularly Audit Logs & User Activities:** Review **Azure Monitor Logs & Audit Reports** for unauthorized access.
