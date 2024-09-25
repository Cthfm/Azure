# KQL Introduction

## **Overview of Kusto Query Language**

### **What is KQL?**

KQL (Kusto Query Language) is a powerful, intuitive query language used to interact with large datasets in Azure Data Explorer and other Microsoft services like Azure Sentinel and Log Analytics. Developed by Microsoft, KQL is designed to be easy to read and write, allowing users to quickly analyze and visualize data.

**History and Use Cases**

KQL was created as part of Azure Data Explorer, a fast and highly scalable data exploration service. It is widely used for log and telemetry data analysis, time series data analysis, security analytics, and more. Common use cases include monitoring and diagnostics, security incident detection, and operational intelligence.

### **KQL Syntax and Structure**

#### **Basic Query Structure**

Queries in KQL are composed of statements separated by a pipe (`|`) character. Each statement performs a specific operation on the data, such as filtering, sorting, or aggregating.

*   Example:

    ```kusto
    MyTable
    | where ColumnA == "Value"
    | summarize Count = count() by ColumnB
    | sort by Count desc
    ```
* **Operators and Expressions**
  * KQL uses various operators to manipulate and query data:
    * Comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`
    * Logical operators: `and`, `or`, `not`
    * Arithmetic operators: `+`, `-`, `*`, `/`
  * Expressions combine operators and functions to perform calculations and data transformations.

### **Setting Up Your Environment**

#### **Introduction to Azure Data Explorer**

Azure Data Explorer is a fast and highly scalable data exploration service optimized for log and telemetry data. It enables users to run complex queries on large datasets in near real-time.

**Navigating the Azure Portal**

1. Access the Azure Portal at [portal.azure.com](https://portal.azure.com).
2. Familiarize yourself with the dashboard, resource groups, and services.
3. Locate Azure Data Explorer and create a new cluster if needed.

**Creating a KQL Query Environment**

* Set up a database in Azure Data Explorer:
  1. Navigate to your Azure Data Explorer cluster.
  2. Select "Databases" and click "Add database."
  3. Provide a name for your database and configure retention and caching policies as needed.
* Ingest sample data into your database:
  1. Select your database and click "Ingest new data."
  2. Follow the prompts to upload a sample dataset or connect to a data source.
* Open the Kusto Query Language editor:
  1. Go to your Azure Data Explorer database.
  2. Click "Query" to open the query editor.
  3. Start writing and executing KQL queries.

