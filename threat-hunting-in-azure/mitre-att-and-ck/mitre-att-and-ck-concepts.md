# MITRE Att\&ck Concepts

## Overview:&#x20;

The following section goes over key MITRE Att\&ck Concepts to help those new to the framework. &#x20;

### Key Concepts of MITRE ATT\&CK

1. **Tactics**
2. **Techniques**
3. **Procedures**

### **1. Tactics**

**Tactics** represent the overarching goals or objectives of an attacker during different stages of a cyber attack. Think of tactics as the "why" behind an attack. They are the high-level goals that adversaries aim to achieve. There are 14 tactics in the MITRE ATT\&CK framework, each representing a different phase of the attack lifecycle.

#### **Full List of Tactics**&#x20;

* **Initial Access**:
  * **Objective**: Gain entry into your network.
  * **Techniques**: Spearphishing, exploiting public-facing applications, and drive-by downloads are common methods used to infiltrate the environment.
* **Execution**:
  * **Objective**: Run malicious code within your systems.
  * **Techniques**: Adversaries may utilize PowerShell, execute malicious files, and run scripts to achieve their goals.
* **Persistence**:
  * **Objective**: Maintain a foothold within your environment.
  * **Techniques**: Methods include creating or modifying user accounts, scheduling tasks, and installing backdoors to ensure continued access.
* **Privilege Escalation**:
  * **Objective**: Gain higher-level permissions.
  * **Techniques**: Exploiting system vulnerabilities, abusing elevated roles, and leveraging access tokens are typical strategies for escalating privileges.
* **Defense Evasion**:
  * **Objective**: Avoid detection by security defenses.
  * **Techniques**: Adversaries may disable security tools, obfuscate malicious files, and delete logs to evade security measures.
* **Credential Access**:
  * **Objective**: Steal account credentials.
  * **Techniques**: Keylogging, credential dumping, and brute force attacks are commonly used to capture usernames and passwords.
* **Discovery**:
  * **Objective**: Understand your environment.
  * **Techniques**: Techniques such as network scanning, system information discovery, and account discovery help adversaries map out the target environment.
* **Lateral Movement**:
  * **Objective**: Move through your environment to reach other systems.
  * **Techniques**: Using remote services, passing the hash, and lateral tool transfers enable adversaries to move within the network.
* **Collection**:
  * **Objective**: Gather data of interest.
  * **Techniques**: Data collection methods include keylogging, screen capture, and accessing data from local systems or network shares.
* **Command and Control (C2)**:
  * **Objective**: Maintain communication with compromised systems.
  * **Techniques**: Web protocols, DNS, and encrypted channels are used to control compromised systems remotely.
* **Exfiltration**:
  * **Objective**: Steal data from your environment.
  * **Techniques**: Data can be exfiltrated via web services, automated exfiltration tools, or compressed before transfer to external locations.
* **Impact**:
  * **Objective**: Manipulate, interrupt, or destroy systems and data.
  * **Techniques**: This includes data destruction, service disruption, and defacement to cause operational harm.
* **Resource Development**:
  * **Objective**: Establish resources for future operations.
  * **Techniques**: Acquiring infrastructure, developing capabilities, and setting up accounts help adversaries prepare for attacks.
* **Reconnaissance**:
  * **Objective**: Gather information to plan future operations.
  * **Techniques**: This involves gathering information on targets, identifying potential victims, and collecting detailed target information.

### **2. Techniques**

**Techniques** are the specific methods or ways adversaries use to achieve the goals outlined in the tactics. Think of techniques as the "how" of an attack. Each tactic can be associated with multiple techniques, detailing the various ways attackers can pursue their objectives.

* **Initial Access**:
  * **Examples of Techniques**: Spearphishing, exploiting public-facing applications, and drive-by downloads.
* **Execution**:
  * **Examples of Techniques**: Using PowerShell, executing malicious files, and running scripts.
* **Persistence**:
  * **Examples of Techniques**: Creating or modifying user accounts, scheduling tasks, and installing backdoors.
