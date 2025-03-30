# Defensive Strategies

## **Defensive Strategies Against Data Exfiltration in Azure**

Preventing data exfiltration in Microsoft Azure requires a layered security approach, combining access controls, monitoring, network restrictions, and anomaly detection. Below are key strategies to mitigate TA0010 - Exfiltration techniques, specifically T1048 (Exfiltration Over Alternative Protocol) and Transfer Data to Cloud Account.

***

### **1️⃣** Access Control & Identity Protection _(T1537, T1552, T1078)_

**Enforce Least Privilege with Role-Based Access Control (RBAC)**

* Restrict access to Azure Storage Accounts, Virtual Machines, and Automation Accounts.
* Use Managed Identities instead of embedding API keys/secrets in applications.
*   Audit RBAC role assignments regularly using:

    ```powershell
    Get-AzRoleAssignment | Select-Object DisplayName, RoleDefinitionName, Scope
    ```

**Implement Conditional Access & Multi-Factor Authentication (MFA)**

* Require MFA for accessing Azure Storage, Key Vault, and high-privilege accounts.
* Implement device compliance policies in Azure Entra ID Conditional Access to restrict access from non-managed devices.

**Disable Unnecessary SAS Tokens & Access Keys**

* Disable Shared Access Signatures (SAS) where possible and enforce Azure Entra ID authentication.
* Rotate Storage Account keys periodically and monitor unauthorized key usage.

**Use Microsoft Defender for Cloud Apps (MCAS) for Cloud DLP**

* Detect sensitive file transfers from Azure Storage to external cloud services (Google Drive, Dropbox, AWS S3).
* Block unauthorized cloud apps from accessing Azure data.

### **2️⃣** Network-Level Protections _(T1048.003, T1048.002)_

**Restrict Outbound Traffic with NSGs & Azure Firewall**

* Block outbound ICMP, DNS tunneling, and unauthorized protocols using Azure Network Security Groups (NSG) and Azure Firewall.
* Implement deny-by-default policies for unnecessary outbound connections.

**Enable Azure Firewall DNS Proxy & Defender for DNS**

* Detect DNS exfiltration by analyzing anomalous domain queries.
* Block access to unknown, newly registered, or high-risk domains.

**Monitor Unusual Network Traffic with Azure Network Watcher**

* Use Flow Logs & Traffic Analytics to detect high-volume data transfers to untrusted destinations.
* Query NSG Flow Logs to identify unusual outbound transfers:

### **3️⃣** Data Protection & Storage Security _(T1537, T1567.002)_

**Enable Microsoft Defender for Storage**

* Detect anomalous storage access, mass data downloads, and external data transfers.
* Generate alerts for suspicious storage operations, such as:
  * Unusual SAS token usage
  * Access from an untrusted IP or location
  * Bulk file downloads

**Implement Private Endpoints for Azure Storage**

* Prevent direct internet access to Storage Accounts by enforcing Private Endpoints and Service Endpoints.
*   Block public network access:

    ```powershell
    Set-AzStorageAccount -ResourceGroupName "RG" -Name "storageacct" -PublicNetworkAccess Disabled
    ```

🔹 **Monitor Unusual File Access in Azure Storage Logs**

* Use Azure Storage Diagnostic Logs to detect unexpected downloads, deletions, or transfers.
* Query logs using Azure Log Analytics:

### **4️⃣** Threat Detection & Logging _(T1537, T1048)_

**Enable Azure Sentinel & Use Predefined Detection Rules**

* Deploy MITRE ATT\&CK-based analytics in Azure Sentinel to detect data exfiltration.
*   Example Sentinel rule for detecting large outbound transfers:



**Use Microsoft Defender for Endpoint for Host-Level Detection**

* Monitor for PowerShell scripts, tunneling tools, or automation scripts transferring data.
* Detect usage of tools like Iodine (DNS tunneling) or Ptunnel (ICMP exfiltration).

**Enable Azure Activity Logs & Storage Logging**

* Set up alerts for:
  * Unusual SAS token access
  * Storage Account key usage
  * High-frequency API calls to external cloud accounts

### **5️⃣** Blocking Alternative Protocol Exfiltration _(T1048.003, T1048.002, T1048.001)_

**Prevent DNS Tunneling**

* Use Microsoft Defender for DNS to block and alert on high-frequency DNS queries to unknown domains.
* Monitor unusual DNS requests in Azure Sentinel:

**Detect ICMP-Based Exfiltration**

* Use Azure Firewall & NSG Flow Logs to detect high-frequency ICMP traffic.
* Block outbound ICMP requests unless explicitly required.

**Monitor for Protocol Obfuscation**

