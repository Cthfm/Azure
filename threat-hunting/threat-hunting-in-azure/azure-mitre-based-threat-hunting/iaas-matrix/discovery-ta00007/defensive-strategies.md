# Defensive Strategies

### **Account Discovery (T1087)**

Attackers try to enumerate users, groups, and permissions.

#### **Defensive Strategies for T1087.004 – Cloud Account Discovery**

1. **Monitor Azure AD Logs**: Use Azure AD Sign-in Logs and Audit Logs to detect mass enumeration.
2. **Restrict Directory Read Permissions**: Apply least privilege principle (RBAC) to limit who can execute az ad user list.
3. **Enable Conditional Access**: Require Multi-Factor Authentication (MFA) for all admin-level users.
4. **Monitor Unusual API Calls**: Detect excessive az ad user list and Get-EntraGroup calls.&#x20;
5. **Monitor Azure Activity Logs:** Look for excessive list directory operations.&#x20;
6. **Enable role-based access control (RBAC):** Use RBAC to restrict API calls.

### **Cloud Infrastructure Discovery (T1580)**

Attackers try to enumerate virtual machines, databases, and cloud resources.

#### **Defensive Strategies for T1580**

1. **Enable Azure Security Center (Defender for Cloud)**: Use **Defender for Cloud** to flag suspicious API queries.
2. **Monitor for Excessive Resource Enumeration**: Use AzureActivity log to look for large number of list requests.&#x20;
3. **Use Role-Based Access Control (RBAC)**: Limit `Reader` role to trusted accounts.
4. **Enable Logging for Azure Resource Manager (ARM)**: Store Azure Activity Logs for forensic analysis.
5. **Enable Azure AD Conditional Access:** Use to detect unauthorized API queries.
6. **Use Microsoft Defender for Cloud and Activity Log:** Use the logs to detect infrastructure enumeration.

### **Cloud Service Dashboard (T1590.001)**

Attackers may log into portal.azure.com to manually browse resources.

#### **Defensive Strategies for T1590.001**

1. **Enable Multi-Factor Authentication (MFA)**: Enforce MFA for all Azure Portal logins.
2. &#x20;**Use Conditional Access Policies**: Restrict logins based on device compliance and geolocation.
3. &#x20;**Monitor Azure Portal Access**: Detect logins from new locations or unusual IP addresses.
4. **Use Azure AD Privileged Identity Management (PIM)**: Require Just-in-Time (JIT) access for high-privilege users.

### **Cloud Service Discovery (T1526)**

Attackers enumerate available services and regions.

#### **Defensive Strategies for T1526**

1. **Monitor for Region Enumeration Attempts**: Review Azure Activity log for any calls Azure Account list location calls.&#x20;
2. **Enforce Azure Policy**: Restrict resource deployments to approved regions.
3. **Use Microsoft Defender for Cloud**: Detect unauthorized API calls.
4. **Limit API Permissions**: Restrict az account list-locations to only those that need to know where resources can be deployed.

### **Cloud Storage Object Discovery (T1613)**

Attackers scan for publicly accessible storage blobs.

#### **Defensive Strategies for T1613**

1. **Disable Public Blob Access**: Use Azure Policy to enforce private access:

```json
  "if": {
    "field": "Microsoft.Storage/storageAccounts/publicNetworkAccess",
    "equals": "Enabled"
  },
  "then": {
    "effect": "Deny"
  }
}
```

2. **Enable Storage Logging**: Use Azure Storage Analytics to track blob access.
3. &#x20;**Monitor Blob Access**: Monitor Storage Blob logs for multiple list calls.

### **Log Enumeration (T1005)**

Attackers attempt to access Azure logs.

#### **Defensive Strategies for T1005**

1\. **Restrict Access to Logs**: Limit az monitor activity-log list&#x20;

2\. **Use Immutable Logging**: Enable log retention and immutability policies.

3\. **Monitor for Unusual Log Access**: Monitor Azure Activity for unauthorized principals attempting to access or read logs.&#x20;

### **Network Service Discovery (T1046)**

Attackers scan Azure virtual networks and Network Security Groups (NSGs).

#### **Defensive Strategies for T1046**

1\. **Enable Just-In-Time (JIT) VM Access**: Prevent unauthorized scanning by restricting SSH/RDP access.

2\. **Use Azure Sentinel to Detect Scanning**: Integrate with Azure Firewall to obtain detections for malicious port scanning activity.&#x20;

3. **Harden Network Security Groups (NSGs)**: Restrict SSH (22) and RDP (3389) to trusted IPs. Use least priviledge for port and IP usage.

### **Network Sniffing (T1040)**

If attackers compromise a VM, they may use packet sniffing tools.

#### **Defensive Strategies for T1040**

1. **Disable Packet Capture on VMs**: Use NSGs to block promiscuous mode.
2. **Deploy Microsoft Defender for Endpoint on VMs**: Detect tools like tcpdump and wireshark (may have authorized uses in some cases).&#x20;
3. **Monitor for Unusual Network Traffic**: Review NetFlow and resource group logs for unusual traffic.

### **Password Policy Discovery (T1201)**

Attackers try to discover password policies.

#### **Defensive Strategies for T1201**

1. **Use Azure Entra ID Password Protection**: Block common passwords and enable Smart Lockout.
2. **Monitor for Password Policy Queries**: Detect whenever Get-MsolPasswordPolicy is called from unauthorized principals.
3. **Enforce Strong Password Requirements**: Require 14+ character passwords with MFA.

### **Permission Groups Discovery (T1069.003)**

Attackers enumerate Azure Entra ID Groups.

#### **Defensive Strategies for T1069.003**

1. **Monitor Group Enumeration**: Check the Azure Activity logs for large group of list group calls.&#x20;
2. **Use Privileged Identity Management (PIM)**: Require JIT activation for admin roles.
3. **Restrict Group Enumeration Permissions**: Remove unnecessary Directory Readers permissions.

### **Software Discovery (T1518)**

Attackers investigate security software and system configurations.

#### **Defensive Strategies for T1518**

1. **Monitor for Security Software Enumeration**: Check logging for any signs of users attempting to enumerate existing software on their devices.&#x20;
2. **Restrict API Access to Security Tools**: Limit az security setting list for providing any information to unauthorized principals.&#x20;
3. **Use Defender for Cloud and Azure Activity Logs**: Detect attempts to disable security tools.
