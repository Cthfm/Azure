# Triggers

**Triggers** are an essential component in Azure Logic Apps, as they initiate the workflow. Triggers can either be **event-based**, meaning they activate when a certain event occurs (such as receiving an email or detecting a security alert), or **time-based**, activating on a predefined schedule.

### **Types of Triggers in Logic Apps**

1. **Event-Based Triggers**: These triggers fire when a specific event happens. In the context of threat hunting, these could include:
   * **Security alerts** from tools like Azure Sentinel or Microsoft Defender.
   * **Data ingestion** triggers when new log data is uploaded or available for analysis.
   * **Changes to resources** such as file uploads, configuration changes, or service account modifications.
2. **Time-Based (Recurrence) Triggers**: These triggers fire based on a schedule. They’re often used for periodic threat-hunting tasks, such as:
   * Running security scans every hour.
   * Querying logs for suspicious activity daily.
   * Automating data enrichment tasks at regular intervals.

### **1. Event-Based Triggers**

**Event-based triggers** respond to a specific event happening in a connected service. In security automation workflows, this is especially useful for real-time monitoring and immediate responses to security incidents.

**Example: Triggering a Workflow on a Security Alert**

In this example, you’ll use **Azure Sentinel** as the source of a trigger. The goal is to automatically trigger a workflow when a **high-severity security alert** is raised.

**Steps:**

1. **Select the Trigger**:
   * In the Logic Apps Designer, search for the **Azure Sentinel** connector.
   * Choose the trigger **When a response to an Azure Sentinel alert is triggered**.
2. **Configure the Trigger**:
   * You’ll be prompted to sign in to Azure Sentinel and select the correct **Log Analytics Workspace**.
   * Specify the conditions under which this trigger should fire. For example:
     * Only trigger when the **Alert Severity** is high.
     * Target specific **Alert Rules**, such as those related to brute-force attempts or malware detection.
3. **Next Steps**:
   * After setting up the trigger, you can define actions such as:
     * Automatically sending notifications to the security team.
     * Triggering threat intelligence enrichment workflows.
     * Logging the incident in a security information and event management (SIEM) platform.

### **2. Time-Based Triggers (Recurrence)**

**Time-based triggers**, also known as **recurrence triggers**, are useful for regularly scheduled threat-hunting tasks or security checks. For example, you might want to automatically query log data every hour to search for patterns of suspicious activity or check for anomalies.

**Example: Querying Logs Every Hour**

In this example, we’ll set up a time-based trigger to query Azure Monitor logs every hour for any failed login attempts, which can be an indicator of a brute-force attack.

**Steps:**

1. **Select the Trigger**:
   * In the Logic Apps Designer, search for the **Recurrence** trigger.
   * Select **Recurrence** (trigger a workflow based on a time schedule).
2. **Configure the Trigger**:
   * Set the **Frequency** to “Hour”.
   * Set the **Interval** to “1” (i.e., the workflow will run every hour).
3.  **Add an Action**:

    * After defining the trigger, add an action that queries **Azure Monitor Logs** or **Azure Sentinel** for any failed login attempts.
    * You can use **KQL queries** (Kusto Query Language) to search through the logs for specific patterns.

    Example KQL Query:

    ```kql
    SecurityEvent
    | where EventID == 4625 // Failed login attempt
    | summarize count() by Account, Computer, TimeGenerated
    ```
4. **Next Steps**:
   * After querying the logs, you can set up actions based on the results:
     * Send a notification if there are more than a certain number of failed attempts within the last hour.
     * Log the information in a separate database for further analysis.
     * Automatically block IP addresses involved in the failed login attempts.

### **3. Multi-Trigger Logic Apps**

You can also create Logic Apps that use **multiple triggers**. This is useful for more complex scenarios where you need to monitor multiple sources of events or combine triggers with scheduled activities.

**Example: Combining Event and Recurrence Triggers**

Imagine a situation where you want to continuously monitor for specific events but also run scheduled checks every hour. You could create a Logic App that:

* **Trigger 1**: Fires whenever a high-severity alert is raised in Azure Sentinel.
* **Trigger 2**: Runs every hour to scan logs for new indicators of compromise (IoCs).

When combining triggers, the Logic App is designed to run whenever any one of the triggers is activated. This allows you to create highly flexible workflows.

**Steps:**

1. **Add Multiple Triggers**:
   * In the Logic Apps Designer, add a new trigger for each event or schedule you want to monitor.
   * Ensure that each trigger is configured with its own conditions, such as specific alerts or recurrence intervals.
2. **Define Actions for Each Trigger**:
   * Based on which trigger is activated, you can customize the actions. For example, a workflow triggered by an Azure Sentinel alert might enrich the alert with threat intelligence, whereas a workflow triggered by the recurrence schedule might send a report of the hourly log scan results.

### **4. Customizing Trigger Conditions**

Triggers can be further customized using **conditions**. You might want to fire a trigger only when certain parameters are met, such as specific types of security alerts, or based on dynamic data values in your workflow.

**Example: Trigger a Workflow Only for Specific Alert Types**

1. **Define Trigger Conditions**:
   * When configuring the trigger, use **conditions** to narrow down when the workflow runs. For example, trigger the workflow only for alerts with a certain **alert type**, such as malware infections or brute-force attacks.
2. **Condition Expression**:
   * You can add expressions to filter based on dynamic content (e.g., only trigger if the **Alert Type** is equal to “BruteForce”).
   *   Example condition expression:

       ```json
       @equals(triggerBody()?['AlertType'], 'BruteForce')
       ```

By using conditions, you can ensure your Logic App is only triggered when specific security-related criteria are met, reducing unnecessary executions and alerts.

### **5. Testing and Monitoring Triggers**

After setting up your triggers, it's crucial to test and monitor them to ensure they are working as expected.

1. **Run Trigger Tests**:
   * Test your Logic App by triggering events manually (e.g., uploading files, sending alerts) or waiting for the recurrence schedule to fire.
2. **Monitor Trigger Execution**:
   * In the **Overview** tab of your Logic App, check the **Run History** to see when and how the Logic App was triggered.
   * Review the inputs and outputs of each trigger to ensure it captured the correct data and executed as expected.