* Attackers may use encrypted VPNs, TOR, or custom proxy servers to exfiltrate data.
* Block outbound VPN protocols (L2TP, OpenVPN, WireGuard) on NSGs.
* Use Azure Firewall Premium TLS Inspection to detect encrypted exfiltration attempts.

## **📌 Summary Table of Defensive Strategies**

| MITRE Technique                                                                   | Description                                                                                     | Prevention                                                                                                                                                                                              | Detection                                                                                                                           | Response                                                                                                                       |
| --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>T1537</strong><br>Transfer Data to Cloud Account</p>                   | Use of authorized or unauthorized cloud apps (Dropbox, Google Drive, AWS S3) to exfiltrate data | <p>- Use MCAS (Microsoft Defender for Cloud Apps) to block unauthorized cloud services<br>- Implement Conditional Access with app restrictions<br>- Disable browser upload from sensitive resources</p> | <p>- MCAS alerts on third-party app usage<br>- Azure Sentinel: App connections from risky locations/devices</p>                     | <p>- Block access to unsanctioned apps<br>- Revoke session tokens<br>- Review audit logs and re-evaluate RBAC roles</p>        |
| <p><strong>T1567.002</strong><br>Exfiltration Over Web Service: Cloud Storage</p> | Use of Azure Blob/File Storage (or external) for staging and exfil                              | <p>- Enforce Private Endpoints on Azure Storage<br>- Disable public access<br>- Rotate and restrict SAS/token usage<br>- Apply DLP rules on sensitive files</p>                                         | <p>- Azure Storage logs: unusual SAS usage, anonymous access<br>- Defender for Storage alerts on mass downloads or IP anomalies</p> | <p>- Revoke SAS tokens<br>- Block source IPs<br>- Rotate storage keys<br>- Investigate download origin and scope</p>           |
| <p><strong>T1048.003</strong><br>Exfiltration Over Alternative Protocol: DNS</p>  | Covert exfil using DNS tunneling (e.g., iodine, dnscat2)                                        | <p>- Block unknown domains using Defender for DNS<br>- Use deny-by-default outbound DNS egress rules<br>- DNS sinkholing for known C2</p>                                                               | <p>- Defender for DNS: anomalous FQDN volume or entropy<br>- Azure Firewall logs: frequent TXT record queries</p>                   | <p>- Alert and isolate compromised host<br>- Block domain/IP<br>- Perform forensic packet analysis</p>                         |
| <p><strong>T1048.002</strong><br>Exfiltration Over Alternative Protocol: ICMP</p> | Exfiltration via ICMP tunnels (e.g., Ptunnel)                                                   | <p>- Block ICMP outbound traffic in NSGs<br>- Use Azure Firewall to deny non-essential ICMP</p>                                                                                                         | <p>- Flow logs: high-volume ICMP<br>- Defender for Endpoint: tunneling tools on host</p>                                            | <p>- Disable NSG rules<br>- Quarantine VM<br>- Deep-dive host telemetry for tunnel activity</p>                                |
| <p><strong>T1048.001</strong><br>Exfiltration Over Custom Protocol</p>            | Use of TOR, VPN, or custom TCP/UDP channels to evade detection                                  | <p>- Block TOR/VPN ports in NSGs<br>- Use Azure Firewall Premium TLS Inspection<br>- Restrict egress to approved destinations</p>                                                                       | <p>- Defender for Endpoint: VPN/proxy software activity<br>- Firewall logs: encrypted unknown protocols to untrusted IPs</p>        | <p>- Block destination in NSG/firewall<br>- Deprovision offending app or function<br>- Initiate containment and IR actions</p> |
| <p><strong>T1078</strong><br>Valid Accounts</p>                                   | Exfil using compromised legitimate accounts with storage access                                 | <p>- Enforce MFA &#x26; PIM<br>- Disable unused accounts<br>- Audit token issuance and access logs</p>                                                                                                  | <p>- Sentinel: suspicious login patterns (geo, device)<br>- Audit logs: abnormal blob/file access</p>                               | <p>- Revoke session tokens<br>- Reset passwords<br>- Review downstream data exposure</p>                                       |
| <p><strong>T1552</strong><br>Unsecured Credentials</p>                            | Attackers find credentials or keys enabling exfil                                               | <p>- Remove hardcoded creds from repos/pipelines<br>- Use Managed Identity for auth<br>- Apply scanning tools (Defender for DevOps)</p>                                                                 | <p>- Sentinel alert: secrets found in code<br>- Defender for Key Vault alerts on enumeration</p>                                    | <p>- Revoke exposed creds<br>- Rotate secrets<br>- Conduct credential hygiene review</p>                                       |

