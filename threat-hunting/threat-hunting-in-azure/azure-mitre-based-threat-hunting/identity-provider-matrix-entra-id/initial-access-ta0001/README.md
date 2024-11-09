# Initial Access: TA0001

## **Overview**

The Initial Access phase in the MITRE ATT\&CK framework refers to how attackers gain an initial foothold in a target environment. In Azure, this often involves abusing identity, exploiting public-facing applications, or leveraging compromised credentials to infiltrate the cloud infrastructure. Below are the core concepts of TA0001.

### **1. Exploiting Public-Facing Applications**

**Technique: T1190 - Exploit Public-Facing Application**\
Attackers target vulnerabilities in exposed services to gain unauthorized access.

* &#x20;Exploit a **vulnerable web app hosted on Azure App Service** to upload a malicious web shell and gain control over the backend server.

### **2. Leveraging Stolen Credentials (Valid Accounts)**

**Technique: T1078 - Valid Accounts**\
Attackers use compromised or weak credentials to log into systems without triggering alarms.

* **T1078.004 - Cloud Accounts:**\
  Use **stolen Azure AD tokens** to access resources without MFA, such as Key Vault secrets and Blob storage.

### **3. Phishing for Credentials or Token Hijacking**

**Technique: T1566 - Phishing**\
Attackers use social engineering to trick users into revealing credentials or approving malicious OAuth apps.

* **T1566.001 - Spearphishing Attachment:**\
  &#x20;Send a **malicious Excel file** with embedded macros to exfiltrate tokens from a victim’s device.
* **T1566.002 - Spearphishing Link:**\
  Direct the target to a **malicious OAuth consent page**, granting the attacker access to Microsoft 365 resources.

### **4. Abusing Remote Services**

**Technique: T1133 - External Remote Services**\
Adversaries gain access by exploiting exposed remote services like **RDP, SSH, or Azure Bastion**.

* Use weak or stolen credentials to access a VM to gain a foothold in the environment.

### **5. Supply Chain Compromise**

**Technique: T1195 - Supply Chain Compromise**\
Attackers compromise a third-party component to infiltrate the target environment.

* **T1195.002 - Compromise Software Supply Chain:**\
  An attacker injects malicious code into a **third-party library** that is integrated into an Azure DevOps CI/CD pipeline.

### **6. Abusing Trusted Relationships**

**Technique: T1199 - Trusted Relationship**\
Attackers exploit inter-organizational trust relationships to gain access to resources.

* **Azure Example:** Leverage a **misconfigured tenant-to-tenant trust** to access sensitive data in another Azure subscription.

### **7. Exploiting Default or Weak Credentials**

**Technique: T1078.001 - Default Accounts**\
Attackers target resources configured with default or weak credentials.

* **Azure Example:** A newly deployed **Azure VM** is left with default admin credentials, allowing the attacker to gain access.

### **8. Using Exploited Hardware or IoT Devices**

**Technique: T1195.003 - Compromise Hardware Supply Chain**\
Adversaries tamper with hardware to introduce malicious code or backdoors.

* **Azure Example:** Attackers compromise firmware in **IoT devices** connected to **Azure IoT Hub**, gaining access to the cloud environment.

### **Summary of Key Concepts with Techniques for TA0001**

| **Key Concept**                       | **Technique**                                | **Azure Example**                                                       |
| ------------------------------------- | -------------------------------------------- | ----------------------------------------------------------------------- |
| Exploiting Public-Facing Applications | T1190 - Exploit Public-Facing Application    | Exploit an Azure App Service to upload a web shell                      |
| Stolen Credentials (Valid Accounts)   | T1078 - Valid Accounts                       | Use stolen Azure AD tokens to access resources                          |
| Phishing and Social Engineering       | T1566 - Phishing                             | Trick user into granting OAuth consent                                  |
| Abusing Remote Services               | T1133 - External Remote Services             | Use weak credentials via Azure Bastion to access a VM                   |
| Supply Chain Compromise               | T1195 - Supply Chain Compromise              | Inject malicious code into an Azure DevOps CI/CD pipeline               |
| Trusted Relationship Exploitation     | T1199 - Trusted Relationship                 | Abuse tenant-to-tenant trust to gain access                             |
| Exploiting Default Credentials        | T1078.001 - Default Accounts                 | Gain access via default admin credentials on a VM                       |
| Compromised Hardware or IoT Devices   | T1195.003 - Compromise Hardware Supply Chain | Gain access through compromised IoT firmware connected to Azure IoT Hub |

###
