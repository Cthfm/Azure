# Defensive Strategies

### **Overview:**

Defensive strategies within the Defense Evasion (TA0005) requires enforcing strong identity controls, network segmentation, data protection, and threat detection. Compliance and security baselines are maintained via Azure Policy, logging, and automated patching, creating a layered defense-in-depth approach to cloud security. This section goes over defensive strategies for each tactic and sub technique.&#x20;

### **1. Abuse Elevation Control Mechanism (T1548)**

#### **Temporary Elevated Cloud Access (T1548.005)**

**Mitigation:**

* Require Justification & Approval: Enforce approval workflows in Azure Privileged Identity Management (PIM) to ensure elevated access is properly reviewed.
* Shorten Activation Time: Limit Global Admin and other privileged role activations to the minimum necessary duration.
* Enable PIM Alerts & Logging: Monitor PIM role activations and create alerts for unexpected admin promotions.
* Review PIM Logs Regularly: Analyze PIM logs in Azure Monitor and Microsoft Sentinel for abnormal privilege escalation activity.

### **2. Exploitation for Defense Evasion (T1211)**

#### **Exploitation of Vulnerabilities**

**Mitigation:**

* Keep Cloud Services Updated: Regularly review and apply security patches for Azure services when you are responsible for upgrades.
* Enable Threat Detection: Use Microsoft Defender for Cloud to detect exploits targeting Azure services.
* Limit Jupyter Notebook Access: For CosmosDB and Azure ML, restrict Jupyter Notebook access and require authentication.
* Use Microsoft Defender for Storage: Enable anomaly detection to flag unauthorized access to storage accounts.

### **3. Impair Defenses (T1562)**

#### **Disable or Modify Security Tools (T1562.001)**

**Mitigation:**

* Prevent Defender Disabling: Set an Azure Policy to prevent users from modifying Defender settings.
* Monitor Defender Logs: Create alerts in Microsoft Sentinel logs for services being disabled. &#x20;
* Restrict Privileges: Ensure that Defender for Endpoint settings can only be modified by security admins.

#### **Disable or Modify Cloud Firewall (T1562.007)**

**Mitigation:**

* Enforce NSG Rules via Azure Policy: Prevent unauthorized changes to Network Security Groups (NSGs).
* Enable NSG Flow Logs: Continuously log and monitor traffic flow using Azure NSG Flow Logs.
* Set NSG Modification Alerts: Create alerts in Microsoft Defender for Cloud to detect changes in firewall configurations.

#### **Disable or Modify Cloud Logs (T1562.008)**

**Mitigation:**

* Use Azure Policy: Enforce diagnostic logging across all resources.
* Monitor Logging Changes: Track changes in diagnostic settings, activity logs, and Entra ID logs.&#x20;
* Enable Log Analytics: Forward all logs to a log analytics workspace, storage account, or event hub for storage and retention.

### **4. Modify Authentication Process (T1556)**

#### **MFA Bypass (T1556.006)**

**Mitigation:**

* Use Conditional Access Policies: Require MFA for all high-privilege users, even in trusted locations.
* Monitor Session Tokens: Enable Continuous Access Evaluation (CAE) to invalidate stolen session tokens.
* Implement Identity protection for risky sign-ins.&#x20;

#### **Hybrid Identity Manipulation (T1556.007)**

**Mitigation:**

* Secure AD FS Servers: Use Azure Entra ID Password Protection and ensure AD FS servers have security monitoring enabled.
* Monitor Federation Changes: Track AD FS claims rule modifications in Azure Sentinel.

#### **Conditional Access Policy Manipulation (T1556.009)**

**Mitigation:**

* Require Approval for Policy Changes: Use Privileged Identity Management (PIM) to require admin approval before modifying Conditional Access policies.
* Monitor Conditional Access Logs: Set up alerts in Sentinel or a third party SIEM for unexpected policy changes.

### **5. Modify Cloud Compute Infrastructure (T1578)**

#### **Create Snapshot (T1578.001)**

**Mitigation:**

* Restrict Snapshot Creation: Use Azure RBAC to limit who can create snapshots.
* Monitor Snapshot Activity: Enable alerts in Microsoft Sentinel for snapshot creation events.

#### **Create Cloud Instance (T1578.002)**

**Mitigation:**

* Limit VM Creation: Use Azure Policy to restrict VM creation to approved users.
* Monitor New VM Deployments: Set alerts for unexpected VM deployments in Microsoft Defender for Cloud.

#### **Delete Cloud Instance (T1578.003)**

**Mitigation:**

* Enable Soft Delete for VMs: Use Azure Soft Delete to prevent accidental or malicious VM deletions.
* Monitor VM Deletion Activity: Set up alerts for VM deletions using Azure Activity Logs.

#### **Revert Cloud Instance (T1578.004)**

**Mitigation:**

* Restrict VM Restore Permissions: Use Azure RBAC to limit who can revert VMs to previous snapshots.
* Monitor VM Reversions: Track restore operations using Azure Monitor.

#### **Modify Cloud Compute Configurations (T1578.005)**

**Mitigation:**

* Enforce Configuration Baselines: Use Azure Policy to prevent unauthorized changes to VM diagnostic settings.
* Monitor Configuration Changes: Set up Azure Change Tracking to detect unexpected modifications.

### **6. Modify Cloud Resource Hierarchy (T1666)**

**Mitigation:**

* Restrict Subscription Movement: Use Azure Management Groups and RBAC to prevent unauthorized subscription transfers.
* Monitor Subscription Activity: Set up alerts in Azure Sentinel for unexpected subscription modifications.

### **7. Unused/Unsupported Cloud Regions (T1535)**

**Mitigation:**

* Block Unauthorized Regions: Use Azure Policy to restrict deployments to specific approved regions.
* Monitor Resource Deployments: Set up Azure Monitor alerts for deployments in unused regions.

### **8. Use Alternate Authentication Material (T1550)**

#### **Application Access Token (T1550.001)**

**Mitigation:**

* Use Managed Identities: Avoid service principal secrets and use Managed Identities instead.
* Monitor Token Usage: Set up Azure Sentinel alerts for anomalous API requests.

#### **Web Session Cookie (T1550.004)**

**Mitigation:**

* Use Conditional Access: Require re-authentication for high-risk activities.
* Monitor Cookie Theft Techniques: Enable Microsoft Defender for Endpoint to detect pass-the-cookie attacks.

### **9. Valid Accounts (T1078)**

#### **Default Accounts (T1078.001)**

**Mitigation:**

* Disable Default Credentials: Rotate Storage Account keys regularly and enforce the use of Azure Managed Identities.
* Monitor Storage Access: Enable Azure Storage Analytics to track unauthorized access.

#### **Cloud Accounts (T1078.004)**

**Mitigation:**

* Use Azure Entra ID Identity Protection: Detect leaked credentials and enforce risk-based conditional access.
* Monitor Credential Exposure: Continuously scan for exposed Azure credentials using Microsoft Defender for Identity.

### **General Recommendations:**

* Enable Microsoft Defender for Cloud: Provides built-in detection for many of these attacks.
* Implement Zero Trust: Limit access based on least privilege and enforce strong authentication.
* Use Azure Sentinel or a third party SIEM for Detection: Build detection rules for suspicious privilege escalation, log tampering, and configuration changes.
* Regularly Review Activity Logs: Use Azure Activity Logs, Microsoft Defender for Cloud Apps, and Azure Monitor to track anomalies.
