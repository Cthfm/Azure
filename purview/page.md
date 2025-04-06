# Page

## **Compliance Manager and Regulatory Compliance**

***

### **What is Compliance Manager?**

**Compliance Manager** is a **risk assessment tool** built into Microsoft Purview that helps you:

> **Continuously assess, monitor, and improve your compliance posture across Microsoft 365, Azure, and third-party services.**

It provides:

* A **real-time compliance score**
* **Actionable recommendations** to reduce risks
* **Pre-built templates** for regulations like GDPR, HIPAA, ISO 27001, NIST, etc.
* **Tracking and reporting** for internal audits or regulatory reviews

> **Key idea:**\
> Compliance Manager **shows you what controls you need to meet** a regulation — and **tracks your progress** toward meeting them.

***

### **Why Compliance Manager Matters**

| Reason                           | Example                                                               |
| -------------------------------- | --------------------------------------------------------------------- |
| **Meet Regulatory Requirements** | Prove compliance with GDPR, HIPAA, PCI-DSS, FedRAMP.                  |
| **Reduce Risk**                  | Identify gaps in your security and compliance posture.                |
| **Stay Audit-Ready**             | Maintain a clear, organized record of compliance efforts.             |
| **Prioritize Actions**           | Focus on tasks that have the biggest impact on your compliance score. |

Instead of guessing, Compliance Manager **shows exactly what you must do** to reduce risk.

***

### **How Compliance Manager Works**

1. **Select an Assessment Template**\
   Choose from a library of regulations and standards (e.g., GDPR, ISO 27001).
2. **Assign Improvement Actions**\
   Microsoft suggests specific actions to help you meet the regulation (e.g., encrypt email, enable MFA).
3. **Implement and Track Progress**\
   Complete actions, upload evidence (like screenshots or policies), and mark them as done.
4. **Monitor Your Compliance Score**\
   Compliance Manager gives you a numerical score to reflect your overall compliance posture.

***

### **What is a Compliance Score?**

The **Compliance Score** is a **numerical value** that reflects how well your organization is implementing recommended controls.

| Compliance Score Range | Meaning                                   |
| ---------------------- | ----------------------------------------- |
| 0–300                  | High Risk (Many gaps)                     |
| 300–700                | Moderate Risk (Some controls implemented) |
| 700–1000               | Low Risk (Most controls implemented)      |

Each **Improvement Action** you complete increases your score.

**Important:**\
The score is not a certification. It’s a **guidance metric** to show how close you are to meeting requirements.

***

### **Pre-built Assessment Templates**

Microsoft Purview provides **dozens** of ready-to-use templates.

| Regulation/Framework | Description                                                          |
| -------------------- | -------------------------------------------------------------------- |
| **GDPR**             | General Data Protection Regulation (EU).                             |
| **HIPAA**            | Health Insurance Portability and Accountability Act (US healthcare). |
| **ISO/IEC 27001**    | International security management standard.                          |
| **NIST 800-53**      | US government cybersecurity standard.                                |
| **CCPA**             | California Consumer Privacy Act.                                     |
| **FedRAMP**          | US federal government cloud authorization.                           |

You can use **one** or **multiple templates** depending on your industry and region.

***

### **Core Elements of an Assessment**

| Element                    | Description                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| **Controls**               | Requirements you must meet (e.g., "Encrypt sensitive data at rest"). |
| **Improvement Actions**    | Recommended steps to meet the controls.                              |
| **Testing Status**         | Indicates whether the action has been reviewed/tested.               |
| **Evidence**               | Documentation you upload to prove you completed an action.           |
| **Responsible User/Group** | Who is assigned to complete the action.                              |

Assessments can track hundreds of controls — **automating a lot of manual compliance work**.

***

### **Managing Improvement Actions**

Each **Improvement Action** includes:

* **Description**: What needs to be done.
* **Impact**: How much completing it improves your compliance score.
* **Status**: Not started, In progress, Implemented, or Resolved.
* **Evidence**: Supporting proof (documents, screenshots, policies).

> **Tip:**\
> Focus first on **high-impact actions** to quickly boost your compliance score.

You can also **filter actions** based on priority, location, service, or user assignment.

***

### **Automated Testing and Manual Testing**

* **Automated Testing**:\
  Compliance Manager automatically verifies whether certain actions are implemented (e.g., checking if MFA is enabled).
* **Manual Testing**:\
  Some actions (like writing a policy or conducting training) require you to manually upload evidence and mark them complete.

**Example:**\
Enabling Customer Lockbox in Microsoft 365 can be automatically tested.\
Documenting your Data Protection Policy requires manual evidence.

***

### **Hands-On Lab: Create a Compliance Assessment**

**Objective:**\
Set up a GDPR assessment in Compliance Manager and assign actions.

#### Step 1: Create an Assessment

1. Open [Microsoft Purview Compliance Manager](https://compliance.microsoft.com/).
2. Navigate to **Assessments** → **+ Add assessment**.
3. Choose **GDPR** as the template.
4. Name your assessment **GDPR 2025 Readiness**.

#### Step 2: Review Controls

* Browse through the list of GDPR-related controls.
* See which services (Exchange, SharePoint, OneDrive) are covered.

#### Step 3: Assign Improvement Actions

* Assign a few actions (like enabling auditing) to yourself or your team.
* Upload evidence if you complete any actions.

#### Step 4: Monitor Compliance Score

* Watch your compliance score improve as you complete tasks!

***

### **Summary**

* **Compliance Manager** helps you track, manage, and improve compliance against standards like GDPR, HIPAA, ISO 27001.
* **Assessments** organize controls into actionable steps.
* **Improvement Actions** guide your work toward better security and compliance.
* **Compliance Score** shows your progress at a glance.
* Using Compliance Manager helps you stay **audit-ready**, **reduce risk**, and **build customer trust**.
