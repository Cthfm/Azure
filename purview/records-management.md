# Records Management

## **Module 8: Records Management**

***

### **What is Records Management?**

**Records Management** in Microsoft Purview is the process of:

> **Managing the lifecycle of important content — deciding how long to keep it, how to store it, and when to delete or archive it.**

It helps organizations comply with legal, regulatory, and business requirements by ensuring:

* Critical information is **retained** for as long as necessary.
* Unnecessary or obsolete data is **disposed of securely**.
* Data is **discoverable** if needed (e.g., for legal investigations).

Records Management protects your organization from:

* Legal risks (by retaining important evidence)
* Compliance risks (by proving you follow regulations)
* Security risks (by removing unnecessary sensitive data)

***

### **Key Concepts: Records vs Regular Content**

| Concept                          | Regular Content   | Records                                  |
| -------------------------------- | ----------------- | ---------------------------------------- |
| **Editable?**                    | Yes               | No (locked after declared)               |
| **Retention Control?**           | No specific rules | Strict retention and deletion rules      |
| **Legal/Compliance Importance?** | Low to medium     | High — must meet regulatory requirements |

In Microsoft Purview, **declaring a record** means a document or email becomes:

* **Immutable**: It cannot be edited or deleted by users.
* **Governed**: It follows strict lifecycle policies until final disposition.

***

### **Retention Labels vs Retention Policies**

| Feature                   | Retention Label                              | Retention Policy                           |
| ------------------------- | -------------------------------------------- | ------------------------------------------ |
| **Granularity**           | Item-level (specific emails, documents)      | Location-wide (entire mailbox, site, etc.) |
| **User Application**      | Users can manually apply labels              | Users don't see retention policies         |
| **Automatic Application** | Yes (with conditions)                        | Yes (applied to all content in a location) |
| **Best Use Case**         | Manage highly sensitive or regulated content | Broad content management at scale          |

> **Important:**\
> **Retention Labels** are more powerful because they can both **retain** and **declare content as a record**.

***

### **Retention Settings Explained**

When you configure a **Retention Label** or **Retention Policy**, you define:

| Setting                   | Meaning                                                      |
| ------------------------- | ------------------------------------------------------------ |
| **Retain content**        | Keep content for a minimum period, even if deleted by users. |
| **Delete content**        | Permanently delete content after a set period.               |
| **Trigger for retention** | When created, modified, or labeled.                          |
| **Declare as a record**   | Lock the item — users can’t edit or delete it manually.      |

You can **retain**, **delete**, or **retain then delete** — depending on your needs.

***

### **Two Types of Records in Microsoft Purview**

| Record Type           | Description                                                                                                    |
| --------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Record**            | Users can still update metadata (e.g., tags), but content (body) is locked.                                    |
| **Regulatory Record** | Even stricter. Neither content nor metadata can be changed — only specific admin actions can modify or delete. |

**Regulatory Records** are typically used in industries like finance or healthcare where extremely tight control is required.

***

### **Disposition Review Workflow**

When an item reaches the end of its retention period, you can:

* **Automatically delete it** without review.
* **Trigger a Disposition Review** — someone manually reviews it before deletion.

**Disposition Review** allows you to:

* Review items one by one
* Extend retention
* Delete
* Transfer or archive valuable records

This step is essential when you need legal or compliance teams to approve destruction of sensitive content.

***

### **How Records Management Fits with eDiscovery**

Proper records management ensures that:

* Relevant records are **available** during legal investigations.
* Records have an **audit trail** showing they were managed correctly.
* Organizations can **prove compliance** with data retention requirements.

***

### **Hands-On Lab: Create and Publish a Retention Label to Declare a Record**

**Objective:**\
Create a Retention Label that marks documents as records for five years and then deletes them.

#### Step 1: Create the Retention Label

1. Open the [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Go to **Information Governance** → **Labels** → **+ Create a label**.
3. Name it: **5-Year Record Retention**\
   Description: **Declare items as records for 5 years, then delete.**

#### Step 2: Configure Retention Settings

* Retain content for **5 years**.
* After 5 years, **delete** the content automatically.
* **Declare items as records**.

#### Step 3: Publish the Label

* Create a **Label Policy** and assign it to **SharePoint sites** or **OneDrive accounts** where critical documents are stored.
* Save and publish.

#### Step 4: Test It

* Upload a document to SharePoint.
* Apply the **5-Year Record Retention** label manually.
* Verify that:
  * The document is marked as a **record**.
  * Editing is restricted.

***

### **Summary**

* **Records Management** in Microsoft Purview governs the lifecycle of important content.
* **Retention Labels** apply at the item level and can declare records.
* **Retention Policies** apply broadly across locations.
* **Records** are locked but allow metadata updates, while **Regulatory Records** are stricter.
* **Disposition Reviews** add a manual review process before deleting important content.
* Good Records Management ensures you stay **legally compliant** and **reduce risk**.
