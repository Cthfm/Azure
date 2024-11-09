# Defensive Strategies for TA0006

## **Defensive Strategies for TA0006 - Credential Access**

Defending against **Credential Access (TA0006)** requires a **multi-layered approach** focusing on **identity management, key rotation, monitoring, and hardening privileged accounts and services**. Attackers may attempt to steal **passwords, OAuth tokens, API keys, or access tokens** through various means, such as **brute force, memory scraping, or metadata abuse**. Below are **defensive strategies** mapped to relevant **techniques and Azure-specific implementations**.

### **1. Enforce Multi-Factor Authentication (MFA)**

**Mitigates:** T1078 - Valid Accounts, T1550 - Use Alternate Authentication Material

* **Action:** Require **MFA** to limit the impact of stolen credentials.
* **Azure Solution:**
  * Enforce **MFA with Conditional Access Policies** for all accounts, including service principals.
  * Use **Azure AD Identity Protection** to monitor for compromised credentials and block risky sign-ins.

### **2. Implement Conditional Access Policies**

**Mitigates:** T1550.001 - Application Access Tokens, T1110 - Brute Force

* **Action:** Apply **IP-based and device-based restrictions** to reduce credential misuse.
* **Azure Solution:**
  * Use **Conditional Access Policies** to block access from untrusted locations or unknown devices.
  * Configure **risk-based access policies** in **Azure AD** to respond to unusual login behaviors dynamically.

### **3. Rotate and Monitor Secrets and Keys Regularly**

**Mitigates:** T1552 - Unsecured Credentials, T1555 - Credentials from Password Stores

* **Action:** Store and **rotate secrets periodically** to reduce the value of stolen credentials.
* **Azure Solution:**
  * Use **Azure Key Vault** to securely manage and rotate service principal keys and API keys.
  * Monitor **Key Vault logs** with **Azure Sentinel** to detect unauthorized secret access.

### **4. Secure Metadata Services to Prevent Token Theft**

**Mitigates:** T1552.004 - Credentials in Cloud Metadata

* **Action:** Restrict access to **Instance Metadata Service (IMDS)** on Azure VMs.
* **Azure Solution:**
  * Use **Network Security Groups (NSGs)** to block unauthorized access to IMDS.
  * Monitor for requests to IMDS using **Azure Defender for VMs**.

### **5. Detect and Block Brute Force Attacks**

**Mitigates:** T1110 - Brute Force (Password Spraying)

* **Action:** Detect and **throttle brute force attacks** targeting Azure AD accounts.
* **Azure Solution:**
  * Use **Azure AD Identity Protection** to detect and block password spraying attempts.
  * Enable **account lockout policies** to temporarily block accounts under attack.

### **6. Monitor for OAuth Token Abuse**

**Mitigates:** T1550.001 - Application Access Tokens

* **Action:** Track **OAuth token usage** and identify abuse.
* **Azure Solution:**
  * Monitor for unusual OAuth token requests with **Azure Sentinel**.
  * Regularly audit **third-party application permissions** in Azure AD.

### **7. Enable Logging and Monitor Credential Usage**

**Mitigates:** T1003 - OS Credential Dumping, T1555 - Credentials from Password Stores

* **Action:** Enable **logging for credential usage and secrets access** to detect suspicious behavior.
* **Azure Solution:**
  * Use **Azure Monitor** and **Activity Logs** to track the creation and use of service principal keys.
  * Set alerts in **Azure Sentinel** for unusual secret access or password changes.

### **8. Use Passwordless Authentication**

**Mitigates:** T1110 - Brute Force, T1078 - Valid Accounts

* **Action:** Implement **passwordless authentication mechanisms** to reduce the risks associated with password theft.
* **Azure Solution:**
  * Use **FIDO2 keys or biometric authentication** in Azure AD for user accounts.
  * Promote the use of **Managed Identities** to reduce reliance on service principal passwords.

### **9. Regularly Audit Service Principal Permissions**

**Mitigates:** T1078 - Valid Accounts (Cloud Accounts)

* **Action:** Ensure **service principals have only the permissions they need** to perform their tasks.
* **Azure Solution:**
  * Use **Azure AD Privileged Identity Management (PIM)** to review service principal permissions.
  * Monitor for new or unauthorized service principal key creation with **Azure Sentinel**.

### **10. Detect and Prevent Memory Dumping on VMs**

**Mitigates:** T1003 - OS Credential Dumping

* **Action:** Harden VMs against **memory dumping attacks** that target cached credentials.
* **Azure Solution:**
  * Use **Microsoft Defender for Endpoint** to block tools like **Mimikatz**.
  * Enable **Credential Guard** on Azure VMs to protect sensitive data in memory.

### **Summary of Defensive Strategies for TA0006**

| **Defensive Strategy**                | **Mitigates**                                                           | **Azure Solution**                                           |
| ------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| Enforce Multi-Factor Authentication   | T1078 - Valid Accounts, T1550 - Use Alternate Authentication Material   | Enforce MFA using Conditional Access Policies                |
| Implement Conditional Access Policies | T1110 - Brute Force, T1550.001 - Application Access Tokens              | Apply IP-based restrictions and device compliance checks     |
| Rotate and Monitor Secrets Regularly  | T1552 - Unsecured Credentials, T1555 - Credentials from Password Stores | Use Azure Key Vault and monitor secret usage logs            |
| Secure Metadata Services              | T1552.004 - Credentials in Cloud Metadata                               | Use NSGs to restrict access to IMDS and monitor requests     |
| Detect and Block Brute Force Attacks  | T1110 - Brute Force                                                     | Use Azure AD Identity Protection to block password spraying  |
| Monitor OAuth Token Usage             | T1550.001 - Application Access Tokens                                   | Monitor OAuth requests with Azure Sentinel                   |
| Enable Logging for Credential Usage   | T1003 - OS Credential Dumping, T1555 - Credentials from Password Stores | Use Azure Monitor and Sentinel to detect unusual access      |
| Use Passwordless Authentication       | T1110 - Brute Force, T1078 - Valid Accounts                             | Implement FIDO2 or biometric authentication in Azure AD      |
| Audit Service Principal Permissions   | T1078 - Valid Accounts                                                  | Use PIM to review and restrict service principal permissions |
| Prevent Memory Dumping on VMs         | T1003 - OS Credential Dumping                                           | Use Defender for Endpoint and enable Credential Guard        |
