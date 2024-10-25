# Defensive Strategies: TA0004

## **Defensive Strategies for TA0004 - Privilege Escalation**

Defending against **Privilege Escalation** in **Azure environments** requires **tight access control, role monitoring, automation security, and detection mechanisms**. Below are key **defensive measures mapped to relevant techniques**, along with **Azure-specific tools and configurations** to mitigate these risks.

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
