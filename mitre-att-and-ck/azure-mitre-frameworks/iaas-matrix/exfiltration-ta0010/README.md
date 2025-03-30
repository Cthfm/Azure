# Exfiltration TA0010

## Overview:

This phase involves attackers attempting to steal sensitive data from a target environment, such as credentials, personally identifiable information (PII), intellectual property, or configuration settings.

In Microsoft Azure, exfiltration tactics are particularly relevant due to the cloud's inherent remote accessibility, shared responsibility model, and the increasing reliance on services such as Entra ID, Azure Storage, and Key Vault.

### **1️⃣ Exfiltration Over Alternative Protocol (T1048)**

#### **What is it?**

Instead of using standard data transfer methods (like HTTP/HTTPS or SMB), attackers use alternative network protocols to bypass security controls. This can include:

* DNS tunneling
* ICMP exfiltration
* Custom encrypted protocols (VPNs, TOR, etc.)
* Email or messaging services

#### **Azure-Specific Attack Scenarios**

**1️⃣ DNS Tunneling via Azure Functions**

* An attacker gains access to an Azure VM or container and does not want to trigger standard HTTP-based logging.
* They use a tool like Iodine or dnscat2 to encode stolen data inside DNS queries.
* The Azure VM makes repeated DNS requests to an attacker-controlled domain (e.g., `exfil.attacker.com`).
* Each query sends a small chunk of base64-encoded data (e.g., API keys, passwords).

**2️⃣ ICMP Exfiltration via Azure VM**

* The attacker installs a tool like Ptunnel or ICMPExfil on a compromised Azure Virtual Machine.
* Instead of using TCP/UDP, data is embedded in ICMP echo request packets (ping traffic).
* The data reaches an attacker-controlled server running a listening ICMP-based exfiltration service.

### **2️⃣ Transfer Data to Cloud Account**

Attackers move stolen data from a compromised Azure environment to a separate cloud storage account under their control (e.g., an attacker’s AWS S3, Google Drive, or another Azure Storage account).

#### **Attack Examples:**

**1️⃣ Abusing SAS Tokens for Exfiltration**

* A compromised service principal or Azure function retrieves a Storage Account SAS token.
* The attacker uses the SAS token to read & exfiltrate sensitive files from Azure Blob Storage.
* The data is copied to an external cloud account (like AWS S3 or another Azure tenant).

**2️⃣ Exfiltrating via Azure Logic Apps**

* An attacker gains access to a compromised account with permissions on Azure Logic Apps.
* They create an automated workflow that copies sensitive data from Azure Blob Storage to Google Drive, Dropbox, or another Azure tenant.
* The exfiltration happens as an automated scheduled task, reducing suspicion.



#### **Exfiltration Defense Matrix – Azure Focus (TA0010)**

<table><thead><tr><th>MITRE Technique</th><th>Description</th><th>Prevention</th><th width="152">Detection</th><th>Response</th></tr></thead><tbody><tr><td><strong>T1537</strong><br>Transfer Data to Cloud Account</td><td>Use of authorized or unauthorized cloud apps (Dropbox, Google Drive, AWS S3) to exfiltrate data</td><td>- Use MCAS (Microsoft Defender for Cloud Apps) to block unauthorized cloud services<br>- Implement Conditional Access with app restrictions<br>- Disable browser upload from sensitive resources</td><td>- MCAS alerts on third-party app usage<br>- Azure Sentinel: App connections from risky locations/devices</td><td>- Block access to unsanctioned apps<br>- Revoke session tokens<br>- Review audit logs and re-evaluate RBAC roles</td></tr><tr><td><strong>T1567.002</strong><br>Exfiltration Over Web Service: Cloud Storage</td><td>Use of Azure Blob/File Storage (or external) for staging and exfil</td><td>- Enforce Private Endpoints on Azure Storage<br>- Disable public access<br>- Rotate and restrict SAS/token usage<br>- Apply DLP rules on sensitive files</td><td>- Azure Storage logs: unusual SAS usage, anonymous access<br>- Defender for Storage alerts on mass downloads or IP anomalies</td><td>- Revoke SAS tokens<br>- Block source IPs<br>- Rotate storage keys<br>- Investigate download origin and scope</td></tr><tr><td><strong>T1048.003</strong><br>Exfiltration Over Alternative Protocol: DNS</td><td>Covert exfil using DNS tunneling (e.g., iodine, dnscat2)</td><td>- Block unknown domains using Defender for DNS<br>- Use deny-by-default outbound DNS egress rules<br>- DNS sinkholing for known C2</td><td>- Defender for DNS: anomalous FQDN volume or entropy<br>- Azure Firewall logs: frequent TXT record queries</td><td>- Alert and isolate compromised host<br>- Block domain/IP<br>- Perform forensic packet analysis</td></tr><tr><td><strong>T1048.002</strong><br>Exfiltration Over Alternative Protocol: ICMP</td><td>Exfiltration via ICMP tunnels (e.g., Ptunnel)</td><td>- Block ICMP outbound traffic in NSGs<br>- Use Azure Firewall to deny non-essential ICMP</td><td>- Flow logs: high-volume ICMP<br>- Defender for Endpoint: tunneling tools on host</td><td>- Disable NSG rules<br>- Quarantine VM<br>- Deep-dive host telemetry for tunnel activity</td></tr><tr><td><strong>T1048.001</strong><br>Exfiltration Over Custom Protocol</td><td>Use of TOR, VPN, or custom TCP/UDP channels to evade detection</td><td>- Block TOR/VPN ports in NSGs<br>- Use Azure Firewall Premium TLS Inspection<br>- Restrict egress to approved destinations</td><td>- Defender for Endpoint: VPN/proxy software activity<br>- Firewall logs: encrypted unknown protocols to untrusted IPs</td><td>- Block destination in NSG/firewall<br>- Deprovision offending app or function<br>- Initiate containment and IR actions</td></tr><tr><td><strong>T1078</strong><br>Valid Accounts</td><td>Exfil using compromised legitimate accounts with storage access</td><td>- Enforce MFA &#x26; PIM<br>- Disable unused accounts<br>- Audit token issuance and access logs</td><td>- Sentinel: suspicious login patterns (geo, device)<br>- Audit logs: abnormal blob/file access</td><td>- Revoke session tokens<br>- Reset passwords<br>- Review downstream data exposure</td></tr><tr><td><strong>T1552</strong><br>Unsecured Credentials</td><td>Attackers find credentials or keys enabling exfil</td><td>- Remove hardcoded creds from repos/pipelines<br>- Use Managed Identity for auth<br>- Apply scanning tools (Defender for DevOps)</td><td>- Sentinel alert: secrets found in code<br>- Defender for Key Vault alerts on enumeration</td><td>- Revoke exposed creds<br>- Rotate secrets<br>- Conduct credential hygiene review</td></tr></tbody></table>



