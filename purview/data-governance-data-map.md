# Data Governance Data Map

## **Data Governance and Data Map**

***

### **What is Data Governance?**

**Data Governance** in Microsoft Purview is the discipline of:

> **Organizing, managing, and controlling access to your organization's data assets to ensure that data is secure, high-quality, trustworthy, and discoverable.**

It helps answer critical questions like:

* **What data do we have?**
* **Where is our data stored?**
* **How sensitive is it?**
* **Who owns it?**
* **Who can access it?**

**In short:**\
Data Governance ensures your data is organized, protected, and usable for both security and business purposes.

***

### **Why Data Governance Matters**

| Reason                            | Example                                                   |
| --------------------------------- | --------------------------------------------------------- |
| **Improve Security**              | Know where sensitive data lives and who can access it.    |
| **Enhance Compliance**            | Track data locations to comply with GDPR, HIPAA, CCPA.    |
| **Boost Productivity**            | Help users quickly find and trust data through a catalog. |
| **Support Data-driven Decisions** | Provide clean, trusted data for analytics and reporting.  |

Without governance, organizations risk **data sprawl**, **compliance violations**, and **loss of data integrity**.

***

### **What is the Data Map?**

The **Data Map** in Microsoft Purview is a **centralized inventory** of all your data assets.

It’s a **living, breathing** map that automatically updates as new data is discovered, classified, or modified.

Think of it like:

> **Google Maps — but for your organization's data!**

The Data Map includes information like:

* Data asset locations (e.g., Azure Storage, SQL databases, AWS S3)
* Classifications (e.g., Confidential, Public)
* Sensitivity labels
* Schema (columns, tables, metadata)
* Data lineage (where the data came from and how it has changed)

***

### **Key Components of the Data Map**

| Component           | Description                                                                           |
| ------------------- | ------------------------------------------------------------------------------------- |
| **Data Sources**    | Systems where data is stored (Microsoft 365, Azure, AWS, on-prem).                    |
| **Collections**     | Logical groupings of data assets (by department, geography, etc.).                    |
| **Classifications** | Automatic tags based on data sensitivity or type (e.g., detects credit card numbers). |
| **Glossary**        | Business terms that standardize data definitions (e.g., "Customer ID").               |
| **Data Lineage**    | Visual map showing how data flows across systems.                                     |
| **Asset Insights**  | Metadata about each file, table, dataset (location, owner, schema, sensitivity).      |

***

### **How the Data Map is Built**

1. **Connect Data Sources**\
   Connect your cloud, on-premises, and SaaS environments.
2. **Scan Data Sources**\
   Use Purview scanning engines to discover metadata, classifications, and labels.
3. **Organize into Collections**\
   Group assets logically (e.g., HR Data, Financial Systems).
4. **Classify and Label**\
   Apply sensitive information types, sensitivity labels, and glossary terms.
5. **Visualize Data Lineage**\
   Track where data comes from, how it’s processed, and where it’s used.

***

### **Supported Data Sources for Scanning**

| Microsoft Sources                           | Non-Microsoft Sources         |
| ------------------------------------------- | ----------------------------- |
| Azure Blob Storage                          | AWS S3 Buckets                |
| Azure SQL Database                          | Google Cloud Storage          |
| Azure Data Lake Storage                     | Teradata, SAP Hana, Oracle DB |
| Power BI                                    | On-prem SQL Servers           |
| Microsoft 365 (Exchange, SharePoint, Teams) | Third-party SaaS apps         |

> **Important:**\
> Microsoft Purview is a **multi-cloud and hybrid cloud** governance solution — not limited to Microsoft-only environments!

***

### **Data Lineage: Tracking the Flow of Data**

**Data Lineage** shows:

* Where data **originated** (source systems)
* How it has been **transformed** (ETL processes)
* Where it is **consumed** (reports, apps)

**Visualizing Data Lineage** helps you:

* Troubleshoot data quality issues.
* Audit data transformations for compliance.
* Understand dependencies before making changes.

**Example:**\
You can see that a Power BI dashboard is built from an Azure SQL table that originally pulled its data from SAP.

***

### **Glossary and Metadata Management**

Microsoft Purview allows you to:

* Create a **Glossary** of standard business terms.
* Link **business definitions** to **technical metadata**.

| Example Business Term | Definition                                              |
| --------------------- | ------------------------------------------------------- |
| **Customer ID**       | Unique identifier assigned to a customer in CRM system. |
| **Invoice Date**      | Date an invoice was generated for billing purposes.     |

This reduces confusion between technical teams and business users.

***

### **Hands-On Lab: Connect a Data Source and Perform a Scan**

**Objective:**\
Connect an Azure Blob Storage account and perform a metadata scan.

#### Step 1: Connect Data Source

1. Open Microsoft Purview Governance Portal.
2. Go to **Sources** → **Register**.
3. Choose **Azure Blob Storage**.
4. Provide authentication and register the account.

#### Step 2: Scan the Data

1. Navigate to the registered storage source.
2. Click **+ New Scan**.
3. Select a scan rule (default is fine for this lab).
4. Start the scan.

#### Step 3: Explore Data Map

* Once the scan completes:
  * View the discovered assets.
  * Check automatically applied classifications.
  * Browse lineage if available.

***

### **Summary**

* **Data Governance** ensures data is discoverable, secure, and trusted across your organization.
* The **Data Map** is a live inventory of all your data assets, automatically updated by Purview.
* Purview connects to **Microsoft**, **AWS**, **Google Cloud**, and **on-premises** sources.
* **Data Lineage** visually tracks the flow and transformation of data across systems.
* **Glossary terms** bridge the gap between technical metadata and business understanding.
