# Defensive Strategies

## **Overview:**

The following provides a list of strategies for defending against the techniques and sub techniques identified within TA0001.&#x20;

### **Exploit Public-Facing Application (T1190)**

**Defense Strategies:**

1. **Secure Application Development:**
   * Implement secure coding practices (e.g., input validation, parameterized queries).
   * Conduct regular code reviews and static/dynamic application testing.
2. **Web Application Firewall (WAF):**
   * Use WAFs like Azure WAF to detect and block exploitation attempts.
3. **Patching and Updates:**
   * Regularly patch operating systems, frameworks, and third-party dependencies.
4. **Access Control:**
   * Restrict access to public-facing applications using Azure NSGs and Azure AD App Proxy.
5. **Monitoring and Alerts:**
   * Monitor application logs for suspicious activity with Azure Monitor and Application Insights.

### **Trusted Relationship (T1199)**

**Defense Strategies:**

1. **Third-Party Risk Management:**
   * Perform security audits and risk assessments of vendors and partners.
   * Limit access for third-party providers to only what is necessary.
2. **Conditional Access:**
   * Enforce Azure AD Conditional Access policies for external accounts and federated users.
3. **Logging and Monitoring:**
   * Enable logging for all delegated administrator actions in Office 365 or Azure AD.
   * Use Azure Sentinel to monitor and detect anomalies in trusted relationships.
4. **Privilege Management:**
   * Regularly review and reduce delegated permissions for third-party entities.
   * Rotate credentials and enforce MFA for all external accounts.
5. **Incident Response:**
   * Create playbooks to handle compromised third-party accounts or abused trust relationships.
6. **Robust Monitoring**
   * Ensure that third party accounts are monitored for any unauthorized activity.&#x20;

### **Valid Accounts (T1078)**

**Default Accounts (T1078.001)**

**Defense Strategies:**

1. **Disable Default Accounts:**
   * Immediately disable or rename default accounts after provisioning new resources.
2. **Strong Authentication:**
   * Enforce complex passwords and MFA for accounts that cannot be disabled.
3. **Configuration Management:**
   * Use Azure Policy to ensure resources are deployed with hardened settings.
4. **Access Auditing:**
   * Regularly audit login attempts and access patterns for default accounts.

**Cloud Accounts (T1078.004)**

**Defense Strategies:**

1. **Credential Management:**
   * Store secrets, tokens, and API keys in Azure Key Vault with strict access policies.
2. **Role-Based Access Control (RBAC):**
   * Enforce least privilege by assigning minimal roles to cloud accounts.
3. **Logging and Monitoring:**
   * Use Azure Activity Logs and Azure Monitor to track access patterns.
4. **Automated Key Rotation:**
   * Implement automated key rotation policies for service accounts and applications.
5. **Zero Trust Architecture:**
   * Use conditional access policies to validate the context of logins.
6. Invest in Identity Protection or Microsoft Defender
   * Utilize Azure Entra Identity Protection and Defender  to detect anomalous behaviors.&#x20;
7. Consider token protections
   * Consider token protection like CAE and Token Protection: Conditional Access
