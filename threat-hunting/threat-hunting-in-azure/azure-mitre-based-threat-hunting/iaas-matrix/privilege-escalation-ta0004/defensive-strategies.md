# Defensive Strategies

## Overview:

Defending against privilege escalation in Azure involves enforcing least privilege with Role-Based Access Control (RBAC), using Privileged Identity Management (PIM) for just-in-time access, and regularly auditing permissions. Enable logging for role assignments and sign-ins and monitor activities with Azure Sentinel and Defender for Cloud to detect anomalies. Secure sensitive resources like Key Vault and Automation Accounts with managed identities, conditional access, and private endpoints. These measures, combined with automated threat detection and response, effectively mitigate privilege escalation risks. Let's take a look at defensive strategies for each technique.&#x20;

### **T1548 - Abuse Elevation Control Mechanism**

1. **Defensive Strategies for Temporary Elevated Cloud Access**

* Enforce Managed Identity Scopes: Restrict the permissions of Managed Identities to the minimum required for their operation by defining explicit scopes in Azure Role-Based Access Control (RBAC).
* Enable Privileged Identity Management (PIM): Use Azure Entra PIM to enforce just-in-time (JIT) access for elevated roles, ensuring that temporary access is time-bound and auditable.
* Monitor Token Usage: Use Azure Monitor and Microsoft Defender for Cloud to detect anomalous API calls or unexpected activity tied to Managed Identities.

### **T1098 - Account Manipulation**

1. **Defensive Strategies for Additional Cloud Credentials**

* Restrict Application Secret Lifetime: Use short-lived application secrets and regularly rotate them using Azure Key Vault's Managed Secret Rotation feature.
* Monitor Service Principal Actions: Enable logging of Azure Entra ID service principal activities via Azure AD Audit Logs to identify unauthorized credential creation.
* Leverage Conditional Access Policies: Restrict access to specific IP ranges, device compliance, or risk-based criteria for service principal logins.

2. **Defensive Strategies for Additional Cloud Roles**

* Enforce RBAC Least Privilege: Regularly review and restrict roles at the subscription, resource group, or resource level to only those absolutely necessary.
* Enable Role Change Alerts: Configure Azure Monitor to trigger alerts on changes to high-privilege roles (e.g., assignments to the Owner or Contributor role).

3. **Defense Strategies for SSH Authorized Keys**

* Disable Password-Based Authentication: Use Azure Policy to enforce key-based authentication for all Linux VMs. Explore Azure Bastion.
* Monitor VM Activity: Use Azure Monitor to audit deployments of VM extensions and configurations, which could be used to modify SSH keys.

### **T1546 - Event-Triggered Execution**

1. **Defensive Strategies for Event-Triggered Execution**

* Restrict Function Triggers: Use Azure Role Assignments and Policies to control which users or services can configure Azure Function triggers.
* Monitor Automation Accounts: Enable logging for Azure Automation Runbooks via Azure Monitor and Log Analytics, and review all automation account actions regularly.
* Implement Secure Deployment Pipelines: Use Azure DevOps or GitHub Actions with deployment gates to prevent unauthorized changes to Function Apps or Automation Runbooks.

### **T1078 - Valid Accounts**

1. **Defensive Strategies for Valid Accounts**

* Enable Azure Entra Identity Protection: Detect and respond to leaked credentials and suspicious login activity, such as logins from unexpected locations or devices.
* Require Multi-Factor Authentication (MFA): Enforce MFA for all user accounts, including administrators, through Conditional Access policies.
* Review Access Logs: Use Azure Entra Sign-In Logs to regularly review account activities and detect anomalies.

2. **Defense Strategies for Default Accounts**

* Secure Default VM Accounts: Enforce strong password policies and disable default local admin accounts where possible. Use Azure Policy to audit and remediate insecure VM configurations.
* Monitor VM Baseline Configurations: Use Azure Defender to detect deviations from expected configurations, such as enabling default credentials.

3. **Defensive Strategies for Cloud Accounts**

* Review Service Principal Permissions: Regularly audit service principal permissions and remove unnecessary or high-privilege roles.
* Enable Key Vault Logging: Use Azure Key Vault’s logging and monitoring capabilities to track access to secrets, certificates, and keys.
* Implement Just-In-Time (JIT) Access: Restrict access to sensitive accounts and resources using Azure AD PIM with time-bound access approval workflows.

### General Guidance Across Techniques

The following are the key takeaways that you can deploy within your environment into order to prevent and or detection this tactic being used within your environment.&#x20;

* Centralize Logging: Aggregate logs from Azure AD, Azure Monitor, and Log Analytics into a single workspace for real-time analysis.
* Leverage Microsoft Defender for Cloud: Enable advanced threat detection and automated response for Azure resources.
* Conduct Regular Security Reviews: Periodically review resource configurations, role assignments, and conditional access policies for gaps in security posture.
* Simulate Attacks: Regularly perform red teaming and threat simulations using tools like Microsoft’s Security Stack or third-party solutions to validate defenses.
