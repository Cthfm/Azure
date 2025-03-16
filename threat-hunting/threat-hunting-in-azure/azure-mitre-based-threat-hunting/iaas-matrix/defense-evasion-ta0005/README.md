# Defense Evasion TA0005

## **Overview:**

In Azure, attackers use Defense Evasion (TA0005) techniques to bypass security controls, avoid detection, and maintain persistence within a compromised environment. Let's look at the different techniques and sub techniques of Defense Evasion (TA0005)

### **Abuse Elevation Control Mechanism (T1548)**

This technique refers to techniques where attackers exploit privilege escalation features to gain higher permissions within a system or cloud environment.

**Temporary Elevated Cloud Access (T1548.005)**

* **Example:** An attacker gains access to an Azure account with low privileges and leverages Azure Privileged Identity Management (PIM) to elevate their access temporarily to a Global Admin role. They then perform actions before their access is revoked.

### **Exploitation for Defense Evasion (**&#x54;1211)

Exploitation for Defense Evasion occurs when attackers leverage vulnerabilities in security tools or cloud services to bypass detection, disable monitoring, or escalate privileges without triggering alerts.

* **Example:** ChaosDB (2021) exploited improper Jupyter Notebook permissions in Azure CosmosDB, allowing attackers to steal database primary keys and access other tenants’ data—breaking multi-tenant security boundaries.

### **Impair Defenses (T1562)**

Impair Defenses refers to techniques where attackers disable, modify, or evade security tools to avoid detection and maintain persistence.&#x20;

**Disable or Modify Tools (T1562.001)**

* **Example:** An attacker disables Microsoft Defender for Endpoint in Azure Security Center via PowerShell (`Set-MpPreference -DisableRealtimeMonitoring $true`) to evade detection.

**Disable or Modify Cloud Firewall (T1562.007)**

* **Example:** An attacker modifies Azure Network Security Group (NSG) rules to allow external traffic to an internal resource, thereby bypassing firewall restrictions.

**Disable or Modify Cloud Logs (T1562.008)**

*   **Example:** Using Azure CLI, an attacker disables diagnostic logging for Azure Key Vault or other resources to prevent activity tracking:

    ```powershell
    az monitor diagnostic-settings delete --name "LogProfileName" --resource-group "ResourceGroupName"
    ```

### **Modify Authentication Process (T1556)**

A technique where adversaries manipulate authentication mechanisms to bypass security controls, escalate privileges, or maintain persistence. By altering how authentication works, attackers can steal credentials, create backdoor access, or evade detection.

**Multi-Factor Authentication (MFA) Bypass (T1556.006)**

* **Example:** An attacker uses phishing to steal an Azure Entra ID admin’s session token and logs in without triggering MFA verification.

**Hybrid Identity Manipulation (T1556.007)**

* **Example:** An attacker gains access to on-premises Active Directory Federation Services (AD FS) and modifies claims rules to grant themselves elevated Azure AD permissions.

**Conditional Access Policy Manipulation (T1556.009)**

* **Example:** An attacker with admin access modifies Azure Conditional Access policies to remove MFA requirements for specific locations or IPs.

#### **Modify Cloud Compute Infrastructure (T1578)**

Refers to adversaries modifying cloud compute resources to gain persistence, escalate privileges, or disrupt services. This is a key tactic in cloud-focused red teaming, where attackers exploit misconfigurations, stolen credentials, or vulnerabilities to manipulate cloud infrastructure.

**Create Snapshot (T1578.001)**

*   **Example:** An attacker creates a snapshot of a critical Azure VM's disk to exfiltrate sensitive data:

    ```
    az snapshot create --resource-group MyResourceGroup --source MyOSDisk --name MySnapshot
    ```

**Create Cloud Instance (T1578.002)**

* **Example:** An attacker creates a new Azure VM in a different region to establish persistence and avoid detection.

**Delete Cloud Instance (T1578.003)**

*   **Example:** After exfiltrating data, an attacker deletes audit-related VM instances:

    ```powershell
    az vm delete --resource-group MyResourceGroup --name AuditVM --yes
    ```

**Revert Cloud Instance (T1578.004)**

* **Example:** An attacker restores an Azure VM from an older snapshot to erase security patches.

**Modify Cloud Compute Configurations (T1578.005)**

* **Example:** An attacker alters an Azure VM’s diagnostic settings to stop security monitoring.

#### **Modify Cloud Resource Hierarchy (**&#x54;1666)

Attackers manipulate cloud structures to avoid detection and maintain persistence.&#x20;

* **Example:** An attacker with elevated privileges may create new subscriptions and deploy new resources. They can move subscriptions from a victim tenant to an attacker-controlled tenant.

#### **Unused/Unsupported Cloud Regions (T1535)**

Attackers use regions that are not actively monitored or utilized within an environment to evade detection.

* **Example:** An attacker deploys resources in an Azure region not actively monitored by security teams to evade detection.

#### **Use Alternate Authentication Material (T1550)**

Attackers bypass traditional authentication mechanisms and avoid detection. Instead of using stolen passwords, adversaries leverage authentication mechanisms to authenticate without triggering login failure alerts or multi-factor authentication (MFA) challenges.

**Application Access Token (T1550.001)**

* **Example:** An attacker extracts an Azure Entra OAuth token from a compromised user's machine and uses it to authenticate API requests.

**Web Session Cookie (T1550.004)**

* **Example:** An attacker steals an authenticated Azure session cookie using a myriad of ways such as a "pass-the-cookie" attack.

#### **Valid Accounts (T1078)**

Attackers leverage legitimate credentials to blend in with normal user activity, avoiding detection. Instead of exploiting vulnerabilities, they use stolen, default, or misconfigured accounts to access systems without triggering security alerts. This includes compromised user accounts, service accounts, cloud credentials, or SSH keys, allowing attackers to persist within networks while bypassing traditional security mechanisms like failed login alerts or brute-force protections.

**Default Accounts (T1078.001)**

* **Example:** An attacker exploits an Azure Storage Account configured with a default shared access key to access stored files.

**Cloud Accounts (T1078.004)**

* **Example:** An attacker uses leaked Azure admin credentials from GitHub to log into the Azure portal and modify security configurations.
