# MITRE Att\&ck Azure AD Matrix

## Overview:

Azure AD (Active Directory) Matrix is a specific adaptation of the MITRE ATT\&CK framework tailored to identify and mitigate attacks on Azure Active Directory. This matrix provides a comprehensive view of tactics and techniques specifically relevant to threats targeting Azure AD environments. Provided below are sample tactics and techniques within the Azure AD Matrix.

####

### 1. Initial Access

**Explanation:** Techniques that attackers use to gain initial access to the Azure AD environment.

* **Example 1: Phishing**: Attackers send emails with malicious links or attachments to trick users into providing their login credentials.
* **Example 2: OAuth Consent Grant**: Attackers trick users into granting permissions to malicious applications through OAuth consent.
* **Example 3: Credential Stuffing**: Using previously breached credentials to access Azure AD accounts.

### 2. Execution

**Explanation:** Methods used by attackers to run malicious code or scripts in the Azure AD environment.

* **Example 1: PowerShell Execution**: Using PowerShell scripts to execute commands and perform malicious actions.
* **Example 2: Scripting**: Utilizing languages like Python to interact with Azure AD APIs and automate malicious tasks.
* **Example 3: Command Line Interface**: Using command-line tools to interact with Azure AD and execute commands.

### 3. Persistence

**Explanation:** Techniques that ensure attackers can maintain their foothold in the environment.

* **Example 1: Application Access**: Registering malicious applications with broad permissions to maintain access.
* **Example 2: Service Principal Abuse**: Creating or modifying service principals to ensure continuous access.
* **Example 3: Account Manipulation**: Creating new accounts or modifying existing ones to retain access.

### 4. Privilege Escalation

**Explanation:** Methods used to gain higher-level permissions within Azure AD.

* **Example 1: Directory Roles**: Compromising accounts with elevated roles such as Global Administrator.
* **Example 2: Application Permissions**: Manipulating application permissions to gain higher privileges.
* **Example 3: Role Elevation**: Exploiting misconfigurations to elevate user roles.

### 5. Defense Evasion

**Explanation:** Techniques used to avoid detection and bypass security measures.

* **Example 1: Token Impersonation**: Using stolen tokens to impersonate users and evade detection.
* **Example 2: MFA Bypass**: Exploiting vulnerabilities in multi-factor authentication methods to bypass additional security layers.
* **Example 3: Obfuscation**: Hiding the nature of the malicious activity through encoding or encryption.

### 6. Credential Access

**Explanation:** Techniques used to steal user credentials.

* **Example 1: Password Spray**: Attempting common passwords across many accounts to find valid credentials.
* **Example 2: Credential Dumping**: Extracting stored credentials from compromised systems.
* **Example 3: Keylogging**: Capturing keystrokes to obtain credentials.

### 7. Discovery

**Explanation:** Techniques for gathering information about the environment.

* **Example 1: Account Discovery**: Enumerating user accounts to identify targets.
* **Example 2: Group Membership**: Identifying group memberships to understand the organizational structure and identify high-value targets.
* **Example 3: Network Mapping**: Mapping the network to understand the layout and key assets.

### 8. Impact

**Explanation:** Techniques that aim to disrupt or destroy data and systems.

* **Example 1: Account Deletion**: Disabling or deleting user accounts to disrupt operations.
* **Example 2: Service Principal Deletion**: Removing service principals to disrupt services and applications.
* **Example 3: Data Destruction**: Deleting or corrupting data to cause damage.

### Azure AD Attack Matrix Document

{% embed url="https://attack.mitre.org/matrices/enterprise/cloud/azuread/" %}
