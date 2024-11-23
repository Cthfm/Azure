# Defensive Strategies for TA0006

## Defensive Strategies for TA0006 - Credentialed Access

The **Credentialed Access (TA0006)** tactic involves attackers leveraging legitimate credentials or forging authentication artifacts to gain unauthorized access to systems, networks, or applications. Defensive strategies focus on protecting credentials, monitoring authentication processes, and ensuring secure configurations in identity management systems like **Entra ID**.

### **1. Defend Against Brute Force Attacks**

**Mitigates:** T1110 - Brute Force\
**Action:** Prevent attackers from successfully guessing or cracking passwords.\
**Azure Procedure:**

* Enforce **strong password policies** using Entra ID banned password lists and complexity requirements.
* Enable **Smart Lockout** to block accounts exhibiting unusual login attempts.
* Detect and respond to suspicious activity by monitoring Entra ID sign-in logs for failed authentication attempts.
* Use **Conditional Access Policies** to restrict access based on geolocation or device compliance.
* Enable **Azure AD Password Protection** to prevent the use of weak or leaked passwords.

### **2. Prevent Exploitation for Credential Access**

**Mitigates:** T1212 - Exploitation for Credential Access\
**Action:** Protect against exploitation of vulnerabilities that reveal credentials.\
**Azure Procedure:**

* Regularly patch and update Entra ID Connect and other identity-related services.
* Monitor for unauthorized access attempts to identity-related endpoints using Microsoft Defender for Identity.
* Limit permissions on Azure Key Vault and ensure credentials stored within are secured using access policies.

### **3. Secure Against Forged Web Credentials**

**Mitigates:** T1606.002 - SAML Tokens\
**Action:** Detect and prevent the forging of SAML tokens.\
**Azure Procedure:**

* Protect the private keys used by Entra ID or federated identity providers by storing them in **Ha**rdware Security Modules (HSMs) or using Azure KMS.&#x20;
* Enable token signing certificate rotation to limit the time attackers can use compromised signing certificates.
* Monitor authentication activity for anomalies, such as SAML tokens with excessive privileges or issued outside normal timeframes.

### **4. Harden the Authentication Process**

**Mitigates:** T1556 - Modify Authentication Process\
**Action:** Prevent attackers from tampering with or bypassing authentication mechanisms.\
**Azure Procedure:**

* Enable Multi-Factor Authentication (MFA) for all users, especially for privileged accounts.
* Disable legacy authentication protocols (e.g., IMAP, SMTP) that bypass MFA enforcement.
* Implement Conditional Access Policies to restrict access based on risk signals like unfamiliar locations, IPs, or devices.
* Monitor sign-in logs for excessive MFA requests, which may indicate an MFA fatigue attack.
* Audit Azure AD Connect synchronization configurations to ensure hybrid identity settings are not exposing vulnerabilities.

### **5. Detect and Protect Against Stolen Access Tokens**

**Mitigates:** T1528 - Steal Application Access Token\
**Action:** Prevent attackers from using stolen tokens to impersonate users or applications.\
**Azure Procedure:**

* Use Conditional Access Policies to require reauthentication for sensitive resources, even with a valid token.
* Monitor Azure Activity Logs for token-related anomalies, such as suspicious `az account get-access-token` commands.
* Use Microsoft Defender for Cloud Apps to monitor and revoke OAuth tokens for compromised accounts or applications.

### **6. Secure Authentication Certificates**

**Mitigates:** T1552.004 - Steal or Forge Authentication Certificates\
**Action:** Protect certificates used for authentication and service-to-service communication.\
**Azure Procedure:**

* Store authentication certificates in **Azure Key Vault**, secured with access policies.
* Regularly rotate and audit certificate permissions.
* Enable **Azure Sentinel** alerts for suspicious activity involving certificates, such as unauthorized downloads.

### **7. Identify and Mitigate Unsecured Credentials**

**Mitigates:** T1552 - Unsecured Credentials\
**Action:** Prevent attackers from accessing plaintext credentials in storage or code.\
**Azure Procedure:**

