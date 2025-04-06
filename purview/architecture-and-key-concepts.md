# Architecture and Key Concepts

## **Microsoft Purview Architecture and Key Concepts**

***

### **Understanding Microsoft Purview Architecture**

Microsoft Purview’s architecture is designed to work **across clouds, devices, and services** seamlessly.

At a high level, it consists of:

| Component                              | Purpose                                                                                                             |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Data Sources**                       | The systems where your data lives (e.g., Microsoft 365, Azure SQL, AWS S3, on-premises servers).                    |
| **Data Map**                           | A cloud-based, continuously updated map that tracks all discovered data assets, their classifications, and lineage. |
| **Purview Governance Portal**          | Interface to manage cataloging, scanning, classification, and metadata.                                             |
| **Purview Compliance Portal**          | Interface to manage information protection, risk management, auditing, and compliance.                              |
| **Microsoft 365 Workloads**            | Exchange Online, SharePoint, OneDrive, Teams — all feed data into Purview.                                          |
| **Scanning and Classification Engine** | Continuously scans data, classifies it based on sensitivity or regulatory requirements, and labels it.              |
| **Policy Enforcement**                 | Applies protection policies like DLP rules, retention, encryption, or access restrictions.                          |

***

### **Important Concepts You Must Know**

When working with Microsoft Purview, you will repeatedly encounter these concepts:

| Concept            | What It Means                                                                                                       |
| ------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Data Asset**     | Any piece of data (document, database, email) that Purview can discover and govern.                                 |
| **Scan**           | The process Purview uses to look into your data sources and extract metadata.                                       |
| **Classification** | Labeling data according to its type, value, or sensitivity (e.g., “Confidential”, “Financial Data”).                |
| **Label**          | A tag attached to data to indicate sensitivity or retention needs.                                                  |
| **Policy**         | A set of rules about what can or cannot happen to labeled or classified data.                                       |
| **Data Map**       | A living index of all scanned data assets, where they reside, how they are classified, and how they move (lineage). |
| **Retention**      | How long you keep data before deleting or archiving it according to regulatory or business needs.                   |
| **Data Lineage**   | The record of where the data came from and how it has been transformed over time.                                   |

***

### **How Data Flows in Purview**

1. **Scan** the data sources (Microsoft 365, Azure Storage, etc.)
2. **Classify** the data automatically or manually (e.g., Credit Card Numbers, Health Records).
3. **Label** the data using sensitivity labels (Confidential, Restricted, Highly Confidential).
4. **Apply Protection Policies** (DLP, Encryption, Retention).
5. **Monitor and Audit** actions related to that data.
6. **Respond** to compliance and risk issues if they arise.

**Visual Overview:**

```
rustCopyEditData Source --> Scan --> Classify --> Label --> Protect --> Monitor/Audit --> Respond
```

***

### **Data Sources Supported by Purview**

Purview can connect to:

| Microsoft Data Sources       | Non-Microsoft Data Sources |
| ---------------------------- | -------------------------- |
| Exchange Online              | Amazon S3 Buckets          |
| SharePoint Online            | Google Cloud Storage       |
| OneDrive for Business        | SQL Server On-premises     |
| Microsoft Teams              | Teradata                   |
| Azure SQL Database           | SAP Hana                   |
| Azure Blob Storage           | Oracle DB                  |
| Azure Data Lake Storage Gen2 | Various SaaS applications  |

**Key point:** Purview is not limited to Microsoft-only data. It can scan and govern hybrid and multi-cloud environments.

***

### **Role-Based Access Control (RBAC) in Purview**

Access to Purview features is tightly controlled by **roles**:

| Role Name                         | Permissions                                                                       |
| --------------------------------- | --------------------------------------------------------------------------------- |
| **Purview Administrator**         | Full access to configure Purview, manage sources, manage scans, and set policies. |
| **Data Curator**                  | Manages data catalog, classifications, glossary terms.                            |
| **Data Reader**                   | Can browse the data catalog but cannot modify data.                               |
| **Compliance Administrator**      | Manages policies for data protection, insider risk, and compliance.               |
| **Insider Risk Management Admin** | Manages insider risk policies and investigations.                                 |

> **Important:** Always follow the **principle of least privilege** — only give users the minimum permissions they need.

***

### **Hands-On Lab: Explore Data Sources and Roles**

**Objective:** Get familiar with how data sources are connected and how roles are assigned in Purview.

#### Step 1: Explore Data Sources

* Go to Microsoft Purview Governance Portal.
* Navigate to **Data Map** → **Sources**.
* Browse the available Microsoft 365 and Azure sources.
* Add a test data source if you have permission.

#### Step 2: Explore Roles

* In the Microsoft Purview Compliance Portal ([https://compliance.microsoft.com](https://compliance.microsoft.com/)):
  * Go to **Permissions** under **Solutions**.
  * Review the available role groups like:
    * **Information Protection Admins**
    * **Compliance Data Administrators**
    * **Insider Risk Management Admins**
  * Check which permissions each role grants.
