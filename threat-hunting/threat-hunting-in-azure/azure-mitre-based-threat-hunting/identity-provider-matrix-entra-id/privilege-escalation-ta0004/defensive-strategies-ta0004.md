# Defensive Strategies: TA0004

## **Defensive Strategies for TA0004 - Privilege Escalation**

Defending against Privilege Escalation in Azure environments requires tight access control, role monitoring, automation security, and detection mechanisms. Below are key defensive measures mapped to relevant techniques, along with Azure-specific tools and configurations to mitigate these risks.

#### 1. **Abuse Elevation Control Mechanism**

**Technique: T1548 - Abuse Elevation Control Mechanism**

* **Defensive Strategy**: Implement Just-In-Time (JIT) access and review JIT configuration in Azure Entra ID Privileged Identity Management (PIM) settings. Avoid setting ‘Automatic Approval Mode’ on sensitive resources.
* **Monitoring and Alerting**: Establish alerts for changes in JIT configurations and monitor logs for abnormal access requests, particularly for high-privilege roles. Log and review activity in Entra ID PIM audit logs, focusing on privilege elevation attempts.

**T1548.005 - Temporary Elevated Cloud Access**

* **Defensive Strategy**: Enforce Conditional Access Policies to restrict and log elevated access, limiting the duration and scope of temporary roles. Ensure that time-limited permissions are appropriately configured, with strict criteria for access and expiry.
* **Monitoring and Alerting**: Enable Azure Monitor alerts for changes in JIT and PIM configurations and review for any unexpected approvals. Investigate any PIM assignments that are extended or overridden without proper authorization.

### 2. **Account Manipulation**

**Technique: T1098 - Account Manipulation**

* **Defensive Strategy**: Regularly review and enforce sign-in risk and user risk policies in Azure to restrict account manipulation, such as password resets and MFA bypasses. Utilize **Privileged Identity Management (PIM)** to set just-in-time role activation, minimizing persistent access to privileged roles.
* **Monitoring and Alerting**: Set up **alerts for changes to account properties** (e.g., MFA settings, role assignments). Log modifications to sensitive accounts, such as those with admin or contributor roles, in Azure AD logs.

**T1098.001 - Additional Cloud Credentials**

* **Defensive Strategy**: Disable SAS Token generation when possible and use RBAC instead. Otherwise ensure SAS token generation permissions and enforce short token expiration times (hours, not days). Use **Azure Key Vault** for secure storage of access keys, and rotate storage account access keys regularly.
* **Monitoring and Alerting**: Enable alerts for **SAS token generation** and audit all generated tokens for unusual permissions or extended expiration periods. Monitor OAuth Application credentials and review changes to App Registration settings for additional credentials.

**T1098.003 - Additional Cloud Roles**

* **Defensive Strategy**: Limit role assignment creation permissions and monitor **‘Contributor’ and other high-privilege role assignments** to ensure they align with documented needs. Implement least-privilege roles using **Role-Based Access Control (RBAC)**.
* **Monitoring and Alerting**: Set alerts for **new role assignments**, especially ‘Contributor’ roles in sensitive resource groups or subscriptions. Regularly review RBAC assignments, logging changes in Azure AD Privileged Role Administrator roles.

**T1098.005 - Registered Device**

* **Defensive Strategy**: Secure **Intune and other device management policies** with strict approval workflows. Restrict device registration to prevent unauthorized device enrollment. Implement compliance policies in Intune to ensure only secure devices can access resources.
* **Monitoring and Alerting**: Monitor **Intune policy changes** and log device registration activity for unusual devices. Use **Conditional Access** to block or require additional verification for newly registered devices.

### 3. **Domain or Tenant Policy Modification**

**Technique: T1484 - Domain or Tenant Policy Modification**

* **Defensive Strategy**: Limit the number of accounts with permissions to modify domain trusts and use **Conditional Access Policies** to restrict high-impact actions to specific locations or IP ranges. Regularly review domain trust relationships and limit federated identity access.
* **Monitoring and Alerting**: Enable logging and alerts for changes to domain trust configurations. Periodically review Azure AD audit logs for new or modified domain trust entries and cross-check them against approved configurations.

