# Initial Access TA0001

## **Overview**

The Initial Access phase in the MITRE ATT\&CK framework refers to how attackers gain an initial foothold in a target environment. In Azure, this often involves abusing identity, exploiting public-facing applications, or leveraging compromised credentials to infiltrate the cloud infrastructure. Below are the core concepts of TA0001.

### **1. Exploiting Public-Facing Applications**

**Technique: T1190 - Exploit Public-Facing Application**\
Attackers target vulnerabilities in exposed services to gain unauthorized access.

* Azure Kubernetes Service (AKS): Leveraging misconfigured ingress controllers or exploiting known vulnerabilities in containerized applications.

### **2.** Trusted Relationship

**Technique:** T1199 **- Trusted Relationship**\
The Trusted Relationship technique involves exploiting relationships or permissions granted between organizations or systems. Specifically:

* **Third-Party Access:** Adversaries may compromise external entities like IT service providers, contractors, or resellers who already have access to the victim’s environment.
* **Delegated Permissions:** Abuse of delegated administrative privileges in cloud environments, like Office 365 or Azure, is a prime example.
* **Insider-Like Access:** The adversary leverages permissions that bypass standard external access controls, often because the trust between entities or systems is poorly scrutinized.

### **3. Valid Accounts**

**Technique:** T1078 **- Valid Accounts**\
Attackers obtain or abuse credentials of existing accounts in order to complete other tactics within MITRE Att\&ck.&#x20;

* **T1078.001 - Default Accounts:**\
  &#x20;Utilizing default account credentials in order to complete other tactics within the MITRE Att\&CK framework.
* **T1078.004 - Cloud Accounts:**\
  Use stolen Entra ID tokens to access resources without MFA, such as Key Vault secrets and Blob storage.

