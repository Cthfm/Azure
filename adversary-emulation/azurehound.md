# AzureHound

## Overview

AzureHound is a tool used by security professionals, especially red teams, to conduct Azure Active Directory (AAD) enumeration and privilege escalation path discovery within Azure environments. It is part of the BloodHound project family and focuses on Azure-specific attack paths, similar to how the original BloodHound maps attack paths within on-premises Active Directory (AD).

AzureHound facilitates mapping and analyzing relationships between users, groups, service principals, and roles within an Azure environment. This helps in identifying misconfigurations and privilege escalation opportunities that could be leveraged to gain elevated access to critical Azure resources.

### Key Features of AzureHound

1. **Azure AD Enumeration:**
   * It gathers information about **users, groups, roles, service principals, and subscriptions**.
   * It identifies potential **attack paths and privilege escalations**, such as users with the ability to assign higher privileges.
2. **Relationship Mapping:**
   * Like BloodHound for AD, AzureHound builds a **graph-based view** of Azure Active Directory objects and their relationships.
   * This graph highlights **direct and indirect paths to privileged access**.
3. **Support for Service Principals and Managed Identities:**
   * It identifies **permissions granted to service principals and managed identities**, which could be abused if misconfigured.
   * Azure environments often depend heavily on service principals, making this aspect of enumeration critical.
4. **Exporting to BloodHound for Visualization:**
   * AzureHound exports collected data into **BloodHound's JSON format**.
   * This enables visualization in the BloodHound UI, making it easier to identify attack paths and escalate privileges.

### How AzureHound Works

#### **Prerequisites**

* Access to the **Azure portal or Azure CLI**.
* Appropriate **API permissions** to collect data from Azure AD.
* **Authentication tokens** (either user or service principal credentials) to run queries against Azure AD.

#### **Data Collection**

* AzureHound runs queries using **Microsoft Graph API** to collect information from Azure AD.
* It maps out relationships and stores them in a graph database that can be analyzed.

**Attack Path Identification**

* After collecting data, AzureHound helps security professionals search for:
  * Users with **excessive permissions**.
  * Roles or identities that could be **exploited**.
  * Misconfigurations that could allow **lateral movement** within the cloud environment.

## Github Link

{% embed url="https://github.com/BloodHoundAD/AzureHound" %}
