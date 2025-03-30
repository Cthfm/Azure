# Defensive Strategies

## Defensive Strategies for Discovery Techniques in Azure

In Microsoft Azure environments, discovery techniques are often the first step adversaries use to map out infrastructure, identities, storage, and network configurations before launching further attacks. Because many of these actions closely resemble legitimate administrative behavior, they can be difficult to detect without proper controls. Defensive strategies must focus on limiting unnecessary visibility, enforcing least privilege, and continuously monitoring for anomalous enumeration activity. This includes implementing strong role-based access control (RBAC), leveraging Conditional Access and Privileged Identity Management (PIM), auditing Azure CLI and Graph API usage, and deploying tools like Microsoft Defender for Cloud and Sentinel to detect and respond to reconnaissance activity. By proactively restricting access and identifying early indicators of unauthorized discovery, organizations can significantly reduce the attacker’s ability to understand and exploit the Azure environment.

### **Account Discovery (T1087.004 – Cloud Account Discovery)**

Attackers enumerate user accounts to map out identity structures.

✅ **Restrict Directory Read Permissions**\
Use Entra ID roles carefully—only grant `Directory Readers` to required accounts.

✅ **Enable Entra ID PIM (Privileged Identity Management)**\
Use time-bound, approval-based elevation for roles like `User Administrator`.

✅ **Monitor Azure CLI and PowerShell Usage**\
Track use of commands like `az ad user list`, `Get-AzureADUser`, and audit logs for suspicious enumeration.

✅ **Alert on Bulk Account Enumeration**\
Create Microsoft Sentinel rules to detect high-volume user listings or access to `/users` endpoint via Graph API.

### **Cloud Infrastructure Discovery (T1580)**

Attackers enumerate cloud infrastructure like VMs, databases, and resource groups.

✅ **Implement Role-Based Access Control (RBAC)**\
Restrict `Reader` role and avoid assigning it broadly.

✅ **Limit Subscription Read Access**\
Segment access with Management Groups and Azure Blueprints.

✅ **Audit ‘az resource list’ and REST API Calls**\
Use Defender for Cloud and Microsoft Sentinel to monitor Azure Resource Graph queries.

✅ **Detect Use of High-Privilege Read Roles**\
Alert when roles like `Owner`, `Contributor`, or `Reader` are assigned unexpectedly.

***

### **Cloud Service Dashboard (T1590.001)**

Adversaries log into the Azure Portal to visually discover assets.

✅ **Require MFA for Portal Access**\
Enforce Conditional Access to require MFA for `portal.azure.com`.

✅ **Enable Sign-in Risk Policies**\
Detect unfamiliar sign-in behavior and risky locations.

✅ **Log Access to the Azure Portal**\
Review sign-ins to `Azure Portal` app and detect logins from new IPs or devices.

✅ **Terminate Sessions & Investigate**\
For any unrecognized login, terminate session via Entra ID and trigger incident response playbook.

***

### **Cloud Service Discovery (T1526)**

Adversaries enumerate regions and service availability.

✅ **Restrict CLI/API Access to Trusted Users**\
Only allow service discovery commands (e.g., `az account list-locations`) for trusted accounts.

✅ **Lock Down Service Principal Access**\
Use least-privilege principles for any SPN or identity used in automation.

✅ **Detect Excessive Metadata Queries**\
Alert on high-frequency use of APIs or CLI commands listing regions, subscriptions, etc.

✅ **Investigate Accounts Performing Enumeration**\
Flag identities making repeated or abnormal discovery calls and review associated IPs.

### **Cloud Storage Object Discovery (T1613)**

Adversaries look for publicly accessible or misconfigured storage.

✅ **Disable Public Access to Storage Containers**\
Set `allowBlobPublicAccess` to false at the storage account level.

✅ **Use Private Endpoints for Storage Access**\
Ensure traffic is internal and uses Azure Private Link.

✅ **Scan for Open Containers**\
Use Azure Policy to flag storage accounts with public access enabled.

✅ **Enable Defender for Storage**\
Generate alerts for anonymous access attempts or data exfiltration.

### **Log Enumeration (T1005)**

Adversaries try to access audit or diagnostic logs.

✅ **Restrict Log Access with RBAC**\
Only grant `Monitoring Reader` or `Log Analytics Reader` to trusted roles.

✅ **Encrypt Logs and Use Diagnostic Settings**\
Route logs securely to a Log Analytics workspace with access control.

✅ **Track `az monitor` Usage**\
Review use of CLI commands like `az monitor activity-log list`.

✅  **Alert on Unauthorized Log Access Attempts**\
Detect access to logs from unexpected users or IPs.

### **Network Service Discovery (T1046)**

