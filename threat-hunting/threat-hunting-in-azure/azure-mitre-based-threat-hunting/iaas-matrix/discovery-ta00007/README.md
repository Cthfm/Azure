---
hidden: true
---

# Discovery TA00007

### **🔎 Account Discovery (T1087)**

Attackers attempt to enumerate **users, groups, and permissions** to understand the access hierarchy in an **Azure** environment.

#### **🛠 T1087.004 – Cloud Account Discovery**

* **Example Attack:**
  *   Using **Azure CLI** to list user accounts:

      ```powershell
      powershellCopyEditaz ad user list --query "[].{Name:displayName, UserPrincipalName:userPrincipalName}"
      ```
  *   **PowerShell Alternative:**

      ```powershell
      powershellCopyEditGet-AzureADUser -All $true
      ```
* **Detection & Mitigation:**\
  ✅ Monitor **Azure AD Sign-in logs** for excessive `List Directory` operations.\
  ✅ Enable **role-based access control (RBAC)** to restrict API calls.

***

### **🔎 Cloud Infrastructure Discovery (T1580)**

Attackers attempt to identify virtual machines, databases, and cloud resources in an **Azure subscription**.

* **Example Attack:**
  *   Using Azure CLI:

      ```powershell
      powershellCopyEditaz resource list --query "[].{Name:name, Type:type}"
      ```
  *   **PowerShell Alternative:**

      ```powershell
      powershellCopyEditGet-AzResource | Select-Object Name, ResourceType
      ```
* **Detection & Mitigation:**\
  ✅ Enable **Azure AD Conditional Access** to detect **unauthorized API queries**.\
  ✅ Use **Microsoft Defender for Cloud** to log infrastructure enumeration.

***

### **🔎 Cloud Service Dashboard (T1590.001)**

Attackers may **log into the Azure portal** (`portal.azure.com`) to manually browse resources.

* **Example Attack:**
  * Login with stolen credentials and browse **Resource Explorer**.
* **Detection & Mitigation:**\
  ✅ Enable **Multi-Factor Authentication (MFA)**.\
  ✅ Monitor for **suspicious IP addresses** logging into Azure Portal.

***

### **🔎 Cloud Service Discovery (T1526)**

Attackers enumerate available **Azure services and regions**.

* **Example Attack:**
  *   Identifying cloud regions:

      ```powershell
      powershellCopyEditaz account list-locations --query "[].{Region:name}"
      ```
* **Detection & Mitigation:**\
  ✅ **Limit API calls** to trusted users using **Azure Policy**.\
  ✅ Detect abnormal requests using **Azure Monitor**.

***

### **🔎 Cloud Storage Object Discovery (T1613)**

Attackers scan for **publicly accessible storage blobs**.

* **Example Attack:**
  *   Listing storage containers:

      ```powershell
      powershellCopyEditaz storage blob list --container-name mycontainer --account-name mystorage
      ```
* **Detection & Mitigation:**\
  ✅ **Disable public access** on storage accounts.\
  ✅ Use **Azure Security Center alerts** to flag unauthorized access.

***

### **🔎 Log Enumeration (T1005)**

Attackers attempt to access **Azure logs** to gather intel on security events.

* **Example Attack:**
  *   Retrieving logs from Azure Monitor:

      ```powershell
      powershellCopyEditaz monitor activity-log list --max-items 10
      ```
* **Detection & Mitigation:**\
  ✅ Use **Azure Log Analytics** to track unauthorized queries.\
  ✅ Restrict log access to **security teams only**.

***

### **🔎 Network Service Discovery (T1046)**

Attackers scan **Azure virtual networks (VNets)** and **Network Security Groups (NSGs)**.

* **Example Attack:**
  *   Checking network security rules:

      ```powershell
      powershellCopyEditaz network nsg rule list --resource-group MyResourceGroup --nsg-name MyNSG
      ```
  *   Performing internal network scanning:

      ```bash
      bashCopyEditnmap -p- -Pn -T4 <Target-IP>
      ```
* **Detection & Mitigation:**\
  ✅ Monitor network scanning activity using **Azure Sentinel**.\
  ✅ Implement **Just-in-Time (JIT) access** for VMs to block scanning.

***

### **🔎 Network Sniffing (T1040)**

If an attacker gains control of a **compromised Azure VM**, they might attempt **packet sniffing**.

* **Example Attack:**
  *   Running `tcpdump` to capture traffic:

      ```bash
      bashCopyEdittcpdump -i eth0 -w capture.pcap
      ```
* **Detection & Mitigation:**\
  ✅ Disable **packet capture permissions** on VMs.\
  ✅ Enable **Microsoft Defender for Endpoint** on all Azure VMs.

***

### **🔎 Password Policy Discovery (T1201)**

Attackers query **password policies** to plan credential attacks.

* **Example Attack:**
  *   Retrieving Azure AD password policy:

      ```powershell
      powershellCopyEditGet-MsolPasswordPolicy -DomainName mydomain.com
      ```
* **Detection & Mitigation:**\
  ✅ Enforce **Azure AD Password Protection** with banned passwords.\
  ✅ Detect excessive API calls for **password policy enumeration**.

***

### **🔎 Permission Groups Discovery (T1069)**

Attackers enumerate **Azure AD groups** to identify privileged accounts.

#### **🛠 T1069.003 – Cloud Groups Discovery**

* **Example Attack:**
  *   Listing Azure AD groups:

      ```powershell
      powershellCopyEditGet-AzureADGroup -All $true
      ```
  *   Checking role assignments:

      ```powershell
      powershellCopyEditaz role assignment list --query "[].{Role:roleDefinitionName, User:principalName}"
      ```
* **Detection & Mitigation:**\
  ✅ Monitor for **excessive group enumeration requests**.\
  ✅ Use **Privileged Identity Management (PIM)** to restrict group access.

***

### **🔎 Software Discovery (T1518)**

Attackers investigate **security software and system configurations**.

#### **🛠 T1518.001 – Security Software Discovery**

* **Example Attack:**
  *   Checking installed security solutions:

      ```powershell
      powershellCopyEditaz security setting list
      ```
* **Detection & Mitigation:**\
  ✅ Limit **security settings visibility** to admins.\
  ✅ Monitor **Azure API requests** for security configuration changes.

#### **🛠 T1518.002 – System Information Discovery**

* **Example Attack:**
  *   Gathering system details:

      ```powershell
      powershellCopyEditaz vm show --name myVM --resource-group myRG
      ```
* **Detection & Mitigation:**\
  ✅ Restrict access to **VM metadata services**.

#### **🛠 T1518.003 – System Location Discovery**

* **Example Attack:**
  *   Identifying VM locations:

      ```powershell
      powershellCopyEditaz account list-locations
      ```
* **Detection & Mitigation:**\
  ✅ Enforce **geo-based restrictions** using **Conditional Access policies**.

#### **🛠 T1518.004 – System Network Connections Discovery**

* **Example Attack:**
  *   Checking active network connections:

      ```powershell
      powershellCopyEditnetstat -ano
      ```
* **Detection & Mitigation:**\
  ✅ Use **Network Security Groups (NSGs)** to restrict outbound traffic.
