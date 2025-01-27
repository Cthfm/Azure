# Privilege Escalation TA0004:

## Overview Privilege Escalation TA0004:

Privilege Escalation (TA0004) involves adversaries seeking to gain higher-level permissions on a system or network to execute unauthorized actions. In Azure, this tactic often exploits misconfigurations in Role-Based Access Control (RBAC), Azure Entra, or mismanaged secrets like keys and tokens. Attackers might abuse excessive privileges, escalate roles through service principals, or compromise automation tools and managed identities to gain unauthorized access or perform privileged actions across Azure subscriptions and services. These vectors highlight the critical need for stringent access controls, continuous monitoring, and secure configuration practices within Azure environments. Let's look at the specific techniques and sub techniques provided in the IAAS Matrix.&#x20;

### **T1548 - Abuse Elevation Control Mechanism**

This technique involves exploiting legitimate mechanisms to gain elevated privileges within a system or environment. Attackers use misconfigurations, insecure practices, or poorly implemented security controls to escalate their access.

**Temporary Elevated Cloud Access (T1548.005)**

* **Example**: An attacker compromises a **Managed Identity** token on an Azure Virtual Machine (VM). They use the token to temporarily elevate privileges, allowing them to interact with Azure Resource Manager (ARM) APIs to modify resource configurations.

### **T1098 - Account Manipulation**

This technique involves modifying user accounts or access credentials to gain or maintain unauthorized access. Attackers manipulate accounts to escalate privileges, establish persistence, or evade detection.

#### **Additional Cloud Credentials T1098.001**

* **Example**: An attacker gains access to a service principal and uses the Azure CLI to generate new application secrets, effectively creating additional credentials for persistent access to the tenant.

#### **Additional Cloud Roles T1098.003**

* **Example**: By exploiting an existing compromised Azure Active Directory (AAD) user account, the attacker assigns themselves the **Owner** role on a subscription or resource group, escalating their privileges over critical resources.

#### **SSH Authorized Keys**

* **Example**: After compromising an Azure VM, the attacker modifies the `~/.ssh/authorized_keys` file of the VM’s admin account via an extension deployment script, enabling persistent SSH access without requiring credentials.

### **T1546 - Event Triggered Execution**

This technique involves configuring events or conditions that automatically execute malicious code when triggered. Attackers leverage misconfigured or maliciously modified event-driven processes to escalate privileges or maintain persistence.

#### **Event-Triggered Execution (T1546.001)**

* **Example**: An attacker modifies an Azure Function App to execute malicious payloads whenever a queue message is processed. For instance, they set up triggers to activate their code when blob storage changes occur in the subscription.

#### **Account Manipulation (T1546.004)**

* **Example**: The attacker exploits a compromised user or service principal to modify an **Azure Automation Runbook**, allowing their custom scripts to execute automatically on defined triggers like VM creation events.
