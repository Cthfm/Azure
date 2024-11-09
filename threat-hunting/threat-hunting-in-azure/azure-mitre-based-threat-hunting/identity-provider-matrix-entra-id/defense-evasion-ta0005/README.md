---
hidden: true
---

# Defense Evasion: TA0005

### Overview

The Defense Evasion tactic focuses on hiding malicious activities to avoid detection by security tools and analysts. In Azure environments, attackers use a variety of techniques, such as disabling logging, bypassing multi-factor authentication, manipulating policies, and abusing trusted tools to stay under the radar. Below are the key concepts with associated techniques, sub-techniques, and Azure-specific examples

### **1. Disabling or Modifying Security Controls**

**Technique:** T1562 - Impair Defenses\
Attackers **disable logging, security alerts, or monitoring tools** to avoid detection.

*   **T1562.001 - Disable or Modify Tools**\
    **Azure Example:** Disable **Azure Defender** alerts to evade monitoring.

    ```bash
    az security pricing create --name VirtualMachines --tier 'Free'
    ```
*   **T1562.004 - Disable Event Logging**\
    **Azure Example:** Use **PowerShell** to stop or clear Azure AD audit logs.

    ```powershell
    Stop-Service -Name "AzureADConnect"  
    ```

### **2. Bypassing Authentication or Conditional Access**

**Technique:** T1556 - Modify Authentication Process\
Attackers **alter or bypass authentication flows**, such as MFA, to gain persistent access.

*   **T1556.004 - Add MFA Bypass Rule**\
    **Azure Example:** Modify **conditional access policies** to exclude specific IPs from MFA requirements.

    ```powershell
    Set-AzureADPolicy -Id <PolicyID> -Definition "{... MFA Exclusion Config...}"
    ```

### **3. Exploiting Trusted Tools for Evasion**

**Technique:** T1218 - Signed Binary Proxy Execution\
Attackers use **legitimate signed tools** to execute malicious commands, bypassing security.

*   **Azure Example:** Use **MSBuild.exe** on a Windows VM to launch payloads while avoiding security alerts.

    ```xml
    xmlCopy code<Project>
      <Target Name="RunPayload">
        <Exec Command="cmd.exe /c calc.exe" />
      </Target>
    </Project>
    ```

### **4. Obfuscating Command Execution**

**Technique:** T1055 - Process Injection\
Attackers hide malicious code within legitimate processes to evade detection.

* **Azure Example:** Inject malicious code into a **PowerShell process** running on a compromised Azure VM to blend into normal operations.

### **5. Deleting or Modifying Logs to Cover Tracks**

**Technique:** T1070 - Indicator Removal on Host\
Attackers remove logs and other traces to **prevent forensic investigations**.

* **T1070.004 - File Deletion**\
  **Azure Example:** Delete **Azure Activity Logs** that contain evidence of privilege escalation.

### **6. Abusing Policies and Configuration Settings for Evasion**

**Technique:** T1564 - Hide Artifacts\
Attackers **manipulate policies or settings** to hide their activities or artifacts.

* **T1564.003 - Hidden Window**\
  **Azure Example:** Run malicious code in the background using **hidden processes** within Automation Accounts to avoid user detection.

### **7. Exploiting Trusted Relationships to Evade Monitoring**

**Technique:** T1199 - Trusted Relationship\
Attackers abuse **multi-tenant or federated relationships** to avoid detection.

* **Azure Example:** Use a trusted tenant's permissions to access sensitive resources without triggering alerts in the victim’s environment.

### **8. Encrypting or Encoding Payloads to Avoid Detection**

**Technique:** T1027 - Obfuscated Files or Information\
Attackers use **encryption or encoding** to make their payloads less detectable by security tools.

*   **Azure Example:** Deliver **Base64-encoded PowerShell scripts** that bypass antivirus scanning.

    ```powershell
    powershell.exe -EncodedCommand <Base64Payload>
    ```

### **9. Disguising Malicious Code as Normal Services or Accounts**

**Technique:** T1036 - Masquerading\
Attackers disguise malicious code or processes as **legitimate services**.

* **T1036.005 - Match Legitimate Name or Location**\
  **Azure Example:** Deploy a malicious automation task named **“Microsoft-Update”** to blend in with legitimate tasks.

### **10. Abusing Service Principals and Automation Accounts for Evasion**

**Technique:** T1098 - Account Manipulation\
Attackers manipulate **service principals** or **automation accounts** to evade detection.

* **Azure Example:** Add extra credentials to a **service principal**, allowing hidden access to resources.

### **Summary of Key Concepts with Techniques for TA0005**

| **Key Concept**               | **Technique**                           | **Azure Example**                                          |
| ----------------------------- | --------------------------------------- | ---------------------------------------------------------- |
| Disable Security Controls     | T1562 - Impair Defenses                 | Disable Azure Defender alerts to evade monitoring          |
| Bypass Authentication         | T1556 - Modify Authentication Process   | Modify conditional access policies to bypass MFA           |
| Use Trusted Tools for Evasion | T1218 - Signed Binary Proxy Execution   | Use MSBuild.exe to execute malicious code undetected       |
| Obfuscate Command Execution   | T1055 - Process Injection               | Inject malicious code into legitimate PowerShell processes |
| Delete or Modify Logs         | T1070 - Indicator Removal on Host       | Delete Azure Activity Logs to cover privilege escalation   |
| Hide Artifacts via Policies   | T1564 - Hide Artifacts                  | Run hidden tasks in Automation Accounts                    |
| Exploit Trusted Relationships | T1199 - Trusted Relationship            | Use tenant trust to access resources without detection     |
| Encode or Encrypt Payloads    | T1027 - Obfuscated Files or Information | Use Base64-encoded scripts to evade antivirus scanning     |
| Masquerade Malicious Code     | T1036 - Masquerading                    | Deploy malicious tasks named after legitimate services     |
| Abuse Service Principals      | T1098 - Account Manipulation            | Add hidden credentials to a service principal              |
