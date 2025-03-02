---
hidden: true
---

# Persistence: TA0003

## **Overview of TA0003: Persistence**&#x20;

The **Persistence** tactic (TA0003) in the MITRE ATT\&CK framework focuses on techniques adversaries use to maintain access to systems and environments even after interruptions, such as credential changes or system reboots. In the context of **Azure Infrastructure-as-a-Service (IaaS)**, persistence techniques are adapted to exploit the unique features of Azure's cloud infrastructure.

### **Closer Review: Persistence in Azure IaaS**

Azure IaaS provides virtualized computing resources, including virtual machines (VMs), virtual networks, and storage. These resources offer flexibility but also introduce potential avenues for attackers to establish and maintain persistence. Below are key elements and techniques associated with persistence in Azure IaaS:

### **Account Manipulation (T1098)**

This technique involves altering accounts or credentials to maintain unauthorized access. In Azure, this includes modifying roles, adding secrets, or creating backdoors in accounts to ensure persistence. Let's look at each sub-technique in greater detail below.&#x20;

1. **Additional Cloud Credentials (T1098.001)**
   * **Example in Azure:** Adding additional Azure Entra application secrets or certificates to an application to maintain persistence. Attackers may exploit stolen Azure Entra credentials to register new secrets for applications they compromised, allowing continued access even if the original credentials are revoked.
2. **Additional Cloud Roles (T1098.003)**
   * **Example in Azure:** Assigning themselves additional roles in Azure AD (e.g., granting `Contributor` or `Owner` roles to maintain broader control). This can be achieved by exploiting compromised privileged accounts to modify role assignments.
3. **SSH Authorized Keys (T1098.003)**
   * **Example in Azure:** Inserting SSH keys into Linux virtual machines deployed in Azure. Attackers can use the Azure CLI to modify the SSH key configurations via az vm user update commands.

### **Create Account (T1136)**

The technique involves creating new accounts to establish unauthorized access or persistence. In Azure, attackers may exploit administrative privileges to create cloud accounts with elevated roles, enabling ongoing access to resources. Let's take a look at the associated subtechnique.

1. **Cloud Account (T1136.003)**
   * **Example in Azure:** Attackers can use compromised global administrator credentials to create new Azure Entra ID accounts with elevated permissions. This provides persistence while concealing the attacker’s presence.

### **Event Triggered Execution (**&#x54;1546)

This technique involves setting up mechanisms that execute malicious code in response to specific system events or conditions.&#x20;

* **Example in Azure: A**ttackers might use VM startup scripts, custom images, or scheduled tasks, or Azure functions to trigger unauthorized actions automatically during resource initialization or usage.

### **Implant Internal Image (T1525)**

* **Example in Azure:** Creating custom VM images with malicious payloads. These images, when deployed, execute the attacker's code automatically. Azure Compute Gallery can be abused to share such malicious images across multiple subscriptions.

### **Modify Authentication Process (T1556)**

This tactic involves altering authentication mechanisms to bypass security controls or maintain access. In Azure, this can include disabling MFA, manipulating Conditional Access Policies, or exploiting hybrid identity configurations to weaken authentication and facilitate persistence. Let's look at the specific subtechniques.&#x20;

1. **Multi-Factor Authentication  (T1556.006)**
   * **Example in Azure:** Disabling MFA for critical accounts or creating conditional access policies to bypass MFA requirements. This ensures attackers can access the environment without triggering MFA challenges.
2. **Hybrid Identity (T1556.007)**
   * **Example in Azure:** Exploiting misconfigurations in hybrid identity setups, such as Azure AD Connect. Attackers might sync malicious on-premises accounts to Azure AD or manipulate the sync rules to bypass security policies.
3. **Conditional Access Policies (T1556.009)**
   * **Example in Azure:** Modifying or disabling conditional access policies to weaken security controls, allowing unrestricted access to specific accounts or resources.

### **Valid Accounts (T1078)**

This technique involves using legitimate credentials to gain or maintain unauthorized access. In Azure, attackers may exploit default accounts, compromised credentials, or inactive cloud accounts to blend in with normal user activity, avoid detection, and sustain persistence within the environment. Let's look at the sub-techniques more closely.

1. **Default Accounts (T1078.001)**
   * **Example in Azure:** Exploiting default credentials in Azure services, such as storage accounts or default administrative accounts in deployed VMs. Attackers may use these accounts to pivot or escalate privileges.
2. **Cloud Accounts (T1078.004)**
   * **Example in Azure:** Utilizing compromised Azure Entra accounts or guest accounts to maintain access. Guest accounts in Azure Entra are often overlooked and can be used for long-term persistence.
