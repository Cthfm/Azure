# SysInternals

## **Overview**

**Sysinternals** is a collection of powerful, lightweight utilities developed by **Mark Russinovich** (now part of Microsoft). These tools are a staple in both **IT operations and cybersecurity** due to their ability to give deep visibility into Windows internals. Sysinternals provides insight into **process management, network activity, file access, security configurations, and more**—which makes it valuable for **blue teams, red teams, and penetration testers** alike.

### **Categories and Key Tools in Sysinternals**

#### 1. **Process and System Monitoring Tools**

These utilities help monitor **processes, threads, memory, and system resource usage**.

* **Process Explorer (procexp)**:
  * **Alternative to Task Manager**, showing a detailed view of running processes, DLLs, and handles.
  * It’s used to inspect processes for malicious activity and **detect rootkits** by revealing hidden processes.
  * **Usage Example**:
    *   Track a suspicious process:

        ```plaintext
        procexp.exe
        ```
    * Use it to identify **parent-child relationships** and loaded modules in each process.
* **Procmon (Process Monitor)**:
  * Captures **real-time logs** of file system, registry, and process/thread activity.
  * Essential for **debugging malware behavior** or finding how an attacker gains persistence via the registry.
  *   **Filter example**: Track modifications to `HKCU\Software`:

      ```plaintext
      procmon.exe
      ```

      Set a filter: `Path → Contains → HKCU\Software`

### 2. **Networking Tools**

Monitor and troubleshoot **network connections and ports**. These are useful for **identifying backdoors, reverse shells, or rogue services**.

* **TCPView**:
  * Displays **open network connections** in real-time, including local and remote IP addresses.
  *   Helps detect unusual outbound connections (e.g., malware calling home).

      ```plaintext
      plaintextCopy codetcpview.exe
      ```
  * Look for processes making suspicious **outbound connections** to IPs not normally accessed.
* **PsPing**:
  *   Tests **network connectivity and performance**, offering more features than `ping` or `tracert`.

      ```bash
      bashCopy codepsping.exe 192.168.1.1:443
      ```
  * **Uses**: Check latency, bandwidth, and open ports during internal recon.

### 3. **File and Disk Utilities**

Tools in this category inspect **file usage, disk performance, and access permissions**.

* **AccessChk**:
  *   Shows **user permissions** on files, directories, and registry keys, helping detect **misconfigurations** that could allow privilege escalation.

      ```bash
      accesschk.exe -w -s c:\sensitive-folder
      ```
  * **Use case**: Identify which services or folders have **write access** for unauthorized users.
* **Autoruns**:
  * Displays all **startup programs and services**, including registry keys and scheduled tasks.
  *   **Used for persistence detection**: Find hidden backdoors or services an attacker planted.

      ```plaintext
      autoruns.exe
      ```

### 4. **Remote Management Tools**

Tools for **remote administration and lateral movement**, widely used by attackers but equally important for defenders.

* **PsExec**:
  * Allows **remote command execution** on other Windows systems.
  *   Commonly used by attackers for **lateral movement** after credential compromise.

      ```bash
      psexec \\target -u admin -p password cmd.exe
      ```
  * **Use case**: Red teams use PsExec to move between machines, while blue teams monitor for suspicious remote executions.
* **PsList / PsKill**:
  *   **PsList** shows detailed process information for remote or local systems:

      ```bash
      pslist \\target
      ```
  *   **PsKill** can terminate processes on local or remote machines:

      ```bash
      pskill \\target notepad.exe
      ```

### 5. **Security and Forensics Tools**

These utilities help **analyze user activity**, track access to sensitive areas, and **uncover malicious behavior**.

* **SigCheck**:
  *   Verifies **digital signatures** of files to detect tampered or untrusted executables.

      ```bash
      sigcheck.exe -e c:\windows\system32\*.exe
      ```
  * **Use case**: Detect if attackers have replaced legitimate Windows files with malicious ones.
* **Strings**:
  *   Extracts **readable strings** from binary files, often used to analyze malware and find hardcoded IPs, URLs, or other clues.

      ```bash
      strings.exe malware.bin
      ```

### 6. **User and Logon Management Tools**

Used to **monitor user sessions, detect unauthorized access, and handle credentials**.

* **LogonSessions**:
  *   Displays all **active user sessions** along with their logon time.

      ```bash
      logonsessions.exe
      ```
  * **Use case**: Detect unauthorized logins or compromised accounts with suspicious session activity.
* **PsLoggedOn**:
  *   Identifies **which users are currently logged in** to local or remote systems.

      ```bash
      psloggedon \\target
      ```
