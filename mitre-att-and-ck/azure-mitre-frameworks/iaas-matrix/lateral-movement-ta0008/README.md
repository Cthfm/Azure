# Lateral Movement TA0008

## Overview

Lateral movement in Azure involves adversaries leveraging various techniques to move from one compromised system to another within the cloud environment.&#x20;

### 1️⃣ **T1021 – Remote Services**&#x20;

Adversaries may use legitimate remote services to access and control systems within an Azure environment.

#### 1️⃣ **Cloud Services (T1021.006)**

* **Definition:** Attackers use cloud-based remote services, such as Azure Bastion, Jump Servers, or Azure Arc-enabled servers, to gain remote access to a compromised VM or service.
* **Example in Azure:**
  * An attacker compromises Azure Entra credentials with Virtual Machine Contributor or Virtual Machine Administrator Login permissions.
  * They log in via Azure Bastion or RDP over the public internet using the compromised credentials.
  * The attacker then pivots to other virtual machines or resources within the same virtual network.

#### 2️⃣ **Direct Cloud VM Connections (T1021.008)**

* **Definition:** Adversaries remotely access a VM by connecting directly over RDP, SSH, or custom TCP ports without using Bastion or Jump Servers.
* **Example in Azure:**
  * An attacker exploits a publicly exposed VM with RDP (TCP 3389) or SSH (TCP 22).
  * They brute-force Azure VM login credentials or use previously stolen credentials.
  * Once inside, they execute commands and move laterally to other VMs via Azure Virtual Network Peering or Azure Arc connections.

### 3️⃣**T1550 – Use Alternate Authentication Material**

This technique allows attackers to bypass normal authentication mechanisms using stolen tokens, cookies, or other credentials.

#### 1️⃣ **Application Access Token (T1550.001)**

* **Definition:** Adversaries use OAuth tokens or Azure Managed Identity tokens to access cloud services without needing passwords.
* **Example in Azure:**
  * An attacker steals a managed identity token from a compromised Azure VM or Azure Function App.
  * They use this token to authenticate against Azure Key Vault, Storage Accounts, or other Azure services.
  * The token allows the attacker to extract secrets, sensitive files, or perform privileged operations.

#### 2️⃣ **Web Session Cookie (T1550.004)**

* **Definition:** Attackers steal and reuse authentication cookies to bypass MFA and access Azure services as a legitimate user.
*   **Example in Azure:**

    * An attacker extracts an Azure Entra session cookie from a compromised user's browser.
    * They replay the cookie to gain SSO access to Microsoft 365 (Exchange, SharePoint, etc.).
    * Using the valid session, the attacker downloads sensitive emails, exfiltrates files from OneDrive, or escalates privileges.

