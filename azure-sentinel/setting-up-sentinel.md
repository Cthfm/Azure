---
hidden: true
---

# Setting up Sentinel

### **Setting Up an Azure Subscription**

Before you can deploy Sentinel, you need an active **Azure Subscription**.

**Options:**

* **Free Trial:** $200 credits for 30 days.
* **Pay-As-You-Go:** Billed monthly based on usage.
* **Microsoft 365 E5 or Azure Trial Bundles:** Some licenses bundle Azure credits.

**Critical Setup for Defenders:**

* **Global Administrator** or **Owner** permissions are needed to create resources.
* Billing alerts should be configured if working with trial subscriptions.

> **Tip:** Always label your resources properly (e.g., "Environment: Production," "Owner: Security Team") for easier management.

***

### **Lesson 2.2: Setting Up a Log Analytics Workspace**

**Why:**\
Microsoft Sentinel is _built on top of_ Azure Log Analytics. Every log that Sentinel collects is stored inside a **Log Analytics Workspace**.

**Steps to Create a Workspace:**

1. Go to the **Azure Portal**.
2. Search for **Log Analytics Workspaces**.
3. Click **Create**.
4. Fill in:
   * **Subscription**
   * **Resource Group** (create a new one like `Sentinel-Resources`)
   * **Name** (e.g., `Production-Sentinel-Workspace`)
   * **Region** (must match region for other resources you’ll monitor)
5. Review + Create.

**Workspace Settings to Check:**

* **Retention Period:** Default is 30 days; you can extend it (costs extra).
* **Pricing Tier:** Usually Pay-As-You-Go or Commitment Tiers.

> **Detection Engineering Tip:**\
> Choose a region closest to your users to minimize latency in hunting and querying logs.

***

### **Lesson 2.3: Onboarding Microsoft Sentinel**

Once you have a Workspace:

**Steps to Enable Sentinel:**

1. Go to **Azure Portal** → **Microsoft Sentinel**.
2. Click **+ Add**.
3. Select your Log Analytics Workspace.
4. Sentinel will now be attached and ready.

**Initial Setup Tasks:**

* Install **Solutions** (bundles of connectors, workbooks, analytics rules).
* Set up **Data Connectors** to start ingesting logs.
* Configure **Permissions** for your SOC Team.

**Core Sentinel Menu Areas:**

| Area           | Purpose                                 |
| -------------- | --------------------------------------- |
| **Overview**   | See total incidents, alerts, automation |
| **Logs**       | Write and run KQL queries               |
| **Analytics**  | Manage detection rules                  |
| **Incidents**  | Investigate and triage threats          |
| **Workbooks**  | Build dashboards and visualizations     |
| **Hunting**    | Proactively search for threats          |
| **Automation** | Build Playbooks for auto-response       |

> **SOC Tip:** Always verify your Sentinel instance is attached to the correct workspace before you connect data sources.

### **Assigning Permissions and RBAC**

**Azure Role-Based Access Control (RBAC)** controls who can do what inside Sentinel.

**Key Built-in Roles:**

| Role                                          | Responsibilities                               |
| --------------------------------------------- | ---------------------------------------------- |
| **Microsoft Sentinel Reader**                 | View incidents, alerts, and dashboards         |
| **Microsoft Sentinel Responder**              | Investigate and update incidents               |
| **Microsoft Sentinel Contributor**            | Create rules, playbooks, workbooks             |
| **Microsoft Sentinel Automation Contributor** | Manage playbooks only                          |
| **Log Analytics Reader**                      | Query logs but can’t manage Sentinel resources |

**Practical Mapping:**

| Team Member        | Recommended Role                  |
| ------------------ | --------------------------------- |
| SOC Tier 1 Analyst | Sentinel Reader                   |
| SOC Tier 2 Analyst | Sentinel Responder                |
| Incident Responder | Sentinel Responder or Contributor |
| Detection Engineer | Sentinel Contributor              |
| Playbook Developer | Sentinel Automation Contributor   |

**Steps to Assign Roles:**

1. Azure Portal → **Microsoft Sentinel** → **Access control (IAM)**.
2. Click **+ Add → Add role assignment**.
3. Choose appropriate role and assign it to users/groups.
