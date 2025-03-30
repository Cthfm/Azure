---
hidden: true
---

# Exfiltration TA0010

### Overview:

This phase involves attackers attempting to steal sensitive data from a target environment, such as credentials, personally identifiable information (PII), intellectual property, or configuration settings.

In Microsoft Azure, exfiltration tactics are particularly relevant due to the cloud's inherent remote accessibility, shared responsibility model, and the increasing reliance on services such as Entra ID, Azure Storage, and Key Vault.



### **1️⃣ Exfiltration Over Alternative Protocol (T1048)**

#### **What is it?**

Instead of using standard data transfer methods (like HTTP/HTTPS or SMB), attackers use **alternative network protocols** to bypass security controls. This can include:

* **DNS tunneling**
* **ICMP exfiltration**
* **Custom encrypted protocols (VPNs, TOR, etc.)**
* **Email or messaging services**

#### **Azure-Specific Attack Scenarios**

**🔹 Scenario 1: DNS Tunneling via Azure Functions**

* An attacker gains access to an **Azure VM** or **container** and **does not want to trigger standard HTTP-based logging**.
* They use a tool like **Iodine** or **dnscat2** to encode stolen data inside **DNS queries**.
* The Azure VM makes **repeated DNS requests** to an attacker-controlled domain (e.g., `exfil.attacker.com`).
* Each query sends a **small chunk of base64-encoded data** (e.g., API keys, passwords).

🔍 **Detection & Mitigation:**

* Enable **Azure Sentinel** with **DNS Analytics** to detect unusual **high-frequency DNS requests** to **non-standard domains**.
* Use **Microsoft Defender for DNS** to detect tunneling activity.
* Restrict **outbound DNS requests** using **Azure Firewall DNS Proxy**.

**🔹 Scenario 2: ICMP Exfiltration via Azure VM**

* The attacker installs a tool like **Ptunnel** or **ICMPExfil** on a compromised **Azure Virtual Machine**.
* Instead of using TCP/UDP, data is **embedded in ICMP echo request packets** (ping traffic).
* The data reaches an attacker-controlled server running a listening ICMP-based exfiltration service.

🔍 **Detection & Mitigation:**

* Block **outbound ICMP** on Azure **NSGs (Network Security Groups)**.
* Use **Azure Network Watcher Flow Logs** to analyze anomalous **ICMP traffic spikes**.
* Monitor **unusual ICMP packet sizes** in **Azure Sentinel** (standard ping packets should be small).

***

### **2️⃣ Transfer Data to Cloud Account**

#### **What is it?**

Attackers **move stolen data from a compromised Azure environment** to a **separate cloud storage account** under their control (e.g., an attacker’s **AWS S3, Google Drive, or another Azure Storage account**).

#### **Azure-Specific Attack Scenarios**

**🔹 Scenario 1: Abusing SAS Tokens for Exfiltration**

* A **compromised service principal** or **Azure function** retrieves a **Storage Account SAS token**.
* The attacker uses the **SAS token** to read & exfiltrate sensitive files from **Azure Blob Storage**.
* The data is copied to an **external cloud account** (like AWS S3 or another Azure tenant).

🔍 **Detection & Mitigation:**

* **Disable SAS tokens where possible** & enforce **Azure RBAC** for storage access.
* Monitor **Azure Activity Logs** for **SAS token generation and usage**.
* Use **Defender for Cloud** to detect **cross-tenant data transfers**.

**🔹 Scenario 2: Exfiltrating via Azure Logic Apps**

* An attacker gains **access to a compromised account** with permissions on **Azure Logic Apps**.
* They create an **automated workflow** that **copies** sensitive data from **Azure Blob Storage** to **Google Drive, Dropbox, or another Azure tenant**.
* The **exfiltration happens as an automated scheduled task**, reducing suspicion.

🔍 **Detection & Mitigation:**

* Restrict **Azure Logic Apps permissions** to essential users only.
* Use **Microsoft Defender for Cloud Apps** to detect **unusual external storage uploads**.
* Implement **Azure Monitor Alerts** for **large data movements** or **unusual API calls**.

***

#### **Final Recommendations for Protecting Azure from Exfiltration**

✅ **Enable Microsoft Defender for Cloud** – Detects **abnormal data transfers** & **alerts on anomalous storage access**.\
✅ **Use Conditional Access & MFA** – Prevents **stolen credentials** from being misused.\
✅ **Monitor Azure Storage Logs & Flow Logs** – Helps **detect unusual outbound transfers**.\
✅ **Block DNS tunneling & ICMP exfiltration** – Restrict **unnecessary outbound connections** via **NSGs**.\
✅ **Disable SAS tokens when not needed** – Enforce **Azure AD authentication** instead.