* Audit scripts, configuration files, and code repositories for hardcoded credentials.
* Use Azure Key Vault to securely store secrets, ensuring that access is controlled by RBAC and policies.
* Monitor resource access logs for unusual access patterns to secrets or storage accounts.
* Disable the retrieval of storage account keys via `az storage account keys list`.

### **8. Use Just-in-Time Access for Privileged Roles**

**Mitigates:** Multiple Credentialed Access Techniques\
**Action:** Reduce the exposure of privileged accounts and credentials.\
**Azure Procedure:**

* Enable Privileged Identity Management (PIM) in Entra ID to enforce just-in-time access for administrative roles.
* Monitor Azure AD role assignments for suspicious or unauthorized changes.
* Require approval workflows for granting elevated permissions.

### **9. Monitor and Automate Response to Credential Theft Attempts**

**Mitigates:** Multiple Credentialed Access Techniques\
**Action:** Leverage automation to detect and mitigate credential misuse in real-time.\
**Azure Procedure:**

* Use Azure Sentinel to create automated playbooks that detect and respond to anomalies, such as excessive failed login attempts or unauthorized role changes.
* Implement playbooks that can disable compromised accounts, revoke tokens, or alert administrators.

### **10. Secure Application Permissions and Delegations**

**Mitigates:** T1212, T1528\
**Action:** Limit the scope and permissions granted to applications.\
**Azure Procedure:**

* Regularly audit OAuth permissions for applications in Entra ID.
* Remove unnecessary delegated permissions from applications.
* Monitor suspicious application access attempts with Microsoft Defender for Cloud Apps.

### **Summary of Defensive Strategies for TA0006**

| **Defensive Strategy**                                        | **Mitigates**                                              | **Azure Solution**                                                                                                    |
| ------------------------------------------------------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Use secrets managers with HSM-backed options like Managed HSM | T1552.004 - Steal or Forge Authentication Certificates     | Azure Key Vault Managed HSM for FIPS 140-2 Level 3 compliance and tamper-resistant key storage.                       |
| Leverage built-in cloud key management services               | T1552 - Unsecured Credentials                              | Azure Key Vault Standard for encrypted key storage and access controls backed by Microsoft-managed HSMs.              |
| Adopt software-based key protection with strong security      | T1552 - Unsecured Credentials                              | Encrypt stored keys using AES-256 and secure storage with RBAC and encrypted databases.                               |
| Replace static keys with managed identities                   | T1528 - Steal Application Access Token                     | Azure Managed Identities for seamless and secure application authentication without storing credentials.              |
| Implement robust key rotation policies                        | T1552.004 - Steal or Forge Authentication Certificates     | Automate key rotation using Azure Key Vault to minimize risks of stale or exposed keys.                               |
| Enforce multi-layered access controls                         | T1556 - Modify Authentication Process                      | Use Conditional Access Policies, MFA, and RBAC in Entra ID to restrict and monitor access to keys.                    |
| Token-based authentication for federated systems              | T1606.002 - SAML Tokens                                    | Use Azure AD B2C for managing federated authentication securely and without key exposure.                             |
| Strengthen threat monitoring and incident response            | T1528 - Steal Application Access Token T1110 - Brute Force | Deploy **Azure Sentinel** to detect anomalies in key access and integrate with playbooks for automated responses.     |
| Evaluate shared HSM services for cost-efficient security      | T1552.004 - Steal or Forge Authentication Certificates     | Use Azure Dedicated HSM for multi-tenant configurations offering hardware-level security at reduced cost.             |
| Mitigate risks with encryption hierarchies                    | TT1552 - Unsecured Credentials                             | Store key encryption keys (KEKs) in Azure Key Vault to secure operational keys with an additional layer.              |
| Detect and block brute force attempts                         | T1110 - Brute Force                                        | Use Smart Lockout, Conditional Access Policies, and Entra ID sign-in logs to monitor and prevent brute force attacks. |

