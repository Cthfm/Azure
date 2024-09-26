# Azure Log Types

## **Overview:**

The following section provides a list of the common log types that are utilized within Azure for security and threat hunting.&#x20;

### Log Types:

#### 1. **Azure Activity Logs**

* **Purpose**: Records all management operations performed on resources within your Azure subscription.
* **Use Cases**:
  * **Monitor Administrative Actions**: Track who made changes to critical resources, such as network security groups, virtual machines, or identity configurations.
  * **Detect Unauthorized Access**: Identify suspicious administrative actions, like creating new users, granting roles, or disabling security features.

#### 2. **Azure Entra ID Logs**

* **Sign-in Logs**:
  * **Purpose**: Logs all sign-in activities within Azure AD.
  * **Use Cases**:
    * **Identify Suspicious Logins**: Look for sign-ins from unfamiliar locations, impossible travel scenarios, or sign-ins using legacy authentication protocols.
    * **Compromised Accounts**: Detect anomalies in user sign-in behavior, such as repeated failed attempts or unusual login times.
* **Audit Logs**:
  * **Purpose**: Provides a record of all changes made within Azure AD, including changes to users, groups, applications, and directory settings.
  * **Use Cases**:
    * **Detect Changes to Privileged Roles**: Monitor changes to roles that could grant elevated permissions.
    * **Track Directory Changes**: Watch for unusual modifications, such as adding a new application or changing group memberships.

#### 3. **Azure Security Center (Defender for Cloud) Alerts and Logs**

* **Purpose**: Provides a unified view of security alerts and recommendations across your Azure environment.
* **Use Cases**:
  * **Detect Threats**: Review alerts for potential threats, such as detected malware, unauthorized access attempts, or risky configurations.
  * **Remediation Tracking**: Track how security recommendations are being addressed and whether security configurations are improving over time.

#### 4. **Azure Resource Logs (formerly Diagnostic Logs)**

* **Purpose**: Logs generated by Azure resources, such as virtual machines, application gateways, and databases.
* **Use Cases**:
  * **Monitor VM Activity**: Analyze logs from Azure VMs to detect unusual activity like high CPU usage, unexpected processes, or unauthorized access.
  * **Web Application Firewall (WAF) Logs**: Investigate logs from Application Gateways to detect and analyze potential web attacks, like SQL injections or cross-site scripting (XSS) attempts.

#### 5. **Azure Key Vault Logs**

* **Purpose**: Tracks access and usage of Azure Key Vaults, where sensitive information such as encryption keys and secrets are stored.
* **Use Cases**:
  * **Monitor Access to Secrets**: Look for unauthorized access attempts or unusual patterns of access to critical secrets or keys.
  * **Audit Key Usage**: Ensure that encryption keys are being used according to policy and that no suspicious activities are occurring, such as key deletions or unauthorized exports.

#### 6. **Azure Network Watcher Logs**

* **Flow Logs**:
  * **Purpose**: Captures network traffic flowing in and out of network security groups (NSGs).
  * **Use Cases**:
    * **Analyze Traffic Patterns**: Detect anomalies in traffic, such as unexpected IP addresses communicating with your environment, or unusual port usage.
    * **Identify Malicious Traffic**: Look for signs of data exfiltration, lateral movement, or communication with known bad IP addresses.
* **Next Hop and Connection Troubleshoot**:
  * **Purpose**: Helps identify and troubleshoot network issues.
  * **Use Cases**:
    * **Trace Suspicious Network Activity**: Use these logs to trace the path of suspicious traffic and identify potential breaches in network security.



7\. **Azure Storage Logs**

* **Purpose**: Captures data related to access and operations on Azure storage accounts, including Blob, Queue, Table, and File storage.
* **Use Cases**:
  * **Monitor Access to Sensitive Data**: Track who accessed specific storage containers or files, especially those containing sensitive data.
  * **Detect Anomalies in Data Access**: Identify unusual patterns in data access, such as large data downloads or access from unexpected locations.

#### 9. **Azure SQL Database Logs**

* **Purpose**: Logs related to Azure SQL Database activities, including database connections, query execution, and security events.
* **Use Cases**:
  * **Database Access Monitoring**: Identify unauthorized or suspicious access to databases.
  * **SQL Injection Detection**: Analyze query logs for patterns indicative of SQL injection attacks or other database-related threats.


