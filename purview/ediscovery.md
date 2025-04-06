# eDiscovery

### **What is eDiscovery?**

**eDiscovery** (short for **electronic discovery**) is:

> **The process of identifying, collecting, preserving, reviewing, and exporting electronically stored information (ESI) for legal cases, internal investigations, or regulatory compliance.**

In Microsoft Purview, **eDiscovery** helps organizations quickly **find and manage evidence** across Microsoft 365 services like:

* Exchange Online (emails)
* SharePoint Online (documents)
* OneDrive for Business (files)
* Microsoft Teams (chats and files)

**Key idea:**\
If your company is involved in a lawsuit, investigation, or compliance audit — eDiscovery ensures you can **find and produce evidence** efficiently and defensibly.

***

### **Why eDiscovery Matters**

| Reason                           | Example                                                     |
| -------------------------------- | ----------------------------------------------------------- |
| **Support Legal Investigations** | Locate emails and Teams chats related to a lawsuit.         |
| **Ensure Regulatory Compliance** | Retrieve communications during an SEC or GDPR audit.        |
| **Minimize Business Risk**       | Respond quickly to subpoenas or internal HR investigations. |

Without a strong eDiscovery process, organizations risk **fines**, **legal sanctions**, and **reputational damage**.

***

### **Types of eDiscovery in Microsoft Purview**

| Type                    | Best For                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Core eDiscovery**     | Simple search, hold, and export of data for basic legal or HR cases.                                                |
| **Advanced eDiscovery** | Complex cases needing deep analysis, review sets, tagging, redaction, and legal holds with sophisticated workflows. |

**Important:**

* **Core eDiscovery** is included in Microsoft 365 E3 licenses.
* **Advanced eDiscovery** requires Microsoft 365 E5 or a separate eDiscovery add-on.

***

### **Core eDiscovery Overview**

**Core eDiscovery** allows you to:

* **Create cases** to organize investigations.
* **Search** content across mailboxes, SharePoint, OneDrive, and Teams.
* **Place content on hold** to prevent it from being modified or deleted.
* **Export** search results for review outside Microsoft 365.

It’s ideal for **basic internal investigations** or **small legal requests**.

***

### **Advanced eDiscovery Overview**

**Advanced eDiscovery** adds powerful features like:

| Feature                      | Description                                                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| **Review Sets**              | Organize search results for deeper analysis before export.                                      |
| **Custodian Management**     | Track users involved in the investigation and apply holds to their content.                     |
| **Deep Search**              | Use machine learning to prioritize and cluster similar content.                                 |
| **Redaction**                | Black out sensitive information (e.g., PII) directly inside Microsoft Purview before exporting. |
| **Legal Hold Notifications** | Notify custodians they are under legal hold and track acknowledgment.                           |
| **Audit Trails**             | Maintain logs of actions taken during an investigation.                                         |

**Advanced eDiscovery** is necessary for large-scale litigation and regulated industries.

***

### **eDiscovery Workflow (Core and Advanced)**

1. **Create a Case**\
   Organize the search, hold, and review activities under a case name.
2. **Identify Custodians and Locations**\
   Choose mailboxes, SharePoint sites, Teams channels, or users to investigate.
3. **Search for Content**\
   Define search conditions like keywords, dates, or file types.
4. **Apply Holds**\
   Freeze relevant content to prevent alteration or deletion.
5. **Review and Refine**\
   Preview search results. In Advanced eDiscovery, load results into a Review Set.
6. **Export Data**\
   Export the collected data for legal counsel or further offline review.
7. **Report**\
   Document all actions taken for audit and legal defensibility.

***

### **Common Search Filters in eDiscovery**

| Filter Type          | Example                                    |
| -------------------- | ------------------------------------------ |
| **Keywords**         | “Confidential Project X”                   |
| **Dates**            | Only emails between January 1 and March 31 |
| **Sender/Recipient** | Emails sent by JohnDoe@company.com         |
| **File Types**       | Only Word documents and PDFs               |
| **Locations**        | Only search SharePoint site "HR Documents" |

**Pro Tip:**\
Use **KQL (Keyword Query Language)** for more precise, complex searches.

***

### **Hands-On Lab: Create a Basic eDiscovery Case and Search**

**Objective:**\
Create a simple eDiscovery case to search for emails about "Project X".

#### Step 1: Create a Case

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **eDiscovery** → **Core**.
3. Click **+ Create case** → Name it **Project X Investigation**.

#### Step 2: Create a Search

1. Inside the case, click **Search** → **+ New search**.
2. Add search conditions:
   * Keywords: `Project X`
   * Locations: Select a few mailboxes.

#### Step 3: Apply a Hold (optional)

* Apply a hold to relevant mailboxes if needed to preserve evidence.

#### Step 4: Review and Export

* Preview results.
* Export data if required for further legal analysis.

***

### **Best Practices for eDiscovery**

| Best Practice                          | Why It Matters                                         |
| -------------------------------------- | ------------------------------------------------------ |
| **Define Clear Case Naming Standards** | Makes future retrieval and audits easier.              |
| **Apply Holds Early**                  | Prevent loss or tampering of evidence.                 |
| **Use Narrow Search Filters**          | Reduces irrelevant results (“noise”).                  |
| **Document the Process**               | Creates defensible evidence for court or regulators.   |
| **Train Legal and Compliance Teams**   | Ensures efficient and correct use of eDiscovery tools. |

***

### **Summary**

* **eDiscovery** in Microsoft Purview helps organizations find, preserve, review, and export electronic evidence.
* Use **Core eDiscovery** for basic cases and **Advanced eDiscovery** for complex litigation.
* The **standard workflow** is: Create Case → Search → Hold → Review → Export → Report.
* Following **best practices** ensures defensibility and reduces legal risk.
