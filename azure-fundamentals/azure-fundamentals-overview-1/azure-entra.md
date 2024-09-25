# Azure Entra

Azure Entra is a suite of identity and access capabilities provided by Microsoft to help organizations secure access, manage identities, and ensure compliance across hybrid and multi-cloud environments. Here are the primary services within Azure Entra:

## Overview of Services:

### 1. **Azure Entra ID (formerly Azure Active Directory)**

Azure Entra ID is the foundational identity and access management service within Azure. It provides comprehensive capabilities for managing user identities and securing access to applications both in the cloud and on-premises. Key functionalities include:

* **Single Sign-On (SSO)**: Users can access multiple applications with a single identity.
* **Multi-Factor Authentication (MFA)**: Adds a layer of security by requiring two or more verification methods.
* **Conditional Access**: Allows organizations to implement automated access control decisions based on conditions.
* **Identity Protection**: Uses machine learning to detect anomalies and potential identity threats.

### 2. **Azure Entra Permissions Management**

This service focuses on providing visibility and control over permissions and access in cloud environments. It helps organizations understand and manage who has access to what and how that access is being used. Features include:

* **Centralized Visibility and Insights**: Provides a unified view of permissions across Azure, AWS, and Google Cloud Platform, allowing organizations to see who has access to what resources and how those permissions are utilized.
* **Risk Assessment and Remediation**: Identifies, prioritizes, and mitigates risky permissions by offering automated workflows to enforce least privilege access, reducing potential security vulnerabilities.
* **Compliance and Reporting**: Delivers comprehensive reporting and auditing capabilities to support compliance requirements, helping organizations demonstrate adherence to security policies and regulations.

### 3. **Azure Entra Verified ID**

Azure Entra Verified ID is a decentralized identity service that empowers individuals to control their digital identities using verifiable credentials. This service aligns with the principles of self-sovereign identity (SSI) and can be used for scenarios like:

* **User verification**: Without exposing personal information, verify user credentials in a secure manner.
* **Secure interactions**: Allow secure, privacy-respecting interactions between users and services.

### 4. **Azure Entra External Identities**

Azure Entra External Identities provides capabilities for managing identities of external users (like customers, partners, suppliers) without compromising security or user experience. It includes:

* **B2B (Business-to-Business) collaboration**: Manage guest access to corporate resources.
* **B2C (Business-to-Consumer)**: Customize and control how customers sign up, sign in, and manage their profiles when using your apps.

### 5. **Azure Entra Domain Services**

Azure Entra Domain Services, extends and enhances traditional Active Directory capabilities to the Azure cloud, It is specifically designed to provide managed domain services without the need for a user to deploy and manage domain controllers in the cloud. Here’s a more detailed look at what Azure Entra Domain Services offers:

#### Key Features of Azure Entra Domain Services:

* **Domain Join for VMs**: Allows Azure Virtual Machines (VMs) to join a domain seamlessly, just like on-premises machines, without the need for manual configuration.
* **Group Policy**: Supports Group Policy for managing settings and enforcing security policies across computers in the domain.
* **LDAP (Lightweight Directory Access Protocol)**: Offers LDAP services that applications and third-party tools can use to query directory data.
* **Kerberos/NTLM Authentication**: Provides secure, integrated authentication using standard protocols known from the Windows environment.
* **NTFS (NT File System) Permissions**: Ensures that file system permissions on network file shares are maintained and enforced.
* **Trusts**: Supports setting up trusts with an on-premises Active Directory environment, enabling smooth hybrid operations.

### Microsoft Entra Documentation

{% embed url="https://learn.microsoft.com/en-us/entra/" %}
