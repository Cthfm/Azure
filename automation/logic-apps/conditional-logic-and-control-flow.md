# Conditional Logic and Control Flow

When building threat-hunting workflows or automating security responses, there will be situations where different actions need to be taken based on conditions or outcomes from earlier steps. **Conditional logic** and **control flow** in Azure Logic Apps allow you to implement decision-making capabilities within your workflows. This ensures that different actions are triggered depending on whether certain conditions are met, enabling more flexible and dynamic automation.

In this module, we will explore how to use conditional logic and control flow to enhance your workflows, with a focus on automating threat-hunting and security incident response tasks.

### **1. Overview of Conditional Logic in Logic Apps**

Conditional logic is essential for automating decisions in your workflows. You can build workflows that react to different inputs, such as the severity of a security alert or the result of a threat intelligence query.

In Azure Logic Apps, conditional logic is implemented using:

* **Conditions**: Basic "if-then-else" statements that allow actions to occur based on whether a specified condition is true or false.
* **Switch**: A statement that checks for multiple possible values and executes different actions for each value.
* **For Each**: A loop that iterates through an array of items and performs actions on each item.
* **Until**: A loop that runs until a specified condition is met.
* **Scope**: Used to group actions and handle errors or run them conditionally.

These controls help make workflows adaptable and capable of handling a wide range of scenarios, such as incident response based on the severity or type of security threats.

***

### **2. Implementing Conditions (If-Then-Else)**

A basic **Condition** in Logic Apps works similarly to traditional if-else statements in programming. You can use conditions to check whether specific data values meet certain criteria and trigger different workflows based on those criteria.

**Example: Responding to Security Alerts Based on Severity**

Suppose you want your Logic App to respond differently based on the severity of a security alert. For high-severity alerts, you might want to notify the security operations center (SOC) immediately, while for medium-severity alerts, you might simply log the incident.

**Steps:**

1. **Add a Condition**:
   * After adding a trigger (e.g., when a security alert is received from **Azure Sentinel**), click **New Step**.
   * Select **Control** and then **Condition**.
2. **Define the Condition**:
   * In the condition, specify the logic to check the alert severity. You can use dynamic content from the trigger (e.g., `@{triggerBody()?['Severity']}`).
   * Example: **If** the alert severity equals “High”.
3. **Define the Actions for True**:
   * If the condition evaluates as true (i.e., the severity is high), add actions such as:
     * Sending an email to the SOC team.
     * Triggering a containment workflow to isolate a compromised machine.
     * Creating a high-priority incident in **ServiceNow** or **Jira**.
4. **Define the Actions for False**:
   * If the condition is false (i.e., the severity is medium or low), you can:
     * Log the alert to a database.
     * Send a less urgent notification, or simply take no action.

**Condition Example in JSON:**

Here’s an example of how a condition might look in the Logic Apps designer:

```json
{
    "condition": {
        "expression": {
            "and": [
                {
                    "equals": [
                        "@triggerBody()?['Severity']",
                        "High"
                    ]
                }
            ]
        },
        "actions": {
            "ifTrue": [
                {
                    "action": "Send Email"
                }
            ],
            "ifFalse": [
                {
                    "action": "Log Incident"
                }
            ]
        }
    }
}
```

***

### **3. Using Switch for Multiple Conditions**

While a basic condition can handle true/false logic, the **Switch** control is used when you want to evaluate multiple possible values and execute different actions for each one. This is helpful when you have more than two outcomes.

**Example: Handling Different Types of Security Alerts**

Suppose you want your Logic App to handle different types of security alerts in various ways. For example:

* Brute-force attacks trigger an immediate response.
* Malware detection alerts trigger a virus scan.
* Phishing alerts notify users and flag the email.

**Steps:**

1. **Add a Switch Control**:
   * After your trigger, click **New Step**, then **Control**, and select **Switch**.
2. **Define the Switch Criteria**:
   * Set the switch to evaluate a field, such as the **Alert Type** (e.g., `@triggerBody()?['AlertType']`).
   * Add different cases for each alert type:
     * Case 1: **BruteForce** → Trigger an immediate response.
     * Case 2: **Malware** → Start a virus scan.
     * Case 3: **Phishing** → Notify the user.
3. **Set Default Case**:
   * You can also define a **default case** for any alerts that don’t match specific criteria. For example, you might log these alerts for manual investigation.

***

### **4. Looping with For Each**

In threat-hunting and security automation, you may need to process arrays of data, such as multiple security incidents, IP addresses, or users. The **For Each** control allows you to loop through an array and perform actions for each item.

**Example: Responding to Multiple Incidents**

Imagine your Logic App is triggered by a query to Azure Monitor that returns a list of security incidents. You want to evaluate each incident and respond accordingly.

**Steps:**

1. **Add a For Each Control**:
   * After your trigger (e.g., querying for incidents), add the **For Each** control.
   * Use dynamic content to set the array you want to loop through, such as a list of **Incidents**.
2. **Define Actions for Each Incident**:
   * Within the loop, you can evaluate each incident using conditions (e.g., check the severity or alert type).
   * For each incident, send notifications, log it, or trigger an automated response.
3. **Handle Parallel Processing**:
   * You can enable **parallelism** in the For Each loop to process multiple items simultaneously. This is useful when processing a large volume of data, such as multiple security alerts.

***

### **5. Using Until for Looping with Exit Conditions**

The **Until** control is a loop that runs until a specific condition is met. This is useful when you want to keep checking for a particular event or outcome, such as waiting for a file to be available or a security incident to be resolved.

**Example: Waiting for Incident Resolution**

In this example, a workflow could keep checking the status of an incident in ServiceNow until it is marked as resolved.

**Steps:**

1. **Add an Until Control**:
   * After the trigger, add an **Until** control.
   * Set the condition to continue looping until the **Incident Status** is “Resolved”.
2. **Configure Loop Actions**:
   * Inside the loop, you can query ServiceNow or another incident management system to check the status of the incident.
   * You can also include a **Delay** action to pause the workflow for a certain amount of time before rechecking the status.
3. **Exit the Loop**:
   * Once the condition is met (e.g., the incident is resolved), the loop exits, and you can take further actions like sending a notification or logging the resolution.

***

### **6. Grouping Actions with Scopes**

**Scopes** allow you to group multiple actions together. This is useful for organizing complex workflows or handling errors for a specific group of actions.

**Example: Grouping Actions for Error Handling**

You might have several actions that should all be executed as part of an incident response. If any of these actions fail, you want to handle the error gracefully.

**Steps:**

1. **Add a Scope**:
   * After your trigger, add a **Scope** control.
   * Add actions inside the scope, such as sending notifications, logging incidents, and querying external systems.
2. **Configure Error Handling**:
   * Set the **Run After** condition for the scope to define what happens if an error occurs in any of the actions.
   * For example, if any action within the scope fails, you can send an error notification or retry the workflow.

***

### **7. Best Practices for Conditional Logic and Control Flow**

When designing Logic Apps with conditional logic and control flow, keep the following best practices in mind:

* **Optimize Performance**: Use **For Each** loops with parallelism enabled when processing large datasets to avoid slow workflows.
* **Reduce Noise**: Use conditions and switches to ensure that only relevant alerts trigger actions, preventing unnecessary notifications or actions.
* **Error Handling**: Always implement error handling using **Scopes** or **Run After** configurations to prevent workflows from failing silently.
* **Limit Loops**: Use **Until** loops carefully to avoid infinite loops. Always set a maximum iteration count or include time-based exit conditions.
