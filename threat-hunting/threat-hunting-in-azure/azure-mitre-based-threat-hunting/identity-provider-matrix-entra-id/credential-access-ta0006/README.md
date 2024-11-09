---
hidden: true
---

# Credential Access: TA0006

## Overview

The Credential Access tactic focuses on how attackers attempt to steal or collect credentials (such as usernames, passwords, access tokens, or cryptographic keys) from compromised systems to gain unauthorized access. In Azure environments, attackers target Entra ID accounts, service principals, OAuth tokens, API keys, and password stores to escalate privileges or maintain persistence.

### **1. Stealing Authentication Tokens**

**Technique:** T1552 - Unsecured Credentials\
Attackers search for **access tokens or secrets** left unprotected in memory, files, or logs.

*   **T1552.001 - Credentials in Files**\
    **Azure Example:** Extract **API keys or service principal credentials** from **unprotected configuration files** stored in Blob Storage.

    ```bash
    az storage blob download --container-name config --name creds.json --file /tmp/creds.json
    ```
*   **T1552.004 - Credentials in Cloud Metadata**\
    **Azure Example:** Query **Azure Instance Metadata Service (IMDS)** on a compromised VM to retrieve temporary access tokens.

    ```bash
    curl -H "Metadata: true" "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01"
    ```

### **2. Dumping Password Hashes or Secrets from Memory**

**Technique:** T1003 - OS Credential Dumping\
Attackers extract **password hashes** or **cached credentials** from memory for offline cracking or re-use.

*   **Azure Example:** Use **Mimikatz** on a Windows VM in Azure to dump cached passwords or **Primary Refresh Tokens (PRTs)**, which can be used to bypass MFA.

    ```powershell
    Invoke-Mimikatz -Command "sekurlsa::logonpasswords"
    ```

### **3. Extracting OAuth Tokens and API Keys**

**Technique:** T1550 - Use Alternate Authentication Material\
Attackers steal **OAuth tokens** or **service principal keys** to bypass authentication.

* **T1550.001 - Application Access Tokens**\
  **Azure Example:** Access a user’s **Microsoft Graph API tokens** by compromising their session or via phishing.

### **4. Brute-Forcing Credentials**

**Technique:** T1110 - Brute Force\
Attackers attempt to guess **weak passwords** or **API keys** via automated tools.

* **T1110.003 - Password Spraying**\
  **Azure Example:** Perform a **password spraying attack** against Azure AD accounts to find users with weak passwords.

### **5. Keylogging and Input Capture**

**Technique:** T1056 - Input Capture\
Attackers collect **user credentials** by logging keystrokes or capturing input from login forms.

* **T1056.001 - Keylogging**\
  **Azure Example:** Deploy malware on a compromised **Azure VM** to log user input and steal credentials.

### **6. Exploiting Service Principals for Credential Theft**

**Technique:** T1078 - Valid Accounts (Cloud Accounts)\
Attackers compromise **service principals** to steal their **keys or secrets**, enabling long-term access.

*   **Azure Example:** Use **Azure CLI** to list and export service principal credentials.

    ```bash
    az ad sp list --output json > service_principals.json
    ```

### **7. Exfiltrating Secrets from Azure Key Vault**

**Technique:** T1555 - Credentials from Password Stores\
Attackers access **Azure Key Vault** to exfiltrate stored secrets or certificates.

*   **Azure Example:** Use **compromised service principal credentials** to extract secrets from Key Vault.

    ```bash
    az keyvault secret show --name db-password --vault-name <vault-name>
    ```

### **8. Exploiting Cloud Identity Tokens (PRTs)**

**Technique:** T1550.004 - Web Session Cookie\
Attackers steal **Primary Refresh Tokens (PRTs)** from hybrid-joined devices to impersonate users without re-authentication.

* **Azure Example:** Use **Mimikatz** to extract PRTs from a compromised device, allowing unauthorized access to Microsoft 365 services.

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