**T1484.002 - Trust Modification**

* **Defensive Strategy**: Enforce **strict trust modification policies** and limit access to tenant federation settings to prevent unauthorized changes. Review and monitor **federated authentication setups** regularly, ensuring federated identities are correctly scoped and governed.
* **Monitoring and Alerting**: Set up alerts for any changes in trust relationships. Track attempts to add or alter domain trust properties, and verify these against security policies. Use **Azure Identity Protection** to detect suspicious trust modifications that could indicate privilege escalation attempts.

### 4. **Valid Accounts**

**T1078 - Valid Accounts**

* **Defensive Strategy**: Disable unused or default accounts and enforce **strong password policies** with MFA on all accounts. Limit the exposure of login interfaces and use **Conditional Access** to require MFA, particularly for privileged roles.
* **Monitoring and Alerting**: Log failed and successful login attempts for all accounts. Review logs to identify any default account logins, and monitor for excessive failed login attempts.

**T1078.001 - Default Accounts**

* **Defensive Strategy**: Remove or disable default accounts immediately after deployment and restrict access to sensitive resources. Conduct regular audits to ensure no default accounts remain active, especially on production systems.
* **Monitoring and Alerting**: Enable alerts for any activity involving default accounts and maintain logs for all default account usage. Flag and review any access from default accounts in high-security zones.

**T1556.003 - Cloud Accounts**

* **Defensive Strategy**: Implement **MFA and Conditional Access** for all cloud accounts and enforce password rotation policies. Utilize Azure AD Identity Protection to monitor for risky sign-ins and enforce strict authentication requirements.
* **Monitoring and Alerting**: Enable alerts for risky login behavior such as login attempts from unusual locations or new devices. Use Azure Security Center to monitor and respond to potential brute-force or phishing attempts targeting cloud accounts.



### **1. Enforce Least Privilege Access**

**Mitigates:** T1078 - Valid Accounts, T1098 - Account Manipulation

* **Action:** Ensure that **users, service principals, and automation accounts** have only the minimum permissions necessary to perform their tasks.
* **Azure Solution:**
  * Use **Role-Based Access Control (RBAC)** to limit roles.
  * Regularly review permissions using **Azure Privileged Identity Management (PIM)**.

### **2. Monitor Role Assignments and Privileged Access**

**Mitigates:** T1098 - Account Manipulation, T1106 - Native API

* **Action:** Continuously monitor **role changes and assignments**, especially privileged roles like "Global Administrator" or "Owner."
* **Azure Solution:**
  * Use **Azure AD PIM** to detect role elevation attempts.
  * Set alerts in **Azure Monitor** for any changes to RBAC roles or new role assignments.
  * Implement **just-in-time (JIT) access** for administrative roles.

### **3. Implement Multi-Factor Authentication (MFA)**

**Mitigates:** T1078.004 - Cloud Accounts, T1134 - Access Token Manipulation

* **Action:** Require **MFA** for all users and service principals, especially for privileged accounts.
* **Azure Solution:**
  * Enforce **MFA with Conditional Access Policies**.
  * Use **Azure AD Identity Protection** to detect and block suspicious logins.

### **4. Secure Service Principals and Automation Accounts**

**Mitigates:** T1098.001 - Additional Cloud Credentials, T1574.007 - Service Hijacking

* **Action:** Protect automation accounts, service principals, and their credentials to prevent misuse.
* **Azure Solution:**
  * Rotate service principal keys regularly.
  * Monitor for unauthorized creation of new credentials using **Azure Policy** and **Azure Defender**.
  * Ensure **runbooks** in **Azure Automation Accounts** only perform authorized tasks.

### **5. Harden Virtual Machines Against Privilege Escalation**

**Mitigates:** T1068 - Exploitation for Privilege Escalation

