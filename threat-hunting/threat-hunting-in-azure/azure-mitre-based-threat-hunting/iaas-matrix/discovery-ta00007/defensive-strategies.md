# Defensive Strategies

### **🔎 Account Discovery (T1087)**

Attackers try to enumerate **users, groups, and permissions**.

#### **🛡 Defensive Strategies for T1087.004 – Cloud Account Discovery**

✅ **Monitor Azure AD Logs**:

* Use **Azure AD Sign-in Logs** and **Audit Logs** to detect mass enumeration.
*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAuditLogs 
    | where OperationName == "List Users"
    ```

✅ **Restrict Directory Read Permissions**:

* Apply **least privilege principle (RBAC)** to limit who can execute `az ad user list`.

✅ **Enable Conditional Access**:

* Require **Multi-Factor Authentication (MFA)** for all admin-level users.

✅ **Monitor Unusual API Calls**:

* Detect excessive `Get-AzureADUser` or `az ad user list` calls.

***

### **🔎 Cloud Infrastructure Discovery (T1580)**

Attackers try to enumerate **virtual machines, databases, and cloud resources**.

#### **🛡 Defensive Strategies for T1580**

✅ **Enable Azure Security Center (Defender for Cloud)**:

* Use **Defender for Cloud** to flag suspicious API queries.

✅ **Monitor for Excessive Resource Enumeration**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAzureActivity
    | where OperationName contains "List" and ActivityStatus == "Succeeded"
    ```

✅ **Use Role-Based Access Control (RBAC)**:

* Limit `Reader` role to trusted accounts.

✅ **Enable Logging for Azure Resource Manager (ARM)**:

* Store **Azure Activity Logs** for forensic analysis.

***

### **🔎 Cloud Service Dashboard (T1590.001)**

Attackers may log into **portal.azure.com** to manually browse resources.

#### **🛡 Defensive Strategies for T1590.001**

✅ **Enable Multi-Factor Authentication (MFA)**:

* Enforce MFA for all **Azure Portal logins**.

✅ **Use Conditional Access Policies**:

* Restrict logins based on **device compliance** and **geolocation**.

✅ **Monitor Azure Portal Access**:

* Detect **logins from new locations** or **unusual IP addresses**.

✅ **Use Azure AD Privileged Identity Management (PIM)**:

* Require **Just-in-Time (JIT) access** for high-privilege users.

***

### **🔎 Cloud Service Discovery (T1526)**

Attackers enumerate **available services and regions**.

#### **🛡 Defensive Strategies for T1526**

✅ **Monitor for Region Enumeration Attempts**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAzureActivity
    | where OperationName contains "List Locations"
    ```

✅ **Enforce Azure Policy**:

* Restrict resource deployments to **approved regions**.

✅ **Use Microsoft Defender for Cloud**:

* Detect unauthorized API calls.

✅ **Limit API Permissions**:

* Restrict `az account list-locations` to **admins only**.

***

### **🔎 Cloud Storage Object Discovery (T1613)**

Attackers scan for **publicly accessible storage blobs**.

#### **🛡 Defensive Strategies for T1613**

✅ **Disable Public Blob Access**:

*   Use **Azure Policy** to enforce private access:

    ```json
    jsonCopyEdit{
      "if": {
        "field": "Microsoft.Storage/storageAccounts/publicNetworkAccess",
        "equals": "Enabled"
      },
      "then": {
        "effect": "Deny"
      }
    }
    ```

✅ **Enable Storage Logging**:

* Use **Azure Storage Analytics** to track blob access.

✅ **Monitor Blob Access**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditStorageBlobLogs
    | where OperationName contains "List Blobs"
    ```

***

### **🔎 Log Enumeration (T1005)**

Attackers attempt to access **Azure logs**.

#### **🛡 Defensive Strategies for T1005**

✅ **Restrict Access to Logs**:

* Limit `az monitor activity-log list` permissions.

✅ **Use Immutable Logging**:

* Enable **log retention** and **immutability policies**.

✅ **Monitor for Unusual Log Access**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAzureActivity
    | where OperationName contains "Read Logs"
    ```

***

### **🔎 Network Service Discovery (T1046)**

Attackers scan **Azure virtual networks** and **Network Security Groups (NSGs)**.

#### **🛡 Defensive Strategies for T1046**

✅ **Enable Just-In-Time (JIT) VM Access**:

* Prevent unauthorized scanning by restricting SSH/RDP access.

✅ **Use Azure Sentinel to Detect Scanning**:

*   KQL Query for detecting port scanning:

    ```kusto
    kustoCopyEditAzureNetworkAnalytics_CL
    | where TimeGenerated > ago(1h) and Message contains "port scan detected"
    ```

✅ **Harden Network Security Groups (NSGs)**:

* Restrict **SSH (22) and RDP (3389)** to trusted IPs.

✅ **Enable Azure DDoS Protection**:

* Detect and block **large-scale scans**.

***

### **🔎 Network Sniffing (T1040)**

If attackers compromise a **VM**, they may use **packet sniffing tools**.

#### **🛡 Defensive Strategies for T1040**

✅ **Disable Packet Capture on VMs**:

* Use **NSGs to block promiscuous mode**.

✅ **Deploy Microsoft Defender for Endpoint on VMs**:

* Detect tools like `tcpdump` and `Wireshark`.

✅ **Monitor for Unusual Network Traffic**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAzureNetworkAnalytics_CL
    | where Message contains "Unusual Traffic Pattern"
    ```

***

### **🔎 Password Policy Discovery (T1201)**

Attackers try to discover **password policies**.

#### **🛡 Defensive Strategies for T1201**

✅ **Use Azure AD Password Protection**:

* Block **common passwords** and enable **Smart Lockout**.

✅ **Monitor for Password Policy Queries**:

* Detect `Get-MsolPasswordPolicy` calls.

✅ **Enforce Strong Password Requirements**:

* Require **14+ character passwords with MFA**.

***

### **🔎 Permission Groups Discovery (T1069.003)**

Attackers enumerate **Azure AD groups**.

#### **🛡 Defensive Strategies for T1069.003**

✅ **Monitor Group Enumeration**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAuditLogs 
    | where OperationName == "List Groups"
    ```

✅ **Use Privileged Identity Management (PIM)**:

* Require **JIT activation** for admin roles.

✅ **Restrict Group Enumeration Permissions**:

* Remove unnecessary `Directory Readers` permissions.

***

### **🔎 Software Discovery (T1518)**

Attackers investigate **security software and system configurations**.

#### **🛡 Defensive Strategies for T1518**

✅ **Monitor for Security Software Enumeration**:

*   KQL Query for Sentinel:

    ```kusto
    kustoCopyEditAzureActivity
    | where OperationName contains "List Security Solutions"
    ```

✅ **Restrict API Access to Security Tools**:

* Limit `az security setting list` permissions.

✅ **Use Defender for Cloud**:

* Detect attempts to disable security tools.
