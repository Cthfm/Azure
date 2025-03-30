# Defensive Strategies

## **Defensive Strategies for Lateral Movement in Azure**

Each technique has prevention, detection, and response strategies.

### **T1021 – Remote Services**

#### **1️⃣ Cloud Services (T1021.006)**

✅ **Least Privilege Access**

* Restrict Azure Bastion and Jumpbox access using role-based access control (RBAC).
* Assign only necessary roles like Virtual Machine User Login to specific accounts.

✅ **Enforce Just-In-Time (JIT) Access**

* Use Microsoft Defender for Cloud’s JIT VM Access to limit remote access duration.
* Require MFA and justification for accessing Bastion.

✅ **Disable Public IPs for VMs**

* Remove public IPs and force access through Bastion, VPN, or Private Link.

✅ **Conditional Access for Remote Logins**

* Create a Conditional Access policy requiring MFA for remote access.
* Block access from high-risk or unknown locations.

#### **2️⃣ Direct Cloud VM Connections (T1021.008)**

✅ **Disable RDP/SSH on Public IPs**

* Require Azure Bastion or VPN instead.

✅ **Restrict Administrative Access**

* Remove the Virtual Machine Administrator Login role from general users.

✅ **Enable Network Security Groups (NSGs)**

* Block TCP 3389 (RDP) and TCP 22 (SSH) from untrusted IPs.

✅ **Require Just-In-Time (JIT) Access**

* Limit RDP/SSH access using JIT VM Access.

### **T1550 – Use Alternate Authentication Material**

#### **1️⃣ Application Access Token (T1550.001)**

✅ **Restrict Managed Identity Permissions**

* Use Azure Entra ID Privileged Identity Management (PIM) to grant temporary access.

✅ **Limit Token Lifespan**

* Configure short-lived OAuth tokens and enforce token expiration policies.

✅ **Use Conditional Access for Token Requests**

* Block token issuance from untrusted locations.

✅ **Enable Defender for Cloud App Discovery**

* Detect applications requesting excessive OAuth tokens.

#### **2️⃣ Web Session Cookie (T1550.004)**

✅ **Enable Continuous Access Evaluation (CAE)**

* Automatically revoke stolen session cookies if the IP or device changes.

✅ **Force Reauthentication for Critical Apps**

* Set Conditional Access policies to require MFA for sensitive applications.

✅ **Prevent Session Hijacking**

* Block legacy authentication to prevent cookie theft.
* Require device compliance checks before granting access.

✅ **Enable Defender for Cloud Apps**

* Detect suspicious session replay attacks.

## **📌 Summary Table of Defensive Strategies**

| MITRE Technique                        | Prevention                                                    | Detection                                                 | Response                                            |
| -------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **T1021.006 Cloud Services**           | Enforce JIT Access, Remove Public IPs, Use Conditional Access | Monitor Azure Bastion logs, Track failed logins           | Block attacker IPs, Invalidate user sessions        |
| **T1021.008 Direct VM Connections**    | Disable RDP/SSH, Use NSGs, Require JIT                        | Detect brute-force logins, Analyze NSG Flow Logs          | Investigate VM logs, Reset credentials              |
| **T1550.001 Application Access Token** | Restrict Managed Identities, Use Conditional Access           | Monitor OAuth token grants, Track Azure Entra ID Sign-Ins | Revoke OAuth tokens, Disable compromised identities |
| **T1550.004 Web Session Cookie**       | Enable CAE, Block legacy auth, Force reauth for critical apps | Detect session reuse, Track Defender for Cloud alerts     | Terminate sessions, Enforce password resets         |
