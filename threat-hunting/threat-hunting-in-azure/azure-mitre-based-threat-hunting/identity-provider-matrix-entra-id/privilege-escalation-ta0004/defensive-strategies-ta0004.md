# Defensive Strategies: TA0004

## **Defensive Strategies for TA0004 - Privilege Escalation**

Defending against Privilege Escalation in Azure environments requires tight access control, role monitoring, automation security, and detection mechanisms. Below are key defensive measures mapped to relevant techniques, along with Azure-specific tools and configurations to mitigate these risks.

## 1. **Abuse Elevation Control Mechanism**

**Technique: T1548 - Abuse Elevation Control Mechanism**\
Attackers circumvent systems that are designed to elevate a principal's access and gain higher privileges.

**T1548.005 - Temporary Elevated Cloud Access**

* **Defensive Strategy**: Enforce Conditional Access Policies to restrict and log elevated access, limiting the duration and scope of temporary roles. Ensure that time-limited permissions are appropriately configured, with strict criteria for access and expiry.
* **Monitoring and Alerting**: Enable Azure Monitor alerts for changes in JIT and PIM configurations and review for any unexpected approvals. Investigate any PIM assignments that are extended or overridden without proper authorization.

### 2. **Account Manipulation**

**Technique: T1098 - Account Manipulation**

Attackers may manipulate accounts to maintain or elevate access to victim systems. This may involve actions like modifying credentials or permission groups to retain control. Attackers might also subvert security policies, such as repeatedly updating passwords to bypass duration policies and extend compromised access.

**T1098.001 - Additional Cloud Credentials**

* **Defensive Strategy**: Disable SAS Token generation when possible and use RBAC instead. Otherwise ensure SAS token generation permissions and enforce short token expiration times (hours, not days).&#x20;
* **Monitoring and Alerting**: Enable alerts for SAS token generation and audit all generated tokens for unusual permissions or extended expiration periods. Ensure to isolate SAS token creation to specific set of users. Monitor OAuth Application credentials and review changes to App Registration settings for additional credentials.

**T1098.003 - Additional Cloud Roles**

* **Defensive Strategy**: Limit role assignmen**t** creation permissions and monitor ‘Contributor’ and other high-privilege role assignments to ensure they align with documented needs. Implement least-privilege roles using Role-Based Access Control (RBAC).
* **Monitoring and Alerting**: Set alerts **for new role assignments, es**pecially ‘Contributor’ or higher roles in sensitive resource groups or subscriptions. Regularly review RBAC assignments, logging changes in Azure Entra ID Privileged Role Administrator roles.

**T1098.005 - Registered Device**

* **Defensive Strategy**: Secure Intune and other device management policies with strict approval workflows. Restrict device registration to prevent unauthorized device enrollment. Implement compliance policies in Intune to ensure only secure devices can access resources.
* **Monitoring and Alerting**: Monitor Intune policy changes and log device registration activity for unusual devices. Use Conditional Access to block or require additional verification for newly registered devices.

### 3. **Domain or Tenant Policy Modification**

**Technique: T1484 - Abuse Elevation Control Mechanism**\
Attackers exploit privileged automation tools to run high-level tasks.

**T1484.002 - Trust Modification**

* **Defensive Strategy**: Enforce strict trust modification policies and limit access to tenant federation settings to prevent unauthorized changes. Review and monitor federated authentication setups regularly, ensuring federated identities are correctly scoped and governed.
* **Monitoring and Alerting**: Set up alerts for any changes in trust relationships. Track attempts to add or alter domain trust properties and verify these against security policies. Use Azure Identity Protection to detect suspicious principal activity and the Activity log for any suspicious trust modifications that could indicate privilege escalation attempts.

### 4. **Valid Accounts**

**Technique:** T1078 **- Valid Accounts**\
Attackers may obtain and abuse credentials of existing accounts as a means of gaining

**T1078.001 - Default Accounts**

* **Defensive Strategy**: Remove or disable default accounts immediately after deployment and restrict access to sensitive resources. Conduct regular audits to ensure no default accounts remain active, especially on production systems.
* **Monitoring and Alerting**: Enable alerts for any activity involving default accounts and maintain logs for all default account usage. Flag and review any access from default accounts in high-security zones.

**T1556.003 - Cloud Accounts**

* **Defensive Strategy**: Implement MFA and Conditional Access for all cloud accounts and enforce password rotation policies. Utilize Azure AD Identity Protection to monitor for risky sign-ins and enforce strict authentication requirements.
* **Monitoring and Alerting**: Enable alerts for risky login behavior such as login attempts from unusual locations or new devices. Use Microsoft Defender for Cloud, Sentinel and or Defender XDR to monitor and respond to potential brute-force or phishing attempts targeting cloud accounts.

### **Summary of Defensive Measures for TA0004**

| **Defensive Strategy**                      | **Mitigates**                                 | **Azure Solution**                                     |
| ------------------------------------------- | --------------------------------------------- | ------------------------------------------------------ |
| Utilize JIT Access                          | T1548 - Abuse Elevation Control Mechanism     | Ensure JIT Access is configured for 'Manual' Approval, |
| Monitor Role Assignment                     | T1098 - Account Manipulation                  | Use Azure Monitor and alerts for RBAC changes          |
| Implement Multi-Factor Authentication (MFA) | T1134 - Access Token Manipulation             | Enforce MFA via Conditional Access                     |
| Secure Service Principals and Accounts      | T1098.001 - Additional Cloud Credentials      | Rotate keys and monitor service principals             |
| Patch and Harden VMs                        | T1068 - Exploitation for Privilege Escalation | Use Update Management and Defender for VMs             |
| Monitor APIs for Misuse                     | T1106 - Native API                            | Use Azure Sentinel to detect API-based privilege abuse |
| Detect and Respond to Escalation Attempts   | T1548 - Abuse Elevation Control Mechanism     | Use Sentinel and automated responses                   |
| Use Conditional Access Policies             | T1078.002 - Domain Accounts                   | Block access from untrusted sources                    |
| Disable Unused Services                     | T1548 - Abuse Elevation Control Mechanism     | Disable RunCommand and legacy authentication           |
| Audit Configurations and Logs               | T1199 - Trusted Relationship                  | Use Azure Policy and Security Center for assessments   |
