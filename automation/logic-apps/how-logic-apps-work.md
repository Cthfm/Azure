# How Logic Apps Work

Logic Apps consist of workflows made up of **Triggers** and **Actions**, allowing security teams to automate processes such as detecting security threats, responding to incidents, and orchestrating security tools. Let's review the key concepts of a Logic App.

## **Key Concepts:**

1. **Workflows**:
   * A Logic App workflow is a sequence of steps that automate tasks or processes. For threat hunting, these workflows can be used to automate responses to suspicious activity, such as blocking an IP address, querying threat intelligence databases, or generating alerts.
2. **Triggers**:
   * **Triggers** are events that start the Logic App workflow. In threat hunting, triggers might be a new security alert, a suspicious event in logs, or a scheduled check for threats.
   * Logic Apps offers two types of triggers:
     1. **Polling Triggers**: Regularly check a data source for new information (e.g., query logs every 5 minutes to check for specific indicators of compromise).
     2. **Push Triggers**: Automatically respond to events (e.g., trigger a workflow when Azure Sentinel generates a new alert).
3. **Actions**:
   * **Actions** are the steps performed after a trigger is fired. In threat-hunting scenarios, actions could include anything from sending an alert, executing a security query, blocking a malicious IP, or quarantining a compromised machine.
   * You can add multiple actions in a workflow to create complex automations, such as:
     * **Run Queries**: Automatically query logs or threat intelligence feeds.
     * **Enrich Data**: Enhance a security event by pulling additional information from external sources (e.g., reputation checks on IP addresses or file hashes).
     * **Remediate Threats**: Execute actions to block or mitigate threats in real-time.

## **Key Components for Threat Hunting Workflows:**

1.  **Triggers in Threat Hunting**:

    * **Azure Sentinel Alert Trigger**: Automatically start a workflow when an alert is generated in Azure Sentinel. This is commonly used in incident response scenarios.
    * **HTTP Trigger**: Receive HTTP requests from other systems (such as security appliances or custom threat intelligence platforms) to start a workflow. For example, a custom script could send a security event to Logic Apps to trigger an investigation.
    * **Recurrence Trigger**: Schedule regular threat-hunting workflows to run at specific intervals. This is useful for daily or weekly automated threat checks, such as reviewing audit logs or checking for failed login attempts.

    **Example**: A Logic App that is triggered every 15 minutes to query Azure Sentinel for high-priority alerts, and automatically escalate them to the security team for further investigation.
2.  **Actions in Threat Hunting**:

    * **Query Security Logs**: Use actions to query logs from Azure Monitor, Office 365, or other connected services for suspicious behavior. For example, you could automatically search for failed login attempts across multiple regions in your organization.
    * **Send Notifications**: Automatically send alerts or notifications (via email, SMS, or Microsoft Teams) when a potential threat is detected. Security teams can be instantly notified of critical incidents without manual intervention.
    * **Automated Remediation**: Perform security actions like blocking an IP address, disabling a user account, or triggering a script to quarantine a compromised device. These actions can be integrated directly into your Logic App workflow.
    * **Integrate Threat Intelligence**: Use Logic Apps to pull data from threat intelligence feeds like VirusTotal, MISP, or others, allowing you to enrich security events with contextual information.

    **Example**: After an IP address is flagged as suspicious, a Logic App can automatically check the IP against a threat intelligence database and take predefined actions based on the response, such as blocking the IP if it has a high-risk score.
3.  **Conditions and Loops**:

    * **Conditions** allow you to introduce decision-making into your workflows. For instance, you can create a condition that checks if an IP is blacklisted in a threat intelligence database, and then decide whether to block it or escalate it.
    * **Loops** enable you to repeat actions for multiple items. This is useful in threat hunting when analyzing multiple log entries, IPs, or alerts in a single workflow.

    **Example**: You could create a loop that iterates through a list of suspicious IP addresses from a log and checks each one against a threat intelligence feed, blocking any IP that is found to be malicious.
4. **Parallel Execution**:
   * Logic Apps allow actions to run in parallel, speeding up workflows that involve multiple steps. For example, while querying threat intelligence feeds, you could also be triggering an investigation in Azure Sentinel and notifying your security team at the same time.

### **Key Components for Advanced Threat Hunting:**

1.  **Variables and Data Handling**:

    * You can store data in variables for later use in your workflow. In threat hunting, variables might store details like a suspicious user’s name, an IP address, or the results of a threat intelligence query. You can reference these variables throughout your workflow for decisions and actions.

    **Example**: Store the results of a log query in a variable and use that information to determine whether to escalate the incident or close the alert.
2.  **Custom Connectors and APIs**:

    * Logic Apps can integrate with third-party APIs using custom connectors. This is particularly useful in security scenarios where your team might need to integrate with specialized threat intelligence platforms, incident management systems, or internal APIs.

    **Example**: Build a custom connector to interact with a proprietary threat intelligence platform, enabling the Logic App to enrich security incidents with the latest threat data.
3. **Error Handling and Retry Policies**:
   * Built-in error handling allows Logic Apps to gracefully handle failures. For example, if a workflow fails to connect to a threat intelligence API, it can automatically retry or notify the team of the issue.

## **How Logic Apps Work in a Threat-Hunting Scenario:**

**Scenario**: Automating Threat Response for Failed Login Attempts

1. **Trigger**: A Logic App is set to trigger when Azure Sentinel detects five failed login attempts from a specific user in a short time frame.
2. **Action 1**: The Logic App automatically queries an external threat intelligence service to check if the source IP of the login attempts is known for malicious activity.
3. **Action 2**: If the IP is flagged as malicious, the Logic App blocks the IP address in the company’s firewall and disables the user account temporarily.
4. **Action 3**: The Logic App sends an alert to the security team via Microsoft Teams, detailing the incident and providing context from the threat intelligence query.
5. **Action 4**: The Logic App logs all actions taken and updates the incident in the company’s ticketing system for further investigation.
