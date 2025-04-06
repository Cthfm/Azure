# Information Protection and Encryption

## **Module 7: Information Protection and Encryption**

***

### **What is Information Protection?**

**Information Protection** in Microsoft Purview is about:

> **Classifying, labeling, and encrypting data — automatically or manually — to protect it throughout its lifecycle, inside or outside your organization.**

No matter where the data goes — to a USB drive, to an external email, or uploaded to a third-party service — **protection stays with the data**.

This is often called **persistent protection**.

**Key point:**\
Information Protection ensures sensitive data is **only accessible** to **authorized people** — at rest, in transit, and in use.

***

### **How Information Protection Works**

When you apply a **sensitivity label** to a document, email, or file, it can trigger:

* **Classification**: Tagging the file as "Confidential," "Restricted," etc.
* **Encryption**: Protecting the file so only authorized users/groups can open it.
* **Access Controls**: Restricting who can edit, print, copy, or forward the file.
* **Visual Markings**: Adding headers, footers, or watermarks (e.g., "Confidential").

Information Protection applies across:

* Microsoft 365 apps (Word, Excel, Outlook, PowerPoint)
* SharePoint, OneDrive
* Microsoft Teams
* Windows devices
* Mobile devices (iOS/Android)
* Non-Microsoft apps (Adobe Reader, etc.)

***

### **What is Encryption?**

Encryption is the process of:

> **Converting data into an unreadable format unless the correct key is used to decrypt it.**

In Purview:

* Encryption is **automatic** based on the sensitivity label applied.
* Encryption can **control access** even if the file leaves your network.
* Encryption keys can be **managed by Microsoft** or **you can bring your own keys** (BYOK or DKE).

**Real-World Example:**\
If someone accidentally forwards a confidential Excel file to a personal Gmail account, the file remains **encrypted** and **unreadable** without the right authorization.

***

### **Types of Encryption in Microsoft Purview**

| Encryption Type                 | Description                                                               |
| ------------------------------- | ------------------------------------------------------------------------- |
| **Microsoft-Managed Keys**      | Microsoft controls the encryption keys automatically.                     |
| **Bring Your Own Key (BYOK)**   | You supply your own encryption keys stored in Azure Key Vault.            |
| **Double Key Encryption (DKE)** | You hold one key, Microsoft holds the other — both are needed to decrypt. |
| **Customer Key (CK)**           | You manage a second layer of encryption for Microsoft 365 services.       |

> **Important:**\
> DKE is useful for industries like financial services and government that require maximum control over data.

***

### **Sensitivity Labels and Encryption**

You can configure **Sensitivity Labels** to automatically apply encryption settings:

| Setting                                           | Example                                                    |
| ------------------------------------------------- | ---------------------------------------------------------- |
| **Only people inside my organization can access** | Encrypt a document so only employees can open it.          |
| **Specific users or groups**                      | Allow only the finance department to access a budget file. |
| **Expire access after a certain time**            | Allow vendors to access a contract for 30 days only.       |
| **Restrict permissions**                          | Allow viewing but block editing, copying, or printing.     |

You can **combine encryption settings with user actions** (e.g., "Allow user to set Do Not Forward in Outlook").

***

### **How Labels Apply Protection Automatically**

**Auto-labeling policies** in Microsoft Purview can detect sensitive content and apply encryption automatically

4o

**You said:**

Write 7

**ChatGPT said:**

Of course! Here’s the full **Module 7: Information Protection and Encryption** properly completed for your course:

***

## **Module 7: Information Protection and Encryption**

***

### **What is Information Protection?**

**Information Protection** in Microsoft Purview is the practice of:

> **Classifying, labeling, and encrypting data to protect it — wherever it travels — throughout its entire lifecycle.**

The goal is to ensure that sensitive information stays protected whether it is **inside** your organization's systems or **outside** (like when sent through email or downloaded onto a USB drive).

> **Important:**\
> Microsoft Purview’s Information Protection _travels with the data_. Even if the data leaves your environment, the protection policies stay attached.

***

### **How Information Protection Works**

When you apply a **Sensitivity Label**, you can automatically:

* **Classify** the data (e.g., Internal, Confidential, Highly Confidential).
* **Protect** the data using **encryption** and **rights management**.
* **Control** what users can do with the data (view, edit, print, copy).
* **Mark** the data visually (headers, footers, watermarks).

This protection is enforced across:

* Microsoft 365 apps (Word, Excel, Outlook, PowerPoint)
* SharePoint Online and OneDrive for Business
* Microsoft Teams chats and files
* Windows, Mac, iOS, Android devices

