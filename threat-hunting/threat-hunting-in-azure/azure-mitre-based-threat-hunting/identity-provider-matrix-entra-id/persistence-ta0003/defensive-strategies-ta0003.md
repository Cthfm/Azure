# Defensive Strategies: TA0003

## **Defensive Strategies for TA0003 - Persistence**

The persistence tactic involves attackers control and repeatedly access resources over extended periods. This is often done by exploiting identity and access management misconfigurations, creating new accounts, adding extra credentials to existing accounts, or modifying authentication processes. Provided below are strategies for defense.

### 1. **Account Manipulation (T1098)**

Attackers often manipulate existing accounts to maintain or elevate their access, sometimes by adding credentials or roles or by modifying Intune policies.

* **T1098.001 - Add Additional Credentials**
  * **Defensive Strategy**:
    * **Monitor for New Application Credentials**: Use Entra ID to sign-in and audit logs to track any creation of new credentials associated with applications. Monitor for unusual credential usage patterns.
    * **Automated Alerts**: Configure Microsoft Sentinel or Entra ID Identity Protection to trigger alerts for the creation of new application credentials, especially with critical service principals.
    * **Access Reviews**: Regularly review service principals and their credentials to ensure they are authorized and necessary.
* **T1098.003 - Additional Cloud Roles**
  * **Defensive Strategy**:
    * **Role Assignment Monitoring**: Enable alerts in Microsoft Sentinel for any new role assignments, particularly for privileged roles like Contributor or Owner, assigned to accounts outside of expected patterns.
    * **Conditional Access Policies**: Use Conditional Access to restrict privileged roles, ensuring only designated devices or IPs can make changes.
    * **Privileged Identity Management (PIM)**: Use PIM to enforce just-in-time (JIT) access for sensitive roles, making it difficult for attackers to maintain persistent privileged access.
* **T1098.005 - Registered Device**
  * **Defensive Strategy**:
    * **Monitor Device Registrations in Intune**: Configure Intune to alert on newly registered devices and any modifications to Intune policies.
    * **Conditional Access Policies**: Require device compliance checks before access to sensitive resources.
    * **Device Compliance Policy Reviews**: Regularly review Intune compliance policies for modifications that could allow rogue devices access.

### 2. **Create Account (T1136)**

Attackers may create new accounts within the tenant to ensure persistence.

* **T1136.003 - Cloud Account**
  * **Defensive Strategy**:
    * **Audit for New Accounts**: Use Entra ID Audit Logs to monitor for any new account creations, especially accounts with privileged roles or unusual naming patterns.
    * **Automated Alerts**: Set alerts in Microsoft Sentinel for unusual account creation activity, particularly during off-hours or from unexpected IP addresses.
    * **Conditional Access Policies**: Require MFA and location-based restrictions for all new accounts, especially for those with access to sensitive resources.

### 3. **Modify Authentication Process (T1556)**

Attackers may modify authentication processes to bypass security controls, such as MFA.

* **T1556.006 - Multifactor Authentication**
  * **Defensive Strategy**:
    * **MFA Configuration Monitoring**: Use audit logs to monitor any changes in MFA settings or Conditional Access policies and alert on modifications.
    * **Enforce Strong MFA**: Require strong, phishing-resistant MFA options, such as FIDO2 tokens, for all privileged accounts.
    * **Access Control Reviews**: Regularly review Conditional Access policies for modifications that could weaken MFA requirements.
* **T1556.003 - Hybrid Identity**
  * **Defensive Strategy**:
    * **Monitor PTA Agent Activity**: Use Azure Entra ID Connect Health to monitor Pass-Through Authentication (PTA) agents for signs of tampering, such as DLL injections or unusual traffic.
    * **AD FS Configuration Monitoring**: Regularly audit AD FS configurations and monitor for modifications in the Microsoft.IdentityServer.Servicehost.exe.config file.
    * **SIEM Integration**: Use Microsoft Sentinel to correlate logs from PTA agents, AD FS, and Entra ID for suspicious modifications.

### 4. **Valid Accounts (T1078)**

Attackers may leverage existing, valid accounts, sometimes using default credentials.

* **T1078.001 - Default Accounts**
  * **Defensive Strategy**:
    * **Disable Unused Default Accounts**: Disable default accounts where possible, especially for high-privilege accounts.
    * **Password Policy Enforcement**: Enforce strong password policies for all accounts, especially service accounts, to prevent the use of default or weak credentials.
    * **Audit Account Access**: Use Entra ID and Conditional Access policies to limit default account usage to specific conditions and locations.
* **T1556.003 - Cloud Accounts**
  * **Defensive Strategy**:
    * **Monitor Failed Sign-Ins**: Use Azure AD Sign-In Logs to identify brute force or credential stuffing attempts, particularly from unusual IPs or countries.
    * **Anomaly Detection**: Use Azure AD Identity Protection to detect risky sign-ins or atypical user behavior that could indicate compromised credentials.
    * **Conditional Access Policies**: Enforce Conditional Access policies to require MFA and restrict access based on risk signals.
