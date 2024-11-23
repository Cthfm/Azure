# Credential Access: TA0006

## Overview

The Credential Access tactic focuses on how attackers attempt to steal or collect credentials (such as usernames, passwords, access tokens, or cryptographic keys) from compromised systems to gain unauthorized access. In Azure environments, attackers target Entra ID accounts, service principals, OAuth tokens, API keys, and password stores to escalate privileges or maintain persistence.

#### **1. Brute Force (T1110)**

* **Password Guessing (T1110.001)**
  * **Example:** Attackers manually or programmatically attempt common passwords (e.g., `Password123`, `Welcome2023`) against an Entra ID user account.
  *   **Tools:** Scripts using Azure CLI with commands like:

      ```bash
      az login --username user@domain.com --password Password123
      ```
* **Password Cracking (T1110.002)**
  * **Example:** Attackers use hashed credentials captured from on-premise or cloud systems and crack them offline with tools like **hashcat** or **John the Ripper**.
* **Password Spraying (T1110.003)**
  * **Example:** Attackers try a common password (e.g., `Winter2023`) across multiple accounts in Entra ID to bypass account lockouts triggered by multiple failed attempts on a single account.
  * **Tools:** **MSOLSpray** or custom PowerShell scripts.
* **Credential Stuffing (T1110.004)**
  * **Example:** Attackers use previously leaked credentials from other breaches to attempt logins on Entra ID accounts.
  * **Tools:** Automated scripts or credential stuffing tools like **Sentry MBA**.

### **2. Exploitation for Credential Access (T1212)**

* **Example:** Exploiting vulnerabilities in **Azure AD Connect** or OAuth misconfigurations to extract credentials directly from memory or to gain access tokens.

### **3. Forge Web Credentials (T1606)**

* **SAML Tokens (T1606.002)**
  * **Example:** Attackers generate forged SAML tokens using stolen private keys or exploiting vulnerabilities in identity federation setups.
  * **Tools:** **ADFSpoof** to create forged tokens that grant unauthorized access to Azure resources.

### **4. Modify Authentication Process (T1556)**

* **Multi-Factor Authentication (T1556.004)**
  * **Example:** Attackers exploit MFA bypass techniques, such as using legacy authentication protocols (e.g., IMAP or SMTP), which do not enforce MFA.
* **Hybrid Identity (T1556.005)**
  * **Example:** Exploiting misconfigured **Azure AD Connect** to sync compromised on-premise credentials to Entra ID, enabling attackers to pivot from on-premise to cloud.
* **Conditional Access Policies**
  * **Example:** Attackers exploit weakly configured policies, such as whitelisting of IP ranges or trusted devices, to bypass conditional access restrictions.
* **Multi-Factor Authentication Request Generation**
  * **Example:** Using **MFA fatigue attacks**, attackers repeatedly generate push notifications until the user unintentionally approves the request.

### **5. Steal Application Access Token (T1528)**

* **Example:** Attackers steal OAuth 2.0 tokens from environments like browser storage, CLI tools, or Azure Key Vault to impersonate users or applications.
* #### **Steal or Forge Authentication Certificates (T1552.004)**
  * **Example:** Attackers steal private certificates used for app registration or API authentication to impersonate services or users.
  * **Tools:** Tools like **Certify** or **Mimikatz** can be used to extract certificates.

### **7. Unsecured Credentials (T1552)**

* **Example:** Attackers locate plaintext credentials in Azure resource configurations, scripts, or storage accounts.
*   **Command to Monitor:**

    ```bash
    bashCopy codeaz storage account keys list --account-name <storage_account>
    ```

###

###

### **Summary of Key Concepts with Techniques and Azure Examples for TA0006**

| **Key Concept**                         | **Technique**                            | **Azure Example**                                        |
| --------------------------------------- | ---------------------------------------- | -------------------------------------------------------- |
| Stealing Authentication Tokens          | T1552 - Unsecured Credentials            | Query metadata service for access tokens                 |
| Dumping Passwords from Memory           | T1003 - OS Credential Dumping            | Use Mimikatz on a Windows VM to dump cached credentials  |
| Extracting OAuth Tokens                 | T1550.001 - Application Access Tokens    | Compromise Graph API tokens via phishing                 |
| Brute-Forcing Credentials               | T1110.003 - Password Spraying            | Attempt password spraying on Azure AD accounts           |
| Keylogging and Input Capture            | T1056.001 - Keylogging                   | Deploy keyloggers on compromised VMs                     |
| Exploiting Service Principals           | T1078 - Valid Accounts                   | List service principal credentials using Azure CLI       |
| Exfiltrating Secrets from Key Vault     | T1555 - Credentials from Password Stores | Extract secrets using compromised service principal keys |
| Exploiting PRTs for Unauthorized Access | T1550.004 - Web Session Cookie           | Extract PRTs using Mimikatz to bypass MFA                |
