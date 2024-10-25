# Defensive Strategies for TA0005

## **Defensive Strategies for TA0005 - Defense Evasion**

Defending against **Defense Evasion (TA0005)** requires **continuous monitoring, strict access controls, auditing of logs, and detection of obfuscation techniques**. Attackers aim to disable security controls, manipulate authentication processes, delete logs, or use trusted tools to stay hidden. Below are key **defensive strategies** mapped to relevant techniques, with **Azure-specific solutions** to mitigate evasion attempts.

### **1. Monitor and Enforce Security Controls**

**Mitigates:** T1562 - Impair Defenses

* **Action:** Continuously monitor the **status of security tools and alerts** to ensure they remain enabled.
* **Azure Solution:**
  * Use **Azure Policy** to enforce that **Azure Defender** remains enabled across all resources.
  * Set **Azure Monitor alerts** to notify administrators when **security settings** are modified.
  * Enable **tamper protection** to prevent disabling of Defender agents on VMs.

### **2. Detect Suspicious Authentication Behavior**

**Mitigates:** T1556 - Modify Authentication Process

* **Action:** Monitor for **changes to MFA settings or Conditional Access Policies**.
* **Azure Solution:**
  * Use **Azure AD Identity Protection** to detect MFA bypass attempts.
  * Monitor changes to **Conditional Access Policies** using **Azure Sentinel** and **Audit Logs**.
  * Configure **just-in-time (JIT) access** to limit administrative actions.

### **3. Prevent Misuse of Legitimate Tools**

**Mitigates:** T1218 - Signed Binary Proxy Execution

* **Action:** Restrict the use of **legitimate binaries**, such as MSBuild, that can be used for malicious purposes.
* **Azure Solution:**
  * Use **AppLocker** or **Windows Defender Application Control (WDAC)** to block unauthorized tools.
  * Monitor for execution of **trusted tools** like MSBuild via **Azure Sentinel**.
  * Use **Microsoft Defender for Endpoint** to detect and block misuse of signed binaries.

### **4. Detect and Block Obfuscation Techniques**

**Mitigates:** T1027 - Obfuscated Files or Information

* **Action:** Monitor for **encoded or encrypted payloads**, such as Base64-encoded PowerShell commands.
* **Azure Solution:**
  * Use **Microsoft Defender for Endpoint** to detect **encoded or obfuscated scripts**.
  * Set alerts in **Azure Sentinel** to flag the use of Base64-encoded commands in PowerShell logs.
  * Enable **PowerShell logging** and **Script Block Logging** on VMs.

### **5. Enable Logging and Monitor for Log Tampering**

**Mitigates:** T1070 - Indicator Removal on Host

* **Action:** Ensure **logs cannot be modified or deleted** by attackers.
* **Azure Solution:**
  * Use **Azure Monitor and Activity Logs** to track changes to logging configurations.
  * Enable **Immutable Blob Storage** to prevent log deletions.
  * Use **Azure Sentinel** to detect gaps in logging that may indicate tampering.

### **6. Monitor and Secure Automation Accounts**

**Mitigates:** T1564 - Hide Artifacts

* **Action:** Track changes to **automation tasks and runbooks** to detect hidden malicious tasks.
* **Azure Solution:**
  * Use **Azure Monitor** to detect modifications to Automation Accounts and **runbooks**.
  * Implement **role-based access control (RBAC)** to restrict who can modify automation settings.
  * Regularly review automation logs for unauthorized changes or suspicious jobs.

### **7. Restrict the Use of Remote Services and JIT Access**

**Mitigates:** T1569 - Service Execution

* **Action:** Limit the use of **remote services** like SSH, RDP, and VM RunCommand to prevent hidden execution.
* **Azure Solution:**
  * Use **JIT access** to restrict RDP and SSH access to Azure VMs.
  * Disable **RunCommand** on VMs unless explicitly required.
  * Monitor **Azure Bastion** logs for suspicious access patterns.

### **8. Detect and Respond to Rogue Service Principal Usage**

**Mitigates:** T1098 - Account Manipulation

* **Action:** Monitor for **suspicious activity involving service principals** and automation accounts.
* **Azure Solution:**
  * Use **Azure Sentinel** to detect unauthorized role assignments to service principals.
  * Rotate **service principal keys** regularly using **Azure Key Vault**.
  * Monitor for new credentials being added to service principals.

### **9. Block Legacy Authentication Protocols**

**Mitigates:** T1078.002 - Domain Accounts

* **Action:** Disable **legacy authentication protocols** to prevent attackers from bypassing modern security features.
* **Azure Solution:**
  * Use **Conditional Access Policies** to block protocols like POP, IMAP, and SMTP.
  * Enforce **modern authentication** across all resources.
  * Monitor for login attempts using legacy protocols with **Azure Sentinel**.

### **10. Automate Incident Response with Playbooks**

**Mitigates:** Multiple Techniques

* **Action:** Use **automated playbooks** to respond to defense evasion attempts.
* **Azure Solution:**
  * Use **Azure Sentinel** to trigger automated workflows when suspicious activities are detected (e.g., disabling compromised accounts).
  * Integrate **Microsoft Defender for Cloud** with Sentinel for enhanced incident response.
  * Configure playbooks to block malicious IPs, revoke OAuth tokens, or disable compromised service principals automatically.

### **Summary of Defensive Measures for TA0005**

| **Defensive Strategy**                   | **Mitigates**                           | **Azure Solution**                                         |
| ---------------------------------------- | --------------------------------------- | ---------------------------------------------------------- |
| Monitor and Enforce Security Controls    | T1562 - Impair Defenses                 | Use Azure Policy to enforce Defender settings              |
| Detect Suspicious Authentication Changes | T1556 - Modify Authentication Process   | Monitor MFA and Conditional Access with Azure Sentinel     |
| Block Misuse of Legitimate Tools         | T1218 - Signed Binary Proxy Execution   | Use AppLocker and Defender for Endpoint to block abuse     |
| Detect Obfuscation Techniques            | T1027 - Obfuscated Files or Information | Monitor PowerShell for encoded commands                    |
| Enable Logging and Monitor Tampering     | T1070 - Indicator Removal on Host       | Use Immutable Blob Storage to prevent log deletion         |
| Secure Automation Tasks                  | T1564 - Hide Artifacts                  | Monitor runbooks with Azure Monitor and enforce RBAC       |
| Restrict Remote Services                 | T1569 - Service Execution               | Use JIT access and disable RunCommand if unnecessary       |
| Monitor Service Principal Usage          | T1098 - Account Manipulation            | Use Sentinel to track suspicious role assignments          |
| Block Legacy Authentication Protocols    | T1078.002 - Domain Accounts             | Enforce modern authentication and block legacy protocols   |
| Automate Incident Response               | Multiple Techniques                     | Use Azure Sentinel playbooks for automated threat response |
