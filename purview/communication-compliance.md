# Communication Compliance

### **What is Communication Compliance?**

**Communication Compliance** in Microsoft Purview is a solution that:

> **Monitors internal and external communications across your organization to detect policy violations such as harassment, sensitive data sharing, or regulatory non-compliance.**

It helps organizations identify risky or inappropriate messages — **before** they escalate into **legal**, **reputational**, or **compliance issues**.

**Think of it like this:**\
Communication Compliance **supervises** communications and flags content that violates your organization’s policies.

***

### **Why Communication Compliance Matters**

| Reason                            | Example                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| **Prevent Harassment**            | Detect inappropriate or offensive language in Teams chats or emails.                    |
| **Protect Sensitive Information** | Catch accidental or intentional sharing of confidential data over email or Teams.       |
| **Support Regulatory Compliance** | Meet supervision requirements in industries like financial services (FINRA, SEC, GDPR). |
| **Improve Company Culture**       | Maintain a safe, inclusive, and respectful work environment.                            |

Organizations are often legally **required** to supervise communications under industry regulations.

***

### **How Communication Compliance Works**

**Communication Compliance** monitors communications across:

* **Microsoft Teams** chats
* **Outlook** emails
* **Yammer** posts
* **Skype for Business** (if still in use)
* **LinkedIn messages** (only when linked to a corporate account)

It does so by:

1. **Scanning communications** for specific keywords, patterns, or sensitive data.
2. **Detecting matches** based on policy definitions.
3. **Flagging content** for review by authorized reviewers (compliance officers, managers).
4. **Allowing reviewers** to investigate and take action (e.g., escalate, dismiss, notify user).

> **Important:**\
> Like Insider Risk Management, Communication Compliance also protects **user privacy** through role-based access, auditing, and user anonymization.

***

### **Policy Templates Available**

Microsoft Purview offers several **pre-built policy templates** to help you get started quickly:

| Template Name                     | Description                                                             |
| --------------------------------- | ----------------------------------------------------------------------- |
| **Offensive Language**            | Detects profane, obscene, or abusive language.                          |
| **Adult Content**                 | Detects sexual or explicit content.                                     |
| **Harassment**                    | Detects harassment, threats, bullying, or discrimination.               |
| **Sensitive Information Sharing** | Detects sharing of financial, healthcare, or confidential company data. |
| **Regulatory Compliance**         | Designed for highly regulated industries (FINRA, SEC).                  |

You can **customize** or **create your own** policies as well.

***

### **Communication Compliance Workflow**

1. **Create a Policy**\
   Define what you want to supervise (e.g., harassment detection).
2. **Assign Reviewers**\
   Choose who will review flagged communications.
3. **Define Scoping Rules**\
   Specify which users, groups, or locations to supervise (e.g., executive team, sales department).
4. **Select Detection Methods**\
   Use built-in classifiers, custom keywords, sensitive information types, or exact data match (EDM).
5. **Review Flagged Communications**\
   Reviewers assess flagged content to determine if action is needed.
6. **Take Actions**\
   Possible actions include dismissing the alert, escalating it, notifying the user, or launching a full investigation.

***

### **Built-in Classifiers**

Communication Compliance uses **Microsoft’s pre-trained machine learning models** to detect sophisticated risks.

| Classifier Name              | What It Detects                                |
| ---------------------------- | ---------------------------------------------- |
| **Threat**                   | Threatening or aggressive language.            |
| **Harassment**               | Workplace bullying or harassment.              |
| **Profanity**                | Profane or obscene language.                   |
| **Confidential Information** | Sharing of confidential corporate data.        |
| **Offensive Terms**          | Inappropriate or culturally insensitive terms. |

Built-in classifiers help **reduce false positives** compared to simple keyword-based policies.

***

### **Privacy and Reviewer Roles**

**User Privacy:**

* Messages are anonymized (User1, User2, etc.) until an investigation is escalated.
* Only **authorized reviewers** can see flagged communications.
* All reviewer actions are **audited** for compliance.

**Reviewer Roles:**

| Role                                      | Permissions                                               |
| ----------------------------------------- | --------------------------------------------------------- |
| **Communication Compliance Admin**        | Full access to configure policies and manage reviews.     |
| **Communication Compliance Investigator** | Can review flagged messages and take action.              |
| **Viewer**                                | Read-only access to flagged communications for oversight. |

**Tip:**\
Follow the **least privilege principle** — only assign reviewer roles to those who absolutely need them.

***

### **Hands-On Lab: Create a Communication Compliance Policy**

**Objective:**\
Create a policy to detect offensive language in Microsoft Teams chats.

#### Step 1: Create a Policy

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Go to **Communication Compliance** → **Policies** → **Create Policy**.
3. Choose the **Offensive Language** template.
4. Name your policy **Monitor Offensive Language in Teams**.

#### Step 2: Scope the Policy

* Apply it to the **Teams** workload.
* Choose a small test group (e.g., a few users) to minimize noise.

#### Step 3: Assign Reviewers

* Assign a **Communication Compliance Investigator** to review flagged content.

#### Step 4: Review Results

* Simulate a violation by sending a test message with offensive terms.
* Check if the policy flags it and routes it for review.

***

### **Summary**

* **Communication Compliance** monitors communications to detect risky, inappropriate, or non-compliant behavior.
* Microsoft provides **pre-built policy templates** and **intelligent classifiers** to help detect issues.
* Privacy is protected through **anonymization** and **role-based access control**.
* Reviewers can **dismiss**, **escalate**, or **take action** on flagged communications.
* Communication Compliance is crucial for maintaining **legal**, **ethical**, and **regulatory standards** in the modern workplace.

***

**End of Module 6**