* **Action:** Apply the **latest security patches** to VMs and use security baselines to prevent exploitation.
* **Azure Solution:**
  * Use **Azure Update Management** to ensure all VMs are patched.
  * Enable **Azure Defender for VMs** to detect vulnerabilities.
  * Disable unnecessary admin accounts and enforce **SSH key-only authentication** for Linux VMs.

### **6. Monitor and Protect APIs**

**Mitigates:** T1106 - Native API

* **Action:** Track and control **API calls** that modify roles or sensitive resources.
* **Azure Solution:**
  * Use **Azure Monitor** and **Azure Sentinel** to detect suspicious API calls.
  * Enable **activity logging** to track role changes through the **Azure REST API**.
  * Configure alerts for **unexpected API requests** related to RBAC.

### **7. Detect and Respond to Privilege Escalation Attempts**

**Mitigates:** T1134 - Access Token Manipulation, T1548 - Abuse Elevation Control Mechanism

* **Action:** Monitor **logs and anomalies** to detect unusual privilege escalation attempts.
* **Azure Solution:**
  * Use **Azure Sentinel** to monitor for anomalies, such as:
    * Sudden assignment of high-level roles.
    * Automation runbooks creating new admin accounts.
    * Suspicious OAuth token usage.
  * Set up automated responses to **disable compromised accounts**.

### **8. Use Conditional Access Policies to Limit Risky Access**

**Mitigates:** T1078.002 - Domain Accounts, T1078.004 - Cloud Accounts

* **Action:** Restrict access to Azure resources based on device compliance, IP addresses, and risk levels.
* **Azure Solution:**
  * Configure **Conditional Access Policies** to block access from untrusted IPs and devices.
  * Use **Identity Protection** to enforce stricter policies for high-risk accounts.

### **9. Disable Unused or Risky Features**

**Mitigates:** T1548 - Abuse Elevation Control Mechanism

* **Action:** Disable **dangerous services or features** that are not required.
* **Azure Solution:**
  * Disable **RunCommand** on VMs if not needed.
  * Disable legacy authentication protocols (e.g., Basic Authentication) that may facilitate token abuse.

### **10. Regularly Audit Cloud Configurations and Logs**

**Mitigates:** T1098.001 - Additional Cloud Credentials, T1199 - Trusted Relationship

* **Action:** Continuously audit **Azure configurations and user activity** to detect misconfigurations or unauthorized role changes.
* **Azure Solution:**
  * Use **Azure Policy** to enforce security best practices.
  * Enable **Audit Logs** in Azure AD and monitor them with **Azure Monitor**.
  * Conduct regular **security posture assessments** with **Azure Security Center**.

### **Summary of Defensive Measures for TA0004**

| **Defensive Strategy**                      | **Mitigates**                                 | **Azure Solution**                                     |
| ------------------------------------------- | --------------------------------------------- | ------------------------------------------------------ |
| Enforce Least Privilege Access              | T1078 - Valid Accounts                        | Use RBAC and PIM to limit access                       |
| Monitor Role Assignments                    | T1098 - Account Manipulation                  | Use Azure Monitor and alerts for RBAC changes          |
| Implement Multi-Factor Authentication (MFA) | T1134 - Access Token Manipulation             | Enforce MFA via Conditional Access                     |
| Secure Service Principals and Accounts      | T1098.001 - Additional Cloud Credentials      | Rotate keys and monitor service principals             |
| Patch and Harden VMs                        | T1068 - Exploitation for Privilege Escalation | Use Update Management and Defender for VMs             |
| Monitor APIs for Misuse                     | T1106 - Native API                            | Use Azure Sentinel to detect API-based privilege abuse |
| Detect and Respond to Escalation Attempts   | T1548 - Abuse Elevation Control Mechanism     | Use Sentinel and automated responses                   |
| Use Conditional Access Policies             | T1078.002 - Domain Accounts                   | Block access from untrusted sources                    |
| Disable Unused Services                     | T1548 - Abuse Elevation Control Mechanism     | Disable RunCommand and legacy authentication           |
| Audit Configurations and Logs               | T1199 - Trusted Relationship                  | Use Azure Policy and Security Center for assessments   |
