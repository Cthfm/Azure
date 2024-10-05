# OneDrive Security

Microsoft OneDrive, part of the Microsoft 365 suite, also has a comprehensive set of security features that mirror and complement those in SharePoint, providing data protection, access control, and compliance options. Here are the key security features of OneDrive:

### 1. **Data Encryption**

* **Encryption at Rest and in Transit**: OneDrive uses encryption both at rest (BitLocker for disk-level encryption and per-file encryption using unique keys) and in transit (SSL/TLS) to protect user data from unauthorized access.

### 2. **Access Control**

* **Role-Based Permissions**: Like SharePoint, OneDrive supports granular access control, where users can control who has access to their files. Permissions can be set at the folder or file level.
* **Conditional Access Policies**: Admins can enforce conditional access policies, ensuring that users only access OneDrive data from compliant or managed devices, approved locations, or under specific conditions.
* **Multi-Factor Authentication (MFA)**: OneDrive integrates with Azure AD for MFA, requiring users to verify their identity with an additional factor beyond just their password.

### 3. **Data Loss Prevention (DLP)**

* OneDrive supports DLP policies to detect and protect against sensitive information leakage. DLP scans files for sensitive data such as financial information, personal data, or intellectual property, and prevents sharing if the policies are triggered.

### 4. **Information Rights Management (IRM)**

* OneDrive uses IRM to restrict actions such as copying, printing, or forwarding files, even if the files are downloaded. This ensures that sensitive information remains secure after it is shared or stored locally.

### 5. **Advanced Threat Protection (ATP)**

* **Malware Scanning and File Blocking**: OneDrive integrates with Microsoft Defender for Office 365, which scans files uploaded to OneDrive for malware and blocks files containing malicious code.
* **Ransomware Protection**: OneDrive has built-in ransomware detection that monitors file activity and alerts users if suspicious behavior (such as rapid file encryption) is detected. It also provides the ability to recover files from a previous version in case of a ransomware attack.

### 6. **Versioning and File Recovery**

* **Version History**: OneDrive automatically maintains a version history for files, allowing users to restore previous versions if files are accidentally deleted, overwritten, or modified.
* **Recycle Bin**: Deleted files are kept in the OneDrive recycle bin for a specific period, enabling users to restore them if needed. For ransomware or accidental deletions, you can also recover the entire OneDrive through a feature called **Files Restore**.

### 7. **External Sharing Control**

* OneDrive allows users to share files with external users but gives administrators full control over how this is done. Admins can set policies to restrict sharing to only specific domains, enforce expiration dates on shared links, or require external users to authenticate.

### 8. **Auditing and Monitoring**

* **Unified Audit Log (UAL)**: OneDrive integrates with the Microsoft 365 Unified Audit Log, allowing detailed tracking of user actions such as file access, sharing, and changes.
* **Alerts**: Administrators can set up alerts for abnormal or suspicious file activities, like large file downloads or sharing events, helping to detect potential insider threats or security breaches.

### 9. **Compliance and Governance**

* **eDiscovery and Legal Hold**: OneDrive integrates with Microsoft 365’s eDiscovery tools, allowing for the identification, preservation, and export of files for legal investigations or compliance needs.
* **Retention Policies**: Organizations can enforce retention policies on OneDrive files to ensure compliance with regulations, making sure files are kept for a required duration or automatically deleted after a specific time.

### 10. **Sensitivity Labels**

* You can apply Microsoft Information Protection sensitivity labels to OneDrive files to classify and protect them based on their level of sensitivity. These labels allow you to automatically apply encryption, set restrictions on access, and track where files are being shared.

### 11. **Secure Sharing Links**

* OneDrive allows users to generate secure sharing links with options to set passwords, expiration dates, and limited permissions (e.g., view-only or edit). Admins can enforce these settings to ensure that shared content remains protected.

### 12. **Zero Trust Integration**

* OneDrive integrates with Microsoft’s Zero Trust framework, ensuring continuous validation of user identities and devices before granting access to sensitive content. This reduces the likelihood of unauthorized access.

### 13. **Personal Vault**

* OneDrive offers a feature called **Personal Vault**, which is an additional layer of security for storing important or sensitive files. Access to this vault requires two-factor authentication (2FA), even for users who are already logged into OneDrive.

### 14. **Compliance Certifications**

* OneDrive is compliant with a range of industry standards, such as ISO 27001, GDPR, HIPAA, and more, ensuring that data stored in OneDrive meets the necessary legal and regulatory requirements.
