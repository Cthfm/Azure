# Microsoft 365: Sharepoint Security

## Overview

Microsoft SharePoint 365, part of Microsoft 365, has several robust security features designed to protect data, control access, and ensure compliance. Here are some key security features:

### 1. **Data Encryption**

* **Encryption at Rest and in Transit**: SharePoint 365 data is encrypted both at rest (using BitLocker and distributed keys) and during transit with SSL/TLS to protect sensitive data.

### 2. **Access Control**

* **Role-Based Access Control (RBAC)**: SharePoint allows detailed permission settings for users, groups, or security roles. You can control access to individual files, folders, and entire SharePoint sites.
* **Conditional Access Policies**: Leveraging Azure AD, administrators can enforce conditional access policies to control how and from where users access SharePoint based on factors like device type, user location, and user risk level.
* **Multi-Factor Authentication (MFA)**: SharePoint 365 can require MFA for users to provide additional verification beyond just a password, adding a layer of security.

### 3. **Data Loss Prevention (DLP)**

* DLP policies can be applied to SharePoint Online to prevent the accidental sharing of sensitive information such as credit card numbers, Social Security numbers, or other sensitive data. Administrators can configure DLP policies to detect specific information types and take action (e.g., blocking access or notifying users).

### 4. **Compliance and Governance**

* **eDiscovery**: SharePoint integrates with Microsoft 365’s eDiscovery tools, allowing organizations to find, preserve, and export content as part of legal investigations.
* **Retention Policies**: Organizations can set up retention labels and policies to retain or delete documents based on compliance regulations or internal policies.

### 5. **Information Rights Management (IRM)**

* IRM in SharePoint Online can restrict actions such as copying, printing, and forwarding files. This ensures that even if a document is downloaded, it remains protected.

### 6. **Advanced Threat Protection (ATP)**

* SharePoint integrates with Microsoft Defender for Office 365, offering protection from malicious files and phishing attempts. ATP scans files in document libraries to detect and block malware.

### 7. **Audit Logs**

* SharePoint Online integrates with the Unified Audit Log (UAL) in Microsoft 365, allowing detailed tracking of user actions (e.g., file access, sharing activity). This is crucial for monitoring suspicious behavior or forensically investigating incidents.

### 8. **External Sharing Management**

* SharePoint 365 has settings to control how data is shared externally. Admins can manage whether sharing with external users is allowed and set limits on how external sharing occurs, ensuring that only authorized users can access sensitive data.

### 9. **Secure Sharing Links**

* **Expiration and Password-Protected Links**: When sharing documents or folders externally, admins can enforce expiration dates and passwords on the shared links for additional security.

### 10. **Alerts and Monitoring**

* Administrators can set up alerts for file modifications or access attempts. These notifications can be used to detect unusual behavior or potential security risks in real time.

### 11. **Sensitivity Labels**

* You can apply Microsoft Information Protection sensitivity labels to classify and protect SharePoint content. These labels ensure documents are appropriately secured based on their classification (e.g., public, confidential, highly confidential).
