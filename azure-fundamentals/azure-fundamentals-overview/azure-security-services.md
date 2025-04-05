# Azure Security Services

## Azure Security Services Overview

The following provides a list of security services that are deployed in Azure.

***

| Service Name                                               | What It Does                                                                                                                                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Microsoft Defender for Cloud**                           | Cloud-native security posture management and threat protection for Azure, AWS, and GCP. Helps you find and fix misconfigurations and detect threats.                                 |
| **Microsoft Defender for Endpoint**                        | Advanced threat protection for devices (Windows, Linux, macOS, Android, iOS). Detects and responds to attacks.                                                                       |
| **Microsoft Defender for Identity**                        | Protects on-premises Active Directory from identity-based attacks (e.g., pass-the-hash, lateral movement).                                                                           |
| **Microsoft Defender for Office 365**                      | Protects email and collaboration tools from phishing, malware, and business email compromise.                                                                                        |
| **Microsoft Defender for Cloud Apps**                      | Monitors and controls cloud app usage (Shadow IT) and protects SaaS apps like Salesforce, ServiceNow, Dropbox.                                                                       |
| **Microsoft Sentinel**                                     | Cloud-native SIEM (Security Information and Event Management) and SOAR (Security Orchestration Automated Response) platform for detecting, investigating, and responding to threats. |
| **Azure Firewall**                                         | Fully managed, scalable, stateful firewall as a service for protecting Azure Virtual Networks.                                                                                       |
| **Azure DDoS Protection**                                  | Protects applications from Distributed Denial of Service (DDoS) attacks by absorbing and mitigating attacks automatically.                                                           |
| **Azure Web Application Firewall (WAF)**                   | Protects web apps from common exploits like SQL injection, cross-site scripting (XSS), and more.                                                                                     |
| **Azure Key Vault**                                        | Securely store and tightly control access to secrets, encryption keys, and certificates.                                                                                             |
| **Azure Active Directory (Entra ID)**                      | Identity and access management service for managing users, groups, and device authentication securely. Supports SSO, MFA, Conditional Access, and Identity Protection.               |
| **Azure Security Center (Now part of Defender for Cloud)** | Previously a standalone service to manage security across Azure, now integrated into Microsoft Defender for Cloud.                                                                   |
| **Azure Policy**                                           | Enforces organization-specific rules and compliance (e.g., "All storage accounts must be encrypted").                                                                                |
| **Azure Blueprints**                                       | Package Azure resources, policies, role assignments, and resource groups into repeatable templates to enforce security and compliance.                                               |
| **Azure Bastion**                                          | Secure RDP/SSH to VMs directly in the Azure Portal without needing a public IP on the VM.                                                                                            |
| **Microsoft Purview Compliance Portal**                    | Manage data governance, information protection, and compliance risks across your cloud and on-premises environments.                                                                 |
| **Microsoft Entra Permissions Management**                 | Provides visibility and control over permissions across multi-cloud environments (Azure, AWS, GCP) to help enforce least privilege.                                                  |
| **Azure Confidential Computing**                           | Protects data while it’s in use by running applications in secure, hardware-based enclaves.                                                                                          |
| **Azure Disk Encryption**                                  | Encrypts Azure Virtual Machine disks using BitLocker (Windows) or DM-Crypt (Linux).                                                                                                  |
| **Azure Private Link**                                     | Enables private access to Azure services over a private network, isolating traffic from the internet.                                                                                |
| **Azure Information Protection**                           | Classifies, labels, and protects documents and emails based on sensitivity.                                                                                                          |
| **Microsoft Intune**                                       | Manages and secures mobile devices, apps, and PCs. Important for endpoint management and Zero Trust security.                                                                        |
| **Azure Monitor and Logs**                                 | Collects, analyzes, and acts on telemetry data from Azure resources to monitor and secure environments.                                                                              |
| **Azure Role-Based Access Control (RBAC)**                 | Controls who can access Azure resources and what they can do. Supports least privilege access management.                                                                            |
| **Microsoft Entra Verified ID**                            | Provides decentralized identity verification (blockchain-backed credentials) for secure authentication and trust scenarios.                                                          |

***

## Categories:

| Area                                 | Services Involved                                                                                          |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| **Identity & Access**                | Azure Active Directory (Entra ID), Entra Permissions Management, Verified ID                               |
| **Threat Protection**                | Microsoft Defender suite (for Cloud, Endpoint, Identity, Office 365, Cloud Apps)                           |
| **Network Security**                 | Azure Firewall, Azure DDoS Protection, Azure Bastion, Azure Private Link                                   |
| **Application & Data Protection**    | Azure Key Vault, Azure Disk Encryption, Azure WAF, Purview Compliance Portal, Azure Information Protection |
| **Security Management & Monitoring** | Microsoft Defender for Cloud, Microsoft Sentinel, Azure Policy, Azure Monitor                              |

***

## Summary:

| Security Need                 | Key Service(s)                                     |
| ----------------------------- | -------------------------------------------------- |
| Secure access and identity    | \Entra ID, Intune                                  |
| Detect and respond to threats | Microsoft Defender family, Sentinel                |
| Protect networks              | Azure Firewall, DDoS Protection, Private Link      |
| Protect data                  | Key Vault, Disk Encryption, Confidential Computing |
| Enforce compliance            | Azure Policy, Blueprints, Microsoft Purview        |
