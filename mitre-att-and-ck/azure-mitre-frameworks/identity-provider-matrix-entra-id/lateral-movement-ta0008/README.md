# Lateral Movement TA0008

## Overview

Lateral Movement in Entra ID (formerly Azure AD) refers to techniques attackers employ to traverse and gain access to resources within an organization's identity and access management (IAM) environment. Adversaries often exploit compromised credentials, abused refresh or access tokens, or misconfigured role assignments to escalate privileges and expand their control. The goal is to navigate through interconnected services, groups, or identities to identify and access high-value targets. Attackers might abuse legitimate Entra ID tools such as PowerShell modules (e.g., AzureAD, MSOnline), Entra Graph API, or third-party management scripts to maintain stealth. Techniques include abusing service principals, leveraging excessive permissions in privileged roles, token impersonation, and exploiting conditional access gaps or trust relationships between tenants. Such activities may also target hybrid setups where on-premises Active Directory is synced to Entra ID, enabling deeper network infiltration.

For the scope of this section, we will primarily focus on compromising credentials.&#x20;

### **1. Stealing Authentication Tokens**

**Technique:** T1550 - Use Alternate Authentication Material\
Attackers search for **a**ccess tokens or secrets left unprotected in memory, files, or logs. Attackers can also intercept them.

*   **T1550.001: Application Access Token**

    Adversaries use tokens such as access, refresh, PRT tokens, or other bearer tokens to authenticate directly with services or applications. In Azure Entra ID, these tokens are commonly issued to apps and can be abused if compromised.
*   **T1550.002: Pass the Hash**

    Attackers use a stolen NTLM hash to authenticate without needing the plaintext password. In hybrid environments involving Azure Entra ID, this technique can be used against synchronized accounts where password hashes are synchronized to on-premises AD.
*   **T1550.003: Pass the Ticket**

    Using stolen Kerberos tickets, such as TGTs (Ticket Granting Tickets), attackers gain access to systems or services without re-entering credentials. This is particularly relevant in environments where Entra ID integrates with on-premises AD through Kerberos-based authentication mechanisms.
*   **T1550.004: Web Session Cookie**

    Adversaries hijack valid web session cookies to impersonate users. In Entra ID, attackers may steal cookies from browsers to bypass MFA and maintain access to cloud services like Microsoft 365 or Azure portal.