Adversaries scan VNets or use NSG data to identify reachable services.

✅ **Use NSGs and Azure Firewall to Block Inbound Scanning**\
Apply deny rules to block unauthorized lateral movement.

✅ **Segment Networks with Subnets and Route Tables**\
Limit visibility between resources using internal firewalls.

✅**Log and Analyze NSG Flow Logs**\
Monitor for internal scanning (e.g., connections to multiple IPs/ports).

✅ **Detect Port Scans from Within the Network**\
Alert on use of tools like `nmap` or behavior indicative of lateral scanning.

### **Network Sniffing (T1040)**

Adversaries may sniff traffic from compromised VMs.

✅ **Use Encrypted Protocols**\
Enforce TLS for internal and external services.

✅ **Deploy Endpoint Detection & Response (EDR)**\
Monitor for tools like `tcpdump` and unusual process execution.

✅ **Log Process Creation Events in Azure VMs**\
Enable Defender for Endpoint to track packet capture attempts.

✅ **Quarantine VM with Evidence of Sniffing**\
Isolate compromised VM and collect memory/process data for forensic review.

### **Password Policy Discovery (T1201)**

Attackers seek password complexity rules for credential attacks.

✅ **Avoid Legacy Auth Protocols (MSOL)**\
Migrate to modern PowerShell (`Microsoft.Graph`) and disable legacy endpoints.

✅ **Enable Strong Password Policy**\
Use Entra ID B2B policies or custom conditional access to enforce strong auth.

✅  **Monitor Access to Policy Data**\
Detect when users invoke `Get-MsolPasswordPolicy` or similar.

✅  **Limit Access to Directory Configuration APIs**\
Flag use of legacy tools to extract config data.

***

### **Permission Groups Discovery (T1069.003 – Cloud Groups Discovery)**

Adversaries enumerate roles and groups in Entra ID.

✅ **Restrict Group & Role Visibility**\
Prevent non-admin users from listing group memberships.

✅ **Limit Graph API Access**\
Use App Consent Policies to limit exposure of group membership to apps.

✅  **Audit Use of `Get-EntraGroup`, `az role assignment list`**\
Look for suspicious enumeration from unknown devices or service principals.

✅  **Flag Sudden Enumeration from Dormant Accounts**\
Detect and investigate idle accounts suddenly used for enumeration.

### **Software Discovery (T1518 Subtechniques)**

Adversaries explore installed software and system info.

✅ **Restrict Local Admin Rights on Azure VMs**\
Prevent the ability to run diagnostic or discovery tools locally.

✅ **Harden VMs with Microsoft Defender for Endpoint**\
Monitor and block tools like `netstat`, `wmic`, or other recon tools.

✅ **Monitor for Discovery Commands**\
Detect `az vm show`, `netstat`, `tcpdump`, `powershell Get-WmiObject`, etc.

✅ **Alert on Execution of Recon Tools**\
Correlate suspicious process execution with network traffic or privilege escalation.

### **📌** Summary Table of Defensive Strategies

| MITRE Technique                             | Prevention                            | Detection                          | Response                               |
| ------------------------------------------- | ------------------------------------- | ---------------------------------- | -------------------------------------- |
| **T1087.004** – Cloud Account Discovery     | Limit directory access, use PIM       | Monitor CLI/API user queries       | Investigate enumeration spikes         |
| **T1580** – Cloud Infrastructure Discovery  | RBAC, Blueprint segmentation          | Monitor resource listings          | Flag unexpected readers                |
| **T1590.001** – Cloud Dashboard Access      | MFA for portal, Sign-in risk policies | Log & audit portal sessions        | Revoke sessions, block IP              |
| **T1526** – Cloud Service Discovery         | Limit CLI/API access                  | Detect metadata queries            | Review identity access logs            |
| **T1613** – Cloud Storage Object Discovery  | Block public blob access              | Azure Policy, Defender for Storage | Alert on public access or exfiltration |
| **T1005** – Log Enumeration                 | Restrict log reader roles             | Monitor `az monitor` usage         | Alert on unauthorized access           |
| **T1046** – Network Service Discovery       | Block scans with NSG                  | Analyze NSG Flow Logs              | Alert on lateral scan activity         |
| **T1040** – Network Sniffing                | Encrypt traffic, enable EDR           | Monitor packet capture tools       | Quarantine VM, review memory           |
| **T1201** – Password Policy Discovery       | Disable MSOL, enforce strong policies | Log policy queries                 | Review tool usage                      |
| **T1069.003** – Permission Groups Discovery | Limit role visibility                 | Detect enumeration cmdlets         | Investigate dormant account use        |
| **T1518.x** – Software Discovery            | Restrict local admin                  | Detect recon command use           | Correlate with other activity          |
