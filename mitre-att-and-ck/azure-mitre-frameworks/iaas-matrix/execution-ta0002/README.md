# Execution TA0002

The Execution (TA0002) tactic in the MITRE ATT\&CK framework involves adversaries running malicious code or commands to advance their objectives, such as stealing data or achieving persistence. This includes techniques like using command-line interpreters (e.g., PowerShell), exploiting vulnerabilities, or leveraging cloud tools (e.g., Azure CLI). Execution often follows Initial Access (TA0001) and is pivotal in enabling further attack stages. Key defenses include least privilege, monitoring suspicious activity, restricting scripting tools, and behavior-based detection.

### **1. Cloud Administration Command** T1651

Adversaries use legitimate cloud administrative tools or commands to execute actions in a cloud environment.

* **Example**:
  * **Azure CLI**: An adversary uses the Azure CLI to run a command that creates a new Azure VM and executes a malicious payload.

### **2. Command and Scripting Interpreter** T1059

Involves adversaries using interpreters like PowerShell, Bash, or Python to execute commands or scripts for malicious purposes, often leveraging built-in tools to avoid detection.

* **Example**:
  * Using Azure PowerShell to execute a script that adds a new role assignment for an attacker-controlled identity.
* **T1078.001 - Cloud API:**\
  Adversaries interact with cloud APIs to perform unauthorized actions or execute commands. Adversaries use the Azure Resource Manager (ARM) REST API to deploy a new function app with malicious payloads.

### **3. Serverless Execution** T1648

Adversaries execute code in serverless environments like Azure Functions.

* **Example**:
  * Deploying a malicious Azure Function app that performs cryptocurrency mining or data exfiltration.

### **4. User Execution** T1204

Involves tricking users into performing actions, such as opening malicious files or clicking links, that execute adversary-controlled code.

* **Example**:
  * Adversaries trick users into executing malicious files disguised as images or other benign-looking formats.
*   **T1204.004: Malicious Image**

    Distributing a malicious Docker container image to Azure Container Registry (ACR) that, when deployed in AKS or another Azure service, executes a reverse shell.
