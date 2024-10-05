# Connectors

Azure Logic Apps' **built-in connectors** allow you to interact with a wide range of services without needing to write custom code. These connectors are critical for integrating different platforms, automating workflows, and building threat-hunting workflows in your security environment. In this module, we’ll focus on how to use built-in connectors in Logic Apps, with examples geared toward security and threat-hunting.

## **What Are Connectors in Logic Apps?**

**Connectors** are pre-built integrations that allow Logic Apps to communicate with external services. They allow you to:

* **Trigger workflows** when events occur in other services (e.g., an alert from Azure Sentinel).
* **Perform actions** like sending an email, querying a database, or creating tickets in service desk systems (e.g., ServiceNow, Jira).
* **Automate tasks** across cloud services, on-premises systems, databases, and more.

Azure Logic Apps has hundreds of connectors, including those for Microsoft services (like Azure Sentinel, Microsoft Defender, Office 365) as well as third-party services (like Slack, VirusTotal, and PagerDuty).

### **1. Types of Connectors**

Logic Apps provides two main types of connectors:

1. **Built-In Connectors**: These are natively provided within Logic Apps and don’t require any additional setup.
   * Examples: **HTTP**, **Outlook**, **Office 365**, **SQL Server**, **Azure Storage**.
2. **Managed Connectors**: These are provided by Azure and typically connect to external services or APIs. Some require additional configuration or authentication.
   * Examples: **Azure Sentinel**, **Microsoft Defender**, **VirusTotal**, **ServiceNow**, **Slack**.

For threat-hunting purposes, the most relevant connectors are likely those that integrate with security services (e.g., Azure Sentinel, Microsoft Defender), logging platforms (e.g., Azure Monitor), and notification or response platforms (e.g., Teams, PagerDuty).

### **2. Adding and Configuring Built-In Connectors**

Let’s explore how to add and configure built-in connectors for your Logic App workflows.

**Example 1: Integrating with Azure Sentinel Using a Built-In Connector**

In this example, we will use the **Azure Sentinel** connector to trigger a workflow when a new security incident is detected.

1. **Open Your Logic App**:
   * In the Azure Portal, navigate to the **Logic Apps Designer**.
   * Create a new Logic App or open an existing one.
2. **Search for the Connector**:
   * In the **Triggers** section, search for the **Azure Sentinel** connector.
   * Select **When a response to an Azure Sentinel alert is triggered**.
3. **Configure the Connector**:
   * You’ll need to authenticate the connector by signing in to your Azure Sentinel workspace.
   * Specify any conditions for when the trigger should activate. For example, set it to trigger only for **high-severity alerts**.

**Example 2: Sending Notifications Using the Outlook Connector**

After a security alert is triggered, you might want to notify your security team. Here’s how to use the built-in **Outlook** connector to send an email when a security incident occurs.

1. **Add an Action**:
   * After adding the trigger, click **New Step** to add an action.
   * Search for **Outlook** and select **Send an email (V2)**.
2. **Configure the Action**:
   * Sign in to your Outlook or Office 365 account to authenticate the connector.
   * Fill out the **To**, **Subject**, and **Body** fields. Use dynamic content to include information about the security alert.
     * Example subject: "Security Incident Detected: @{triggerBody()?\['AlertName']}"
     * Example body: "A security alert of severity @{triggerBody()?\['Severity']} has been detected in Azure Sentinel."
3. **Test the Workflow**:
   * Once configured, save your Logic App and test it by triggering a security alert in Azure Sentinel. You should receive an email notification based on the alert details.

### **3. Common Security-Related Built-In Connectors**

For threat-hunting workflows, you’ll often work with connectors for services like Azure Sentinel, Microsoft Defender, or third-party security tools. Here’s a list of common connectors used in security automation:

**Security Connectors:**

* **Azure Sentinel**: Trigger workflows when new security incidents are detected or alerts are generated.
* **Microsoft Defender for Cloud**: Trigger workflows based on security recommendations or alerts from your cloud environment.
* **VirusTotal**: Enrich security alerts by querying VirusTotal for threat intelligence on suspicious IPs, URLs, or files.

**Communication & Notification Connectors:**

* **Microsoft Teams**: Automatically send messages to a Teams channel when a critical security event occurs.
* **Outlook/Office 365**: Send email notifications to security teams with details of incidents and threats.
* **Slack**: Notify your team in Slack when a new security alert is detected.

**Operations & Ticketing Connectors:**

* **ServiceNow**: Create a ticket automatically when a new incident is detected.
* **Jira**: Log security issues and assign them to the appropriate teams for investigation.

**Database & Storage Connectors:**

* **SQL Server**: Store threat data in an on-premises or cloud-hosted SQL database.
* **Azure Blob Storage**: Save log files, threat data, or reports in Azure Blob Storage for further analysis.

### **4. Working with Dynamic Content in Connectors**

One of the most powerful aspects of using built-in connectors is the ability to use **dynamic content**. Dynamic content allows you to pass data from previous steps in your workflow into subsequent actions. This is critical in threat-hunting workflows, where you may need to enrich alerts with additional information or send detailed reports based on security incidents.

**Example: Using Dynamic Content from Azure Sentinel Alerts**

1. **Trigger**: You’ve already set up a trigger for an Azure Sentinel alert.
2. **Add an Action**: Use the **HTTP** connector to make a web request to VirusTotal or another threat intelligence service to check the reputation of a suspicious IP address.
3. **Configure Dynamic Content**:
   * In the HTTP action, you can insert the IP address from the Azure Sentinel alert using dynamic content. Click **Add dynamic content** and select the IP address field from the alert payload.
4. **Use Results in Subsequent Actions**:
   * After receiving the response from the HTTP action, you can use the result (e.g., whether the IP is flagged as malicious) in the next step, such as sending an alert to the security team or logging the information in a database.

### **5. Creating Custom Connectors**

In some cases, you might need to integrate with a service that doesn’t have a built-in or managed connector. In such cases, you can create a **Custom Connector** that allows Logic Apps to interact with virtually any web API.

**Steps to Create a Custom Connector:**

1. **API Definition**:
   * Identify the web API you want to connect to and ensure it supports RESTful communication and authentication.
2. **Build the Connector**:
   * In the Azure Portal, go to **Logic Apps** and search for **Custom Connector**.
   * Define the API endpoints, methods (GET, POST, etc.), and authentication mechanisms (such as OAuth 2.0).
3. **Use the Custom Connector**:
   * Once the custom connector is built, you can use it just like any other connector in your Logic Apps workflow.

**Example:**

* If you're working with a proprietary threat intelligence platform or a security monitoring tool that isn’t directly supported by Logic Apps, you can create a custom connector to query that platform’s API and integrate the results into your workflows.

### **6. Error Handling in Connectors**

When working with external services via connectors, it’s important to handle potential errors gracefully. Logic Apps offers built-in **error handling** mechanisms to deal with failed API calls, timeouts, or other issues that might occur during workflow execution.

**Example: Handling Failed HTTP Requests**

1. Add an **HTTP** action to make a request to an external threat intelligence service.
2. Click on the **ellipsis (three dots)** next to the action and select **Configure run after**.
3. Choose the option **has failed** to handle the case where the HTTP request fails. You can then define alternative actions, such as logging the error or sending an alert to the security team.
