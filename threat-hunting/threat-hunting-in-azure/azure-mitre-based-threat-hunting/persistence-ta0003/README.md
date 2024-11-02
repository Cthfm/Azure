# Persistence: TA0003

## **Overview**

Persistence refers to how attackers ensure continued access to a system or cloud environment, even after reboots, password changes, or other defensive efforts. In Azure, attackers leverage tools such as automation services, identities, or misconfigurations to establish long-term control.

### **1. Account Manipulation**

**Technique: T1098 - Account Manipulation**\
Attackers may manipulate accounts to maintain and/or elevate access.

*   **T1098.001 - Add additional credentials**\
    Attacker creates additional set of credentials

    ```powershell
    $servicePrincipal = Get-AzADServicePrincipal -DisplayName <App_Name>
    Get-AzADApplication -ApplicationId <App_Id> | New-AzADAppCredential -StartDate 11/01/2024 -EndDate 11/01/222
    ```
*   **T1098.003 - Additional Cloud Roles**\
    Attacker creates additional roles with a compromised user

    ```powershell
    $userId = (Get-AzADUser -UserPrincipalName "compromised_user@example.com").Id $roleDefinition = Get-AzRoleDefinition -Name "Contributor"
    $roleDefinition = Get-AzRoleDefinition -Name "Contributor"

    New-AzRoleAssignment -ObjectId $userId -RoleDefinitionName $roleDefinition.Name -Scope "/subscriptions/<SubscriptionID>/ResourceGroups/CompanySecrets"
    ```
* **T1098.005 - Registered Device**\
  Attackers that already have initial access will modify existing Intune policies to register a rouge device.

### **2. Create an Account**

**Technique: T1136- Create Account**\
Attackers create an account to establish persistence within a tenant.

*   **T1136.003 - Cloud Account**\
    Attacker creates a user account within a given tenant

    ```bash
    az ad user create --display-name CTHFM_Persistence --password l33thax0rh3r3!nth3b4s3 --user-principal-name user@cthfm.onmicrosoft.com
    ```

### **3. Modify Authentication Process**

{% hint style="danger" %}
Microsoft is in the process of enforcing MFA across all of Azure by early 2025.  See link below for more details.[https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mandatory-multifactor-authentication](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mandatory-multifactor-authentication)
{% endhint %}

**Technique: T1556 - Modify Authentication Process**\
Attackers change authentication configurations and processes to access user credentials or enable otherwise unwarranted access to accounts.

* **T1556.006 - Multifactor Authentication**\
  Attacker either disables, modifies MFA configuration, to enable persistent access within an account.&#x20;
* **T1556.003 - Hybrid Identity**\
  Attackers can target the authentication process in hybrid identity environments to establish covert, persistent access across both cloud and on-premises resources.'

1. #### **Directly Modifying PTA Agents to Backdoor Authentication**

* **Pass-Through Authentication (PTA)** delegates authentication requests from Azure AD to on-premises Active Directory through a PTA agent. Compromising the PTA agent allows adversaries to intercept or manipulate authentication requests. Specifically:
  * **DLL Injection**: Attackers may inject a malicious DLL into the `AzureADConnectAuthenticationAgentService` on the PTA server. This backdoor approach could allow attackers to intercept credentials, authorize unauthorized access, or bypass MFA by manipulating the response that goes back to Entra ID.
  * **Credential Harvesting**: Injected code can intercept and log user credentials that pass through PTA for later misuse, enabling attackers to authenticate as any user​​.
* **AD FS (Active Directory Federation Services)** provides a federation link for single sign-on (SSO) between on-premises AD and cloud applications. Attackers targeting AD FS can modify configuration files, specifically:
  * **Microsoft.IdentityServer.Servicehost Configuration**: Editing the configuration file (`Microsoft.IdentityServer.Servicehost.exe.config`) to load a malicious DLL can create fake tokens with any claim, effectively bypassing MFA and gaining access to any cloud resources trusted by AD FS.
  * **Custom Claims Injection**: By manipulating claims, attackers could generate valid tokens for any user or even escalate privileges by granting extra permissions, making it challenging to detect their presence in cloud environments like AWS or GCP that also federate with AD FS​.

#### 3. **Modifying Authentication in Entra ID Directly from the Cloud**

* If an attacker compromises a Global Administrator account within Entra ID, they could bypass on-premises controls entirely by modifying Entra ID configurations directly:
  * **Registering Malicious PTA Agents**: An attacker with Global Admin privileges in Entra ID can register new PTA agents via the Azure portal. These rogue agents would relay credential information to the attacker or manipulate authentication attempts without needing further on-premises access.
  * **Creating and Exploiting Conditional Access Policies**: Modifying or creating Conditional Access policies can selectively enforce (or bypass) MFA and other controls, creating avenues for unmonitored and persistent access to sensitive resources​​.

### **3. Valid Accounts**

**Technique:** T1078 **- Valid Accounts**\
Attackers may obtain and abuse credentials of existing accounts as a means of gaining

* **T1078.001 - Default Accounts**\
  Attacker utilized default usernames and passwords in order to gain access to establish persistence.
* **T1556.003 - Cloud Accounts**\
  Attacker is able to compromise an account in order to get access. This can be done a myriad of ways that include phishing, brute forcing, and other mechanisms.&#x20;

### **Summary Techniques for TA0003**

<table><thead><tr><th>Key Concept</th><th width="214">Technique</th><th>Azure Example</th></tr></thead><tbody><tr><td>Account Manipulation</td><td>T1098 - Account Manipulation</td><td><strong>T1098.001 - Add Additional Credentials</strong>: Attacker creates additional credentials for persistence. Example: <code>$servicePrincipal = Get-AzADServicePrincipal -DisplayName &#x3C;App_Name></code><br>`Get-AzADApplication -ApplicationId &#x3C;App_Id></td></tr><tr><td>Create an Account</td><td>T1136 - Create Account</td><td><strong>T1136.003 - Cloud Account</strong>: Attacker creates a new user within Azure AD for persistence.<br>Example: <code>az ad user create --display-name CTHFM_Persistence --password l33thax0rh3r3!nth3b4s3 --user-principal-name user@cthfm.onmicrosoft.com</code></td></tr><tr><td>Modify Authentication Process</td><td>T1556 - Modify Authentication Process</td><td><strong>T1556.006 - Multifactor Authentication</strong>: Disable or alter MFA settings to maintain access.<br><br><strong>T1556.003 - Hybrid Identity</strong>: Attackers exploit PTA agent to intercept or manipulate credentials and bypass MFA through DLL injection or credential harvesting.<br><br>Example: Injecting a malicious DLL into <code>AzureADConnectAuthenticationAgentService</code> on PTA agent for credential logging.<br><br><strong>AD FS Manipulation</strong>: Modifying <code>Microsoft.IdentityServer.Servicehost.exe.config</code> to create backdoor tokens, allowing unrestricted cloud access.<br><br><strong>Direct Modifications from Entra ID</strong>: Attackers with Global Admin privileges may register rogue PTA agents or alter Conditional Access policies to selectively enforce or bypass MFA and other security controls.</td></tr><tr><td>Valid Accounts</td><td>T1078 - Valid Accounts</td><td><strong>T1078.001 - Default Accounts</strong>: Using default credentials for access.<br><br><strong>T1556.003 - Cloud Accounts</strong>: Gain access through compromised Azure AD accounts, often via phishing or brute force.</td></tr></tbody></table>
