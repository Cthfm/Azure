# Defensive Strategies

## Overview

The Persistence tactic in Azure IaaS enables adversaries to maintain access by exploiting credentials, creating accounts, modifying authentication, or deploying malicious configurations like custom VM images. Defenses include strict access controls, monitoring, and enforcing least privilege. This section goes over defensive strategies by each technique.&#x20;

### **Account Manipulation (T1098)**

1. **Additional Cloud Credentials**
   * **Defensive Strategies:**
     * Enforce strict access control for Azure Entra ID application management.
     * Enable and monitor Azure Entra ID Audit Logs for changes to application credentials or certificates.
     * Implement Conditional Access Policies to restrict access to sensitive Azure Entra operations.
     * Use Azure Key Vault to securely manage application secrets and certificates.
2. **Additional Cloud Roles**
   * **Defensive Strategies:**
     * Monitor role assignment changes using Azure Activity Logs and configure alerts for suspicious role escalations.
     * Enforce the principle of least privilege (PoLP) and regularly review role assignments.
     * Use Azure Policy to deny or restrict assignments of high-privilege roles to unnecessary users or groups.
3. **SSH Authorized Keys**
   * **Defensive Strategies:**
     * Disable password-based SSH access and enforce SSH key management policies.
     * Regularly audit and rotate SSH keys for Linux VMs in Azure.
     * Use Azure Policy to enforce VM configurations, such as blocking unauthorized key updates.
     * Explore Azure Bastion as it provides browser based SSH/RDP access without exposing resources to the public internet.

### **Create Account (T1136)**

1. **Cloud Account**
   * **Defensive Strategies:**
     * Restrict account creation privileges to a small group of administrators.
     * Enable Azure Entra Audit Logging  to detect suspicious account creation activities.
     * Use Conditional Access Policies to block sign-ins from newly created accounts until verified.

## **Event Triggered Execution (**&#x54;1546)

1. **Implant Internal Image**
   * **Defensive Strategies:**
     * Verify and restrict permissions for creating and sharing custom VM images in Azure Compute Gallery.
     * Use Azure Policy to ensure only authorized images are used in deployments.
     * Monitor Azure Activity Logs for suspicious image creation or modification activities.

### **Modify Authentication Process (T1556)**

1. **Multi-Factor Authentication (MFA)**
   * **Defensive Strategies:**
     * Enforce MFA for all privileged accounts and sensitive resources.
     * Use Azure AD Identity Protection to detect and respond to risky user sign ins.
     * Monitor changes to MFA settings in Azure Entra ID and configure alerts for suspicious modifications.
2. **Hybrid Identity**
   * **Defensive Strategies:**
     * Regularly review and audit Azure Entra Connect synchronization rules.
     * Enable logging and monitoring for Azure Entra Connect to detect unusual sync activities.
     * Restrict access to Azure Entra Connect configurations and enforce strong security practices for hybrid identity.
3. **Conditional Access Policies**
   * **Defensive Strategies:**
     * Implement role-based access control (RBAC) to restrict who can modify Conditional Access Policies.
     * Enable versioning and logging of Conditional Access Policies for auditing.
     * Use Azure Security Center to monitor policy compliance and flag risky configurations.

### **Valid Accounts (T1078)**

1. **Default Accounts**
   * **Defensive Strategies:**
     * Disable or rename default administrative accounts in deployed VMs or other services.
     * Regularly audit Azure environments for unused or default accounts.
     * Implement just-in-time (JIT) access for administrative accounts via Azure Security Center.
2. **Cloud Accounts**
   * **Defensive Strategies:**
     * Enable and enforce strong password policies for all Azure AD accounts.
     * Monitor sign-ins from unusual locations or devices using Azure AD Identity Protection.
     * Review and disable inactive or guest accounts regularly.

### **General Recommendations Across All Techniques**

* **Enable Logging and Monitoring:** Use tools like Azure Monitor, Azure Sentinel, and Azure Activity Logs to detect anomalies. Defender XDR is also an option here.
* **Automated Response:** Configure automated responses to specific triggers, such as disabling suspicious accounts or revoking roles.
* **Least Privilege Access:** Enforce RBAC and restrict administrative privileges to minimize the impact of compromise.
* **Continuous Training:** Educate administrators and users on recognizing phishing attempts, credential misuse, and policy abuse. Continue to train your blue teams by conducting regular exercises by internal or third-party red teams.
* **Regular Audits:** Perform periodic security reviews and penetration tests to identify gaps in defenses.
