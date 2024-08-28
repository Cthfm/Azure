# Alerts

## Azure Monitor Alert Overview

Azure Monitor Alerts are a feature within Azure Monitor, designed to proactively notify you of potential issues, suspicious activities, and security threats in your Azure environment.&#x20;

### Key Concepts for Alerts in Azure Monitor

1. **Define Alert Criteria**: Identify the specific conditions that should trigger an alert based on your threat-hunting objectives.
2. **Create Alert Rules**: Configure alert rules to specify the conditions and actions for the alerts.
3. **Set Up Action Groups**: Define the actions to take when an alert is triggered, such as sending notifications or executing automated responses.
4. **Monitor and Refine**: Continuously monitor the effectiveness of your alerts and refine them as needed.

### Step-by-Step Guide to Creating Alerts

**Step 1: Access Azure Monitor**

1. **Log in to Azure Portal**: Go to [Azure Portal](https://portal.azure.com) and log in with your credentials.
2. **Navigate to Azure Monitor**: Use the search bar to find and select "Azure Monitor".

**Step 2: Define Alert Criteria**

Determine the specific conditions that you want to monitor. Common criteria for threat hunters include:

* Multiple failed login attempts.
* Unusual access patterns.
* High-severity security alerts.

**Step 3: Create Alert Rules**

1. **Go to Alerts**: In the Azure Monitor overview pane, select "Alerts".
2. **Create New Alert Rule**:
   * Click on **New Alert Rule**.
   * Select the target resource (e.g., a Log Analytics Workspace, virtual machine, or specific Azure resource).
3. **Define the Condition**:
   * Click on **Add condition**.
   * Select the appropriate signal type (e.g., log search, metric, activity log).
   *   Use Kusto Query Language (KQL) to define the specific condition. For example, to detect multiple failed login attempts:

       ```kusto
       SecurityEvent
       | where EventID == 4625
       | summarize FailedLogins = count() by bin(TimeGenerated, 1h), IPAddress
       | where FailedLogins > 10
       ```
4. **Configure Alert Details**:
   * Provide a name and description for the alert rule.
   * Set the severity level (e.g., Sev 0 - Critical, Sev 1 - Warning, etc.).
   * Define the evaluation criteria (e.g., how often the condition should be evaluated).

**Step 4: Set Up Action Groups**

1. **Add Action Group**:
   * In the alert rule creation pane, click on **Add action group**.
   * Create a new action group or select an existing one.
2. **Define Actions**:
   * Configure the actions to take when the alert is triggered. Common actions include:
     * Sending email notifications to specific recipients.
     * Sending SMS messages.
     * Triggering a Logic App to automate response actions (e.g., blocking an IP address).
     * Running an Azure Automation runbook to execute custom scripts.
   * Provide necessary details for each action type (e.g., email addresses, phone numbers, or Logic App URIs).

**Step 5: Review and Create**

1. **Review Alert Rule**:
   * Review the configured alert rule, conditions, and actions.
2. **Create Alert Rule**:
   * Click on **Create** to save and activate the alert rule.

#### Example Alert Scenarios

**Multiple Failed Login Attempts**

1. **Condition**:
   *   KQL Query:

       ```kusto
       SecurityEvent
       | where EventID == 4625
       | summarize FailedLogins = count() by bin(TimeGenerated, 1h), IPAddress
       | where FailedLogins > 10
       ```
2. **Action**:
   * Send email notification to the security team.
   * Trigger a Logic App to block the offending IP address.

**High-Severity Security Alerts**

1. **Condition**:
   *   KQL Query:

       ```kusto
       SecurityAlert
       | where Severity == "High"
       | summarize count() by bin(TimeGenerated, 1h), AlertName
       ```
2. **Action**:
   * Send SMS notification to the on-call security analyst.
   * Trigger an Azure Automation runbook to collect additional forensic data.

### Monitoring and Refining Alerts

1. **Monitor Alert Effectiveness**:
   * Regularly review the alerts to ensure they are firing as expected and providing useful information.
2. **Refine Alert Conditions**:
   * Adjust the alert conditions and thresholds based on observed patterns and feedback to reduce false positives and improve accuracy.
3. **Update Action Groups**:
   * Periodically review and update the action groups to ensure that the correct contacts and response actions are in place.