* **Privilege Escalation**:
  * **Examples of Techniques**: Exploiting system vulnerabilities, abusing elevated roles, and leveraging access tokens.
* **Defense Evasion**:
  * **Examples of Techniques**: Disabling security tools, obfuscating malicious files, and deleting logs.
* **Credential Access**:
  * **Examples of Techniques**: Keylogging, credential dumping, and brute force attacks.
* **Discovery**:
  * **Examples of Techniques**: Network scanning, system information discovery, and account discovery.
* **Lateral Movement**:
  * **Examples of Techniques**: Using remote services, passing the hash, and lateral tool transfer.
* **Collection**:
  * **Examples of Techniques**: Keylogging, screen capture, and accessing data from local systems or network shares.
* **Command and Control (C2)**:
  * **Examples of Techniques**: Using web protocols, DNS, and encrypted channels.
* **Exfiltration**:
  * **Examples of Techniques**: Data transfer over web services, automated exfiltration tools, and data compressed before transfer.
* **Impact**:
  * **Examples of Techniques**: Data destruction, service stop, and defacement.
* **Resource Development**:
  * **Examples of Techniques**: Acquiring infrastructure, developing capabilities, and setting up accounts.
* **Reconnaissance**:
  * **Examples of Techniques**: Gathering information on targets, identifying potential victims, and collecting detailed target information.

### **3. Procedures**

**Procedures** are the detailed, specific implementations of techniques used by adversaries. They describe exactly how a particular technique is executed. Procedures can vary widely even within the same technique, reflecting the diversity of methods attackers use in real-world scenarios.

**Example of a Procedure**:

* For the **Defense Evasion** technique under the **Impair Defenses** tactic, a procedure might involve disabling audit logging to prevent the recording of malicious activities, making it harder for security teams to detect the adversary's presence and actions.

### How MITRE ATT\&CK is Used

1. **Threat Detection**
2. **Incident Response**
3. **Security Gap Analysis**
4. **Threat Hunting**

### **1. Threat Detection**

By mapping detected activities and behaviors to the ATT\&CK framework, security teams can better understand the tactics and techniques being used by attackers. This helps in identifying suspicious patterns and indicators of compromise (IOCs).

**Example**:

* If unusual login attempts are detected from multiple IP addresses, this activity can be mapped to the **Brute Force** technique under the **Credential Access** tactic.

### **2. Incident Response**

During and after a security incident, the ATT\&CK framework helps incident responders to systematically analyze and categorize the attack. This structured approach aids in identifying the full scope of the breach and in developing effective containment and remediation strategies.

**Example**:

* Analyzing a malware attack can reveal multiple techniques used, such as **File Deletion** (Defense Evasion) and **Command and Scripting Interpreter** (Execution). Knowing these helps responders address all aspects of the incident.

### **3. Security Gap Analysis**

Organizations can use the ATT\&CK framework to assess their current security measures and identify gaps. By understanding which tactics and techniques are not adequately covered by existing defenses, they can prioritize improvements and investments in security controls.

**Example**:

* If an organization finds it lacks detection capabilities for the **Persistence** tactic, they might invest in tools and processes to monitor for unauthorized changes to user accounts or scheduled tasks.

### **4. Threat Hunting**

Threat hunters use the ATT\&CK framework to proactively search for signs of adversarial activity within their networks. By focusing on specific tactics and techniques, they can develop hypotheses and queries to uncover hidden threats.

**Example**:

* A threat hunter might investigate for signs of **PowerShell** usage (Execution technique) across their environment to find potential malicious activities leveraging this powerful scripting tool.

### Benefits of the MITRE ATT\&CK Framework

1. **Standardization**: Provides a common language and structure for describing adversary behaviors.
2. **Comprehensive Coverage**: Includes a wide range of tactics and techniques, offering a thorough understanding of the attack lifecycle.
3. **Real-World Relevance**: Based on actual observations of adversary behaviors, making it highly relevant for real-world threat analysis.
4. **Actionable Insights**: Helps security professionals develop targeted defenses, improve threat detection, and respond more effectively to incidents.