**Example:**\
If a file labeled "Confidential" is emailed externally, it will remain encrypted and inaccessible to unauthorized users.

***

### **What is Encryption?**

**Encryption** transforms readable data into unreadable ciphertext.\
Only those with the correct decryption keys can access the original data.

In Purview:

* Encryption happens **automatically** based on policies.
* Labels can specify **who** can access the content (specific users, domains, groups).
* Encryption **stays with the file** even if it is downloaded, emailed, or shared outside the company.

***

### **Types of Encryption in Microsoft Purview**

| Encryption Type                 | Description                                                                                          |
| ------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Microsoft-Managed Keys**      | Microsoft fully manages and rotates the encryption keys for you.                                     |
| **Bring Your Own Key (BYOK)**   | You manage the encryption keys via Azure Key Vault. Microsoft uses your key to encrypt/decrypt data. |
| **Double Key Encryption (DKE)** | You and Microsoft each hold a separate key. Both keys are required to access the data.               |
| **Customer Key (CK)**           | Adds a second layer of encryption over Microsoft’s standard encryption for more control.             |

> **Key Tip:**\
> **DKE** is best when you want to prevent even Microsoft from being able to access your encrypted data.

***

### **Sensitivity Labels and Encryption**

When you create a **Sensitivity Label**, you can **configure it to apply encryption settings** automatically.

**Label Settings Options:**

| Setting                                       | What It Does                                           | Example                                                    |
| --------------------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------- |
| **Restrict access to specific people/groups** | Only allow intended recipients to open the file/email. | Only the HR group can open a personnel file.               |
| **Allow offline access**                      | Control whether users can access the file offline.     | Prevent offline access to "Highly Confidential" documents. |
| **Set expiration date**                       | Revoke access after a certain time.                    | Vendors' access to a file expires after 30 days.           |
| **Restrict permissions**                      | Control editing, copying, printing, and forwarding.    | Users can view but cannot print a sensitive document.      |

You can also allow users to **override** the settings if needed (with justification).

***

### **Auto-labeling with Information Protection**

You don’t have to rely solely on users to manually apply labels.\
You can create **auto-labeling policies** based on:

* **Sensitive Information Types (SITs)** (e.g., detecting credit card numbers, SSNs)
* **Keywords or phrases** (e.g., "Confidential Project")
* **Document properties** (e.g., owner, department)
* **Trainable classifiers** (machine learning models trained to recognize types of content)

**Example Auto-Labeling Policy:**

* If a document contains more than **one credit card number**, automatically apply the **"Highly Confidential"** label and encrypt it.

Auto-labeling ensures that **even if users forget**, **Purview still protects the data**.

***

### **Visual Markings**

Sensitivity labels can also apply **visual markings** like:

* **Headers** (e.g., "Confidential")
* **Footers** (e.g., "Company Confidential - Do Not Distribute")
* **Watermarks** (e.g., "Draft" across the background)

These visual cues help users understand the sensitivity of the data at a glance.

**Example:**\
You apply a "Confidential" label to a Word document — it adds a **Confidential** header to each page and a **watermark** saying **Internal Use Only**.

***

### **Hands-On Lab: Create a Sensitivity Label with Encryption**

**Objective:**\
Create and publish a Sensitivity Label that encrypts documents and restricts access to internal users only.

#### Step 1: Create the Label

1. Go to the [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Navigate to **Information Protection** → **Labels**.
3. Click **Create a label**.
4. Name: **Internal Only**\
   Description: **Encrypt files and emails, internal use only.**

#### Step 2: Configure Protection Settings

* Enable **Encryption**.
* Set permissions to **Only people inside my organization**.
* Allow users to **view and edit**, but **block forwarding** on emails.

#### Step 3: Publish the Label

* Create a **Label Policy** to publish the label.
* Assign it to a group of test users.
* Save and publish.

#### Step 4: Test

* Open Word or Outlook.
* Apply the **Internal Only** label.
* Try sending it externally — external recipients should be **blocked** or **prompted** for credentials they don’t have.

***

### **Summary**

* **Information Protection** in Microsoft Purview allows you to classify, label, encrypt, and protect data automatically.
* **Sensitivity Labels** can enforce encryption and access restrictions.
* **Encryption** ensures only authorized people can read sensitive files or emails — even outside your network.
* **Auto-labeling** protects data without relying only on users.
* **Visual markings** (headers, footers, watermarks) make sensitivity obvious to users.
