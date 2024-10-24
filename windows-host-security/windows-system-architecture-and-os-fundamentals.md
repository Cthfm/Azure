# Windows System Architecture and OS Fundamentals

Understanding Windows architecture and OS fundamentals involves knowing the underlying layers that manage processes, memory, hardware, security, and services. Let's break this into sections:

### **Architecture Overview**

Windows OS follows a **layered architecture** with two primary components:

* **User Mode:** Where user applications and some system services operate.
* **Kernel Mode:** Where the core OS components, including device drivers, operate with full system privileges.

#### **High-Level Architecture Diagram:**

1. **User Mode:**
   * User applications (e.g., Chrome, Office)
   * Environment subsystems (e.g., Win32)
   * System processes (e.g., `explorer.exe`, `lsass.exe`)
2. **Kernel Mode:**
   * Executive (e.g., Process Manager, Memory Manager)
   * HAL (Hardware Abstraction Layer)
   * Device Drivers

### **User Mode vs. Kernel Mode**

* **User Mode:**
  * Limited access to hardware for security and stability.
  * If an application crashes, it won’t bring down the entire system.
* **Kernel Mode:**
  * Has unrestricted access to hardware resources.
  * A failure here (e.g., driver crash) can cause a system-wide crash, resulting in a **Blue Screen of Death (BSOD)**.

### **Core Components of Windows OS**

#### **The Executive**

The Executive manages system-level operations through the following managers:

* **Memory Manager:** Manages virtual and physical memory.
* **Process and Thread Manager:** Creates, manages, and terminates processes and threads.
* **I/O Manager:** Handles input/output requests and interacts with device drivers.
* **Security Reference Monitor (SRM):** Manages security policies and access control.
* **Object Manager:** Creates and manages system objects like files, processes, and threads.

#### **Hardware Abstraction Layer (HAL)**

* The HAL abstracts hardware differences and provides a consistent interface for the OS, allowing Windows to run on different hardware platforms without changing the core OS code.

### **Windows Boot Process**

1. **BIOS/UEFI:** Initializes hardware and loads the bootloader from the disk.
2. **Boot Manager (`bootmgr`)**: Loads the OS loader (`winload.exe`).
3. **OS Loader:** Loads the Windows kernel (`ntoskrnl.exe`) and HAL.
4. **Kernel Initialization:** Starts system processes like `smss.exe` (Session Manager).
5. **Logon Process:** Launches `winlogon.exe`, `lsass.exe`, and displays the login screen.

### **Process and Thread Management**

* **Processes:** Executing instances of programs. Each process gets its own memory space to prevent interference from other processes.
* **Threads:** Units of execution within a process. Multiple threads allow for concurrent operations.

### **Memory Management**

Windows uses **virtual memory** to ensure each process has its own isolated memory space. Key concepts include:

* **Paging:** Moves data between physical memory (RAM) and the paging file on disk.
* **Working Set:** Memory pages currently in use by a process.

### **File Systems**

* **NTFS (New Technology File System):** Default file system for modern Windows versions. It supports large files, encryption, and permissions.
* **FAT32:** Used for external drives and compatibility with other systems.

### **Security Architecture**

* **Access Control Lists (ACLs):** Define permissions for files, folders, and objects.
* **User Account Control (UAC):** Prevents unauthorized applications from making system changes.
* **Security Identifiers (SIDs):** Unique IDs assigned to users and groups.

### **Networking in Windows**

* **Winsock API:** Provides network communication services.
* **Network Protocols:** Supports TCP/IP, HTTP, SMB, and more.
* **Windows Firewall:** Built-in host-based firewall to control inbound/outbound traffic.

### **Windows Registry**

The **registry** is a hierarchical database used to store configuration settings for the OS, applications, and hardware.

* **HKEY\_CLASSES\_ROOT (HKCR):** File associations and COM objects.
* **HKEY\_LOCAL\_MACHINE (HKLM):** System-wide settings and configurations.
* **HKEY\_CURRENT\_USER (HKCU):** User-specific settings for the logged-in user.

### **Key Windows Processes and Services**

* **`explorer.exe`:** Manages the desktop and file explorer.
* **`lsass.exe`:** Local Security Authority Subsystem Service, responsible for enforcing security policies.
* **`svchost.exe`:** Hosts Windows services that run in the background.
