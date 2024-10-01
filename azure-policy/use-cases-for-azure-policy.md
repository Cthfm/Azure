# Use Cases for Azure Policy

## **Common Use Cases for Azure Policy in Threat Hunting**

Azure Policy plays a critical role in ensuring the security of your cloud environment by automatically detecting and addressing misconfigurations or violations of security controls. For threat hunters, Azure Policy provides both preventive and detective capabilities that reduce the attack surface and help monitor for potential threats. Let’s explore some common use cases that are directly relevant to threat hunters.

{% hint style="danger" %}
Whether or not certain activity is blocked or audited will depend on the risk appetite of the business and is unique to each organization. It is always highly recommended and encouraged to follow standard security best practices.
{% endhint %}

### **1. Enforcing Encryption on Sensitive Data**

**Use Case**: Ensuring that all sensitive data stored in Azure, such as in **Azure Storage Accounts** or **Azure SQL Databases**, is encrypted to prevent unauthorized access if data is breached or accessed maliciously.

**How Azure Policy Helps:**

* You can create or assign a policy that enforces encryption at rest on all storage resources. The policy audits storage accounts, databases, or other resources and flags any that do not have encryption enabled.
* **Example Policy**: “Ensure encryption is enabled on all storage accounts.” This policy could deny the creation of unencrypted storage accounts, ensuring that sensitive data is always stored securely.

### **2. Auditing Public IPs on Virtual Machines**

**Use Case**: Public IP addresses on virtual machines expose them to the internet, increasing the risk of brute force attacks, DDoS attacks, and unauthorized access. As a threat hunter, you want to audit and restrict the use of public IP addresses to minimize the attack surface.

**How Azure Policy Helps:**

* Azure Policy can audit and even deny the creation of VMs with public IP addresses unless explicitly allowed. You can create a policy that automatically flags or blocks VMs that are deployed with a public IP, ensuring that only specific machines have external exposure.
* **Example Policy**: “Audit VMs with public IP addresses.” This policy audits any VM with a public IP and logs non-compliant resources. You can review these logs to investigate potential risks or enforce tighter controls by switching to a **Deny** effect.

**Threat Hunting Advantage: Using the audit data, threat hunters can monitor the exposure of VMs to the internet and detect patterns of potential unauthorized access or attempts to exploit publicly exposed resources.**

### **3. Enforcing Multi-Factor Authentication (MFA) for Administrative Accounts**

**Use Case**: Protecting administrative accounts is crucial since compromised privileged accounts can lead to complete control of your environment. Threat hunters need to ensure that all administrative accounts use **Multi-Factor Authentication (MFA)** to prevent unauthorized access, even if passwords are compromised.

**How Azure Policy Helps:**

* You can create an Azure Policy that ensures MFA is enabled for all administrative accounts within **Azure Active Directory (AAD)**. The policy can audit accounts that lack MFA and log them for further investigation, or automatically enforce MFA.
* **Example Policy**: “Audit Azure AD users without MFA enabled.” This policy checks administrative accounts and flags any that don’t have MFA enabled.

**Threat Hunting Advantage: By auditing accounts without MFA, you can immediately detect potential security gaps and take action to secure these high-risk accounts before they are exploited by attackers.**

### **4. Requiring Network Security Groups (NSGs) on Virtual Machines**

**Use Case**: Network Security Groups (NSGs) are essential for controlling inbound and outbound traffic to virtual machines. Without proper NSG configurations, VMs can be exposed to unauthorized access or malicious network traffic. Threat hunters need to ensure that every VM is protected by NSGs.

**How Azure Policy Helps:**

* Azure Policy can enforce the use of NSGs on all virtual machines by auditing VMs that don’t have an NSG attached or by denying the creation of VMs without NSGs.
* **Example Policy**: “Deny the creation of VMs without a Network Security Group (NSG).” This policy ensures that all VMs have proper traffic controls in place, reducing the risk of unauthorized access or data exfiltration.

**Threat Hunting Advantage: Using Azure Policy to enforce NSGs simplifies your ability to detect misconfigurations and close potential attack vectors, ensuring that traffic to and from VMs is always controlled and monitored.**

### **5. Ensuring Diagnostic Logs are Enabled**

**Use Case**: As a threat hunter, having access to diagnostic logs is crucial for identifying and investigating potential threats. You want to ensure that all Azure resources (e.g., VMs, storage accounts, databases) have diagnostic logging enabled to capture critical security events.

**How Azure Policy Helps:**

* Azure Policy can be used to ensure that diagnostic logs are always enabled on resources. If logging is disabled on any resource, the policy will flag the issue and can automatically enable the logging settings.
* **Example Policy**: “Ensure diagnostic logs are enabled for all VMs.” This policy ensures that all VM activity is logged, providing essential data for threat hunting and forensic investigations.

**Threat Hunting Advantage: Diagnostic logs give you visibility into resource activities, helping you detect anomalies, investigate incidents, and track potential threats across your environment. By ensuring logs are always enabled, you never miss critical security data.**

### **6. Controlling Resource Locations**

**Use Case**: To comply with organizational security standards or regulatory requirements, some data must be stored in specific geographic regions (e.g., within the EU for GDPR compliance). As a threat hunter, you want to ensure that resources are only deployed in approved regions to avoid data exposure to unauthorized jurisdictions.

**How Azure Policy Helps:**

* You can create a policy that restricts resource creation to specific regions. For example, the policy could deny the creation of any resource outside of the **EU** or the organization's approved regions.
* **Example Policy**: “Restrict resource creation to specific geographic regions.” This policy ensures that resources are always deployed in approved locations, reducing compliance risks.

**Threat Hunting Advantage: By restricting resource locations, you minimize the risk of sensitive data being accessed or stored in unauthorized locations, reducing the chance of regulatory violations or data exposure in high-risk regions.**

### **7. Auditing and Denying Deprecated Services**

**Use Case**: Over time, certain Azure services may become deprecated or obsolete. Using deprecated services can expose your environment to security vulnerabilities as they are no longer updated with security patches. Threat hunters must ensure that deprecated services are not used in the environment.

**How Azure Policy Helps:**

* Azure Policy can audit and deny the usage of deprecated or unsupported services, ensuring that all resources comply with the latest security and performance standards.
* **Example Policy**: “Audit deprecated services.” This policy flags any use of deprecated services, allowing you to investigate and decommission them as needed.

**Threat Hunting Advantage: Ensuring that only supported services are used reduces the risk of unpatched vulnerabilities, helping you maintain a secure and up-to-date cloud environment.**
