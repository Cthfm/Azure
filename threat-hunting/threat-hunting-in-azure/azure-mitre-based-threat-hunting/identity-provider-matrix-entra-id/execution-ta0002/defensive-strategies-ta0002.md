# Defensive Strategies: TA0002

### **Defensive Strategies for TA0002 - Execution**

The Execution phase involves attackers running malicious code within a compromised environment to carry out their objectives, such as privilege escalation, lateral movement, or exfiltration. In Azure, attackers may abuse scripting tools, automation accounts, APIs, and remote commands to execute malicious actions. Below are key defensive strategies for TA0002 mapped to relevant techniques.

### **1. Limit Scripting and Shell Access**

**Mitigates:** T1059 - Command and Scripting Interpreter (PowerShell, Unix Shell, Python)

* **Action:** Restrict the use of **PowerShell, Bash, and other scripting tools** to reduce the attack surface.
* **Azure Solution:**
  * **Disable PowerShell remoting** unless explicitly required.
  * Use **AppLocker** or **Windows Defender Application Control** to block unauthorized scripts.
  * Monitor PowerShell and shell activities with **Azure Sentinel** and **Defender for Cloud**.

### **2. Monitor and Secure Automation Accounts**

**Mitigates:** T1569.002 - Service Execution, T1574.007 - Service Hijacking

* **Action:** Ensure that **Automation Runbooks** and tasks are not modified to run malicious scripts.
* **Azure Solution:**
  * Use **Azure Monitor** to track changes to automation accounts and **runbooks**.
  * Set alerts in **Azure Sentinel** for any unauthorized execution of automation tasks.
  * Apply **least privilege** principles to automation accounts to limit the impact of abuse.

### **3. Control Remote Command Execution**

**Mitigates:** T1569 - System Services, T1546 - Event Triggered Execution

* **Action:** Monitor and restrict remote command execution on VMs using **VM RunCommand**.
* **Azure Solution:**
  * **Disable VM RunCommand** if not required, or restrict access using **RBAC**.
  * Enable **Azure Defender for VMs** to detect suspicious script executions on virtual machines.
  * Use **just-in-time (JIT) VM access** to limit remote command execution windows.

### **4. Monitor API Calls for Execution Activities**

**Mitigates:** T1106 - Native API

* **Action:** Track **API calls** that can create resources or trigger automation.
* **Azure Solution:**
  * Enable **Azure Monitor** and **Azure Sentinel** to track suspicious API calls, such as role assignments or VM creation.
  * Use **activity logs** to detect unusual API activity patterns and respond to incidents.

### **5. Detect Malicious User-Initiated Actions**

**Mitigates:** T1204 - User Execution (Malicious Link, Malicious File)

* **Action:** Monitor for **social engineering attacks** targeting users with malicious links or files.
* **Azure Solution:**
  * Use **Microsoft Defender for Office 365** to block phishing attempts and malicious attachments.
  * Configure **Azure AD Conditional Access Policies** to limit risky user behavior.
  * Enable **audit logging** to detect malicious file executions and access attempts.

### **6. Disable or Restrict Sudo Access on Linux VMs**

**Mitigates:** T1548 - Abuse Elevation Control Mechanism

* **Action:** Limit **sudo privileges** on Linux VMs to prevent abuse.
* **Azure Solution:**
  * Enforce **key-based authentication** and disable password-based logins.
  * Use **Azure Defender** to monitor for unauthorized privilege escalation attempts.

### **7. Use Conditional Access Policies to Limit Execution Risk**

**Mitigates:** T1078 - Valid Accounts

* **Action:** Use **Conditional Access Policies** to restrict account usage based on context (e.g., IP, device compliance).
* **Azure Solution:**
  * Block risky sign-ins and apply **MFA** requirements for privileged users.
  * Use **Azure Identity Protection** to detect suspicious logins and mitigate compromised accounts.

### **8. Implement Application Whitelisting and Endpoint Protection**

**Mitigates:** T1218 - Signed Binary Proxy Execution

* **Action:** Restrict the execution of **legitimate but potentially abused binaries**, such as MSBuild.
* **Azure Solution:**
  * Use **Microsoft Defender for Endpoint** to monitor and block the execution of unauthorized processes.
  * Implement **AppLocker** policies to restrict the use of binaries like `MSBuild.exe`.

### **9. Harden VMs Against Reverse Shells and Backdoors**

**Mitigates:** T1059.004 - Unix Shell

* **Action:** Monitor Linux VMs for **reverse shells or malicious cron jobs**.
* **Azure Solution:**
  * Use **Azure Defender for Linux VMs** to detect and block threats including web shells.
  * Set up alerts for modifications to **cron jobs** and `.bashrc` files.

### **10. Respond to Execution Attempts Automatically**

**Mitigates:** T1569 - System Services, T1106 - Native API

* **Action:** Automate responses to **suspicious execution activities**.
* **Azure Solution:**
  * Use **Azure Sentinel** playbooks to disable accounts or stop VMs upon detecting suspicious activity.
  * Integrate **Microsoft Defender for Cloud** with **Sentinel** to respond to execution alerts in real-time.

### **Summary of Defensive Measures for TA0002**

| **Defensive Strategy**                | **Mitigates**                             | **Azure Solution**                                           |
| ------------------------------------- | ----------------------------------------- | ------------------------------------------------------------ |
| Limit Scripting and Shell Access      | T1059 - Command and Scripting Interpreter | Block unauthorized scripts with AppLocker and monitoring     |
| Secure Automation Tools               | T1569.002 - Service Execution             | Monitor runbooks with Azure Monitor and Sentinel             |
| Control Remote Execution              | T1569 - System Services                   | Use JIT VM access and restrict RunCommand usage              |
| Monitor API Calls                     | T1106 - Native API                        | Use Azure Sentinel to detect suspicious API activity         |
| Detect User-Initiated Execution       | T1204 - User Execution                    | Use Defender for O365 to block malicious links and files     |
| Restrict Sudo and Privileges          | T1548 - Abuse Elevation Control Mechanism | Monitor sudo usage with Azure Defender                       |
| Apply Conditional Access Policies     | T1078 - Valid Accounts                    | Enforce MFA and apply risk-based conditional access policies |
| Implement App Whitelisting            | T1218 - Signed Binary Proxy Execution     | Use AppLocker to block unauthorized binaries                 |
| Harden VMs Against Reverse Shells     | T1059.004 - Unix Shell                    | Monitor for cron jobs and reverse shells with Defender       |
| Automate Response to Execution Events | T1569 - System Services                   | Use Sentinel playbooks for automated response                |
