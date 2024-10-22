# Sysmon

### **Overview**

**Sysmon (System Monitor)** is a Windows system service and driver from Microsoft’s Sysinternals suite. It provides **detailed logging of system activity**, which goes beyond native Windows auditing capabilities. Sysmon helps in tracking **process creation, network connections, and other system-level activities** for forensic investigations, threat hunting, and incident response.

### **Key Features of Sysmon:**

1. **Process Monitoring:**
   * Logs process creation, including process ID, command line, and hashes.
   * Captures process termination events.
2. **Network Monitoring:**
   * Tracks network connections, including IP addresses, ports, and protocols.
   * Monitors DNS query events for domain lookups.
3. **File and Registry Monitoring:**
   * Detects changes to file creation time (even if altered retroactively).
   * Monitors registry modifications and event access attempts.
4. **Driver and DLL Loading:**
   * Captures details of drivers and DLLs loaded into processes.
5. **Event Forwarding:**
   * Logs are integrated with **Windows Event Log**, making them accessible via tools like **Event Viewer** or SIEM solutions.
6. **Hashing and Data Integrity:**
   * Hashes of processes (MD5, SHA-1, SHA-256) are captured to detect tampered or malicious files.

### **Why Sysmon is Important:**

* **Granular Monitoring:** Sysmon complements basic and advanced auditing by offering **more detailed telemetry**.
* **Threat Detection and Forensics:** It enables **early detection of suspicious activities**, like unusual process launches or unauthorized network connections.
* **Customization with Configuration Files:** Administrators can tune Sysmon’s behavior via XML configuration files to reduce noise and focus on critical events.

### **Deployment and Usage:**

* **Installation:**\
  Download and install Sysmon from the [Sysinternals site](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon). The service runs persistently in the background.
*   **Configuration:**\
    Use **XML configuration files** to define which activities are logged. Example commands:

    ```arduino
    sysmon.exe -accepteula -i config.xml
    ```

    This installs Sysmon with your custom rules.
* **Event Analysis:**\
  Sysmon events appear under **"Microsoft-Windows-Sysmon/Operational"** in Event Viewer, making them easy to collect and analyze.

### **Comparison to Windows Auditing:**

* **Sysmon** offers **more detailed event logging** than native Windows security auditing.
* It captures **more context-rich data**, such as **process command-line arguments and DNS queries**, which are either unavailable or harder to configure in **Advanced Security Auditing**.

### Documentation

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon" %}
