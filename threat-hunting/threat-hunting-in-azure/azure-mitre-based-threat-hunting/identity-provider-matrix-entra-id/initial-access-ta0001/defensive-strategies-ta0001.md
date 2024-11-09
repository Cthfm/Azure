# Defensive Strategies: TA0001

## **Defensive Strategies for TA0001 - Initial Access**

The Initial Access (TA0001) phase involves attackers gaining entry into a target environment, often through phishing, exploiting vulnerabilities, abusing remote services, or using stolen credentials. In Azure environments, it’s critical to block unauthorized access early through secure configurations, identity protection, and attack detection. Below are defensive strategies mapped to the techniques and sub-techniques of TA0001.

### **1. Secure Public-Facing Applications and Services**

**Mitigates:** T1190 - Exploit Public-Facing Application

* **Action:** Identify and patch vulnerabilities in public-facing Azure services and web apps.
* **Azure Solution:**
  * Use **Azure Web Application Firewall (WAF)** to block attacks targeting Azure-hosted applications.
  * Enable **Azure Defender for App Service** to detect vulnerabilities and monitor for suspicious activity.
  * Implement **Azure Security Center** recommendations to harden configurations.

### **2. Enforce Multi-Factor Authentication (MFA)**

**Mitigates:** T1078 - Valid Accounts (Cloud Accounts)

* **Action:** Ensure **MFA is enforced** for all accounts, especially privileged ones.
* **Azure Solution:**
  * Use **Conditional Access Policies** to require MFA for user logins.
  * Apply **Azure AD Identity Protection** to detect and block risky sign-ins.
  * Monitor token re-use to prevent attackers from abusing compromised tokens for initial access.

### **3. Harden Remote Services**

**Mitigates:** T1133 - External Remote Services

* **Action:** Restrict access to **RDP, SSH, and Azure Bastion** services.
* **Azure Solution:**
  * Use **Just-in-Time (JIT) VM access** to limit remote access windows.
  * Monitor **Azure Bastion logs** to detect suspicious activity.
  * Apply **NSG (Network Security Group) rules** to restrict access from unauthorized IPs.

### **4. Detect and Mitigate Phishing Attempts**

**Mitigates:** T1566 - Phishing (Spearphishing Link, Spearphishing Attachment)

* **Action:** Block phishing emails and prevent OAuth consent phishing.
* **Azure Solution:**
  * Use **Microsoft Defender for Office 365** to block malicious emails and attachments.
  * Monitor for **unusual OAuth consent requests** with **Azure AD Identity Protection**.
  * Train users to recognize phishing attempts and report suspicious emails.

### **5. Monitor OAuth and Consent Grants to Applications**

**Mitigates:** T1199 - Trusted Relationship

* **Action:** Prevent attackers from abusing **application consents** to gain access.
* **Azure Solution:**
  * Use **Azure AD Conditional Access Policies** to limit which apps can access sensitive resources.
  * Enable alerts in **Azure Sentinel** for new OAuth permissions being granted.
  * Regularly review **third-party app permissions** to detect unauthorized grants.

### **6. Regularly Rotate and Monitor Credentials**

**Mitigates:** T1078 - Valid Accounts (Default Accounts)

* **Action:** Rotate **service principal keys** and **API tokens** regularly to limit abuse.
* **Azure Solution:**
  * Use **Azure Key Vault** to store and rotate secrets.
  * Monitor for new keys being added to service principals with **Azure Security Center**.
  * Disable **default or unused accounts** in VMs and services to reduce attack surface.

### **7. Apply Conditional Access Policies for Trusted Devices and Networks**

**Mitigates:** T1199 - Trusted Relationship

* **Action:** Limit access to Azure resources from only **trusted devices and IP addresses**.
* **Azure Solution:**
  * Configure **Conditional Access Policies** to restrict access based on device compliance.
  * Use **Azure Identity Protection** to detect and block suspicious sign-ins from unknown devices.
  * Monitor for tenant-to-tenant attacks, especially in multi-tenant environments.

### **8. Secure DevOps Pipelines from Supply Chain Attacks**

**Mitigates:** T1195 - Supply Chain Compromise (Software Dependencies and Tools)

* **Action:** Harden DevOps tools and scan for vulnerabilities in pipelines.
* **Azure Solution:**
  * Use **Azure DevOps Security Scanning** to detect vulnerable libraries in CI/CD pipelines.
  * Monitor Azure pipelines for unauthorized changes to configurations and jobs.
  * Store build secrets securely in **Azure Key Vault**.

### **9. Block Legacy Authentication Protocols**

**Mitigates:** T1078.002 - Domain Accounts

* **Action:** Disable **legacy authentication protocols** that don’t support MFA (e.g., POP, IMAP).
* **Azure Solution:**
  * Use **Azure Security Center** to detect and disable legacy protocols.
  * Enforce **modern authentication** via **Conditional Access Policies**.
  * Monitor for logins using **basic authentication protocols** and block them.

### **10. Automate Detection and Response with Azure Sentinel**

**Mitigates:** T1133 - External Remote Services, T1078 - Valid Accounts

* **Action:** Use **Azure Sentinel** to detect and respond to initial access attempts.
* **Azure Solution:**
  * Configure **Azure Sentinel playbooks** to disable accounts or revoke access tokens upon suspicious logins.
  * Monitor **activity logs** for signs of brute force or unauthorized access attempts.
  * Integrate **Defender for Cloud** with Sentinel to enhance visibility and response capabilities.

### **11. Ensure Tenant Access Has Least Privilege Access**

**Mitigates:** Technique: T1199 - Trusted Relationship

* **Action:** Review Tenant Access Policies
* **Azure Solution:**
  * Configure access policies with least privilege.
  * Monitor Sign-In logs for signs of brute force or unauthorized access attempts
  * Integrate Defender for Identity to detect suspicious behavior.&#x20;
  * Review Activity logs for any suspicious behavior by '#EXT' users

### **Summary of Defensive Measures for TA0001**

| **Defensive Strategy**                | **Mitigates**                             | **Azure Solution**                                                    |
| ------------------------------------- | ----------------------------------------- | --------------------------------------------------------------------- |
| Secure Public-Facing Applications     | T1190 - Exploit Public-Facing Application | Use WAF and Defender for App Services                                 |
| Enforce Multi-Factor Authentication   | T1078 - Valid Accounts                    | Use Conditional Access and Identity Protection                        |
| Harden Remote Services                | T1133 - External Remote Services          | Apply JIT access and restrict Bastion access                          |
| Detect and Block Phishing             | T1566 - Phishing                          | Use Defender for O365 to block phishing emails                        |
| Monitor OAuth Grants and Permissions  | T1199 - Trusted Relationship              | Use Azure Activity logs to detect OAuth consent phishing              |
| Rotate and Monitor Credentials        | T1078 - Valid Accounts                    | Use Key Vault for secret management and rotation                      |
| Apply Conditional Access Policies     | T1199 - Trusted Relationship              | Block access from untrusted devices and networks                      |
| Secure DevOps Pipelines               | T1195 - Supply Chain Compromise           | Use Azure DevOps to scan images and Key Vault for secrets management. |
| Block Legacy Authentication Protocols | T1078.002 - Domain Accounts               | Disable basic authentication protocols                                |
| Automate Detection and Response       | T1133 - External Remote Services          | Use Sentinel playbooks for automated incident response                |
| Tenant Access Policies                | T1199 - Trusted Relationship              | Use Least Privilege and MFA                                           |
