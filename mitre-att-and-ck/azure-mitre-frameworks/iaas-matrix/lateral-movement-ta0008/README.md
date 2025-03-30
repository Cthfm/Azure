---
hidden: true
---

# Lateral Movement TA0008

Overview:

Lateral movement in Azure involves adversaries leveraging various techniques to move from one compromised system to another within the cloud environment. Below, I’ll detail **T1021 (Remote Services)** and **T1550 (Use Alternate Authentication Material)** with **Azure-specific** examples.

***

### 🛠 **T1021 – Remote Services (2)**

Adversaries may use legitimate remote services to **access** and **control** systems within an Azure environment.

#### 1️⃣ **Cloud Services (T1021.006)**

* **Definition:** Attackers use cloud-based remote services, such as Azure Bastion, Jump Servers, or Azure Arc-enabled servers, to gain remote access to a compromised VM or service.
*   **Example in Azure:**

    * An attacker compromises **Azure AD credentials** with **Virtual Machine Contributor** or **Virtual Machine Administrator Login** permissions.
    * They log in via **Azure Bastion** or **RDP over the public internet** using the compromised credentials.
    * The attacker then pivots to other virtual machines or resources within the same virtual network.

    **Detection Strategies:**

    * Monitor **Azure Bastion logs** (`AzureDiagnostics` table) for unusual login patterns.
    * Analyze **Sign-in logs** for anomalies, such as new IP addresses or unusual login times.
    * Use **Microsoft Defender for Cloud** alerts for suspicious RDP activities.

    **Mitigation:**

    * Enforce **Conditional Access policies** to restrict access to Bastion.
    * Use **Just-In-Time (JIT) VM Access** to limit unnecessary remote access.

#### 2️⃣ **Direct Cloud VM Connections (T1021.008)**

* **Definition:** Adversaries remotely access a VM by connecting directly over **RDP, SSH, or custom TCP ports** without using Bastion or Jump Servers.
*   **Example in Azure:**

    * An attacker exploits a **publicly exposed VM** with RDP (TCP 3389) or SSH (TCP 22).
    * They brute-force Azure VM login credentials or use previously stolen credentials.
    * Once inside, they execute commands and move laterally to other VMs via **Azure Virtual Network Peering** or **Azure Arc connections**.

    **Detection Strategies:**

    * Check for successful and failed RDP/SSH authentication attempts in **Azure Activity Logs** and **NSG Flow Logs**.
    * Detect abnormal RDP logins in **AADSignInLogs**.
    * Alert on unexpected use of the **Azure Serial Console**, which provides remote VM access.

    **Mitigation:**

    * Remove all **public IP addresses** from Azure VMs.
    * Implement **Network Security Groups (NSGs)** and **Azure Firewall** to restrict inbound traffic.
    * Require **Azure AD authentication for VM login** instead of local accounts.

***

### 🔹 **T1550 – Use Alternate Authentication Material (2)**

This technique allows attackers to bypass normal authentication mechanisms using stolen **tokens, cookies, or other credentials**.

#### 1️⃣ **Application Access Token (T1550.001)**

* **Definition:** Adversaries use **OAuth tokens** or **Azure Managed Identity tokens** to access cloud services **without needing passwords**.
*   **Example in Azure:**

    * An attacker **steals a managed identity token** from a compromised Azure VM or **Azure Function App**.
    * They use this token to authenticate against **Azure Key Vault, Storage Accounts, or other Azure services**.
    * The token allows the attacker to extract **secrets, sensitive files, or perform privileged operations**.

    **Detection Strategies:**

    * Monitor **Microsoft Graph API calls** (`AuditLogs` table) for unexpected token usage.
    *   Use KQL queries to analyze **Azure AD Token Issuance** for anomalies:

        ```kql
        kqlCopyEditAuditLogs
        | where ActivityDisplayName == "TokenIssued"
        | where InitiatedBy.userPrincipalName != "<expected user>"
        ```
    * Look for API requests to **Microsoft Key Vault** from unexpected sources.

    **Mitigation:**

    * Restrict Managed Identity permissions to **least privilege**.
    * Use **Conditional Access** to prevent risky OAuth token usage.
    * Enable **Defender for Cloud alerts** on suspicious API token activity.

#### 2️⃣ **Web Session Cookie (T1550.004)**

* **Definition:** Attackers steal and reuse authentication cookies to **bypass MFA** and access Azure services as a legitimate user.
*   **Example in Azure:**

    * An attacker **extracts an Azure AD session cookie** from a compromised user's browser.
    * They replay the cookie to gain **SSO access to Microsoft 365 (Exchange, SharePoint, etc.)**.
    * Using the valid session, the attacker **downloads sensitive emails, exfiltrates files from OneDrive, or escalates privileges**.

    **Detection Strategies:**

    * Use **Microsoft Defender for Cloud Apps (MDCAP)** to monitor suspicious session activity.
    * Correlate **Azure AD logs** (`SigninLogs`) with unusual locations or new devices.
    *   Detect suspicious web logins that bypass MFA:

        ```kql
        kqlCopyEditSigninLogs
        | where Status.errorCode == 0
        | where ConditionalAccessStatus == "notApplied"
        ```

    **Mitigation:**

    * **Enforce reauthentication policies** for sensitive applications.
    * Enable **Continuous Access Evaluation (CAE)** to revoke tokens dynamically.
    * Require **device compliance checks** before allowing authentication.
