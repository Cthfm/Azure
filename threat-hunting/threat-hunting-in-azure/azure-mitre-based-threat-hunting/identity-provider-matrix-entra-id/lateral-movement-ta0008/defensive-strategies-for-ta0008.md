# Defensive Strategies for TA0008

## **1. Application Access Token (T1550.001)**

**Defenses**:

* **Token Security**:
  * Rotate and revoke tokens periodically, especially after a potential breach.
  * Use Azure Managed Identities for secure token management.
  * Restrict token scope to the minimum permissions required (Principle of Least Privilege).
* **Conditional Access**:
  * Implement policies to ensure that tokens are only issued to compliant devices and trusted locations.
  * Enforce MFA for token issuance where possible.
* **Audit and Monitoring**:
  * Use Azure Monitor or Microsoft Sentinel to track unusual API calls or token activity via logs such as Azure Entra ID Sign-ins and Application logs.

### **2. Pass the Hash (T1550.002)**

**Defenses:**

* **Disable NTLM**:
  * Where feasible, disable NTLM authentication entirely using Group Policy and enforce Kerberos instead.
* **Credential Protection**:
  * Enable Credential Guard on Windows to prevent attackers from extracting password hashes.
  * Regularly reset passwords for accounts synchronized between on-premises AD and Entra ID.
* **Privileged Account Management**:
  * Use Azure Privileged Identity Management (PIM) to limit exposure of privileged accounts.
* **Monitoring**:
  * Analyze sign-ins and authentication patterns for anomalies, focusing on NTLM authentications.

### **3. Pass the Ticket (T1550.003)**

**Defenses**:

* **Kerberos Ticket Expiry**:
  * Reduce Kerberos ticket lifetimes to limit the viability of stolen tickets.
* **Service Account Hardening**:
  * Ensure SPNs (Service Principal Names) are secured and constrained to specific purposes.
* **Privileged Account Segmentation**:
  * Use separate accounts for administrative tasks and day-to-day operations to reduce ticket exposure.
* **Monitoring and Detection**:
  * Enable logging for Kerberos events (Event ID 4769, 4768) and monitor for anomalies such as tickets issued to unauthorized systems.

### **4. Web Session Cookie (T1550.004)**

**Defenses**:

* **Session Security**:
  * Enforce short session lifetimes and require frequent re-authentication for sensitive accounts.
  * Use HTTP-only, Secure, and SameSite attributes for cookies to reduce client-side tampering and cross-site attacks.
* **Zero Trust Enforcement**:
  * Leverage continuous access evaluation (CAE) in Azure Entra ID to monitor for unusual session activities and enforce token revocation dynamically.
* **Browser Security**:
  * Encourage users to avoid public or untrusted devices and clear sessions after use.
  * Deploy Microsoft Defender SmartScreen or similar tools to prevent phishing that may steal cookies.
* **Advanced Threat Detection**:
  * Use Microsoft Defender for Identity to detect anomalous browser patterns or cookie reuse from unexpected geographies or devices.

### Defenses Across Sub-techniques



| Mitigation                        | Guidance                                                                                                                                                                                                                                         |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Multi-Factor Authentication (MFA) | <p>Enforce MFA universally, especially for administrative and privileged accounts.</p><p></p><p>Use phishing-resistant MFA methods, such as hardware security keys (FIDO2).</p>                                                                  |
| Privileged Identity Management    | Apply just-in-time access with Azure AD PIM to limit token exposure for administrative roles.                                                                                                                                                    |
| Audit and Logging                 | <p>Continuously monitor Entra ID logs for unusual authentication patterns (e.g., repeated token refresh attempts, cookie reuse from new geolocations).</p><p></p><p>Centralize log analysis with Microsoft Sentinel or other SIEM solutions.</p> |
| Endpoint Security:                | <p>Harden endpoint devices with tools like Microsoft Defender for Endpoint.</p><p></p><p>Ensure workstations are patched to prevent credential theft methods (e.g., Mimikatz).</p>                                                               |
| Incident Response Playbooks       | Develop playbooks for compromised credentials, including automated token and session revocation through PowerShell or Azure AD APIs.                                                                                                             |
| Conditional Access Policies       | Implement session control policies in Microsoft Defender for Cloud Apps to enforce real-time access restrictions.                                                                                                                                |
| User Education                    | Train users to identify and avoid phishing attempts that target session cookies or token theft.                                                                                                                                                  |
| Continuous Access Evaluation      | Enable within applications as well as users access Microsoft applications such as Outlook and SharePoint.                                                                                                                                        |
