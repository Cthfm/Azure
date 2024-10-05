# Logic App Types

When using Azure Logic Apps for threat hunting and security automation, it's important to understand the two main types of Logic Apps: **Consumption-based** and **Standard**. Each type has its strengths, pricing model, and use cases, and knowing the difference helps you choose the right one for your security needs.

***

#### **1. Consumption-based Logic Apps**

**Consumption-based Logic Apps** are the original version of Logic Apps, operating on a **pay-per-execution model**. This means you only pay for the number of times your Logic App runs, and for the actions executed within each workflow. These Logic Apps are serverless, meaning Azure automatically manages the scaling and infrastructure.

**Key Features:**

* **Cost-efficient for Intermittent Workflows**: You pay only for what you use, making it ideal for workflows that are triggered by security events or that run periodically, such as daily threat-hunting scans or responding to security alerts.
* **Wide Range of Connectors**: Access to hundreds of built-in and custom connectors, including those tailored for security like Azure Sentinel, Microsoft Defender, and third-party SIEM or threat intelligence platforms.
* **Event-Driven Workflows**: Ideal for scenarios where workflows are triggered by specific security events (e.g., new security incidents in Azure Sentinel or alerts from an intrusion detection system). You can set the Logic App to activate when needed without having to pay for idle time.

**Best Use Cases for Threat Hunting:**

1. **On-demand and Trigger-Based Security Workflows**:
   * For example, setting up a Logic App to trigger when a critical alert is raised in Azure Sentinel. The Logic App can automatically enrich the alert with threat intelligence, send notifications, and initiate investigation steps.
2. **Ad Hoc Threat-Hunting Queries**:
   * Consumption-based Logic Apps are ideal for workflows that run based on threat-hunting queries, such as querying logs for failed login attempts or scanning specific users for suspicious activity.
3. **Security Incident Response Automation**:
   * You can build incident response workflows that automatically trigger when an attack is detected, such as blocking a malicious IP or disabling a compromised user account.

***

#### **2. Standard Logic Apps**

**Standard Logic Apps** offer more advanced capabilities and greater flexibility in terms of control over **hosting**, **performance**, and **scalability**. Unlike Consumption-based Logic Apps, Standard Logic Apps use a **fixed pricing model** based on the number of **workflow executions and instances**, which can be more cost-effective for high-volume workflows. Standard Logic Apps are designed for scenarios where you need more customization, control, or need to process large volumes of security data continuously.

**Key Features:**

* **Stateful and Stateless Workflows**: Standard Logic Apps can run in either **stateful** or **stateless** mode, which is particularly useful for security automation:
  * **Stateful Workflows**: These maintain their state across long-running processes, such as threat-hunting workflows that involve multiple steps over a longer duration (e.g., correlating log data over hours or days).
  * **Stateless Workflows**: Ideal for high-performance scenarios where the response needs to be fast, such as responding to security alerts in real-time without the need for state persistence.
* **Higher Performance and Lower Latency**: Standard Logic Apps are optimized for scenarios where performance is critical, such as threat-hunting tasks that need to process high volumes of security data quickly or respond to fast-moving threats in real-time.
* **Integrated Development Environments**: With Standard Logic Apps, you can use tools like **Visual Studio Code** to develop, test, and debug workflows locally. This is useful when building complex threat-hunting automation workflows that require extensive customization.
* **Managed in Azure Functions Environment**: Unlike Consumption-based Logic Apps, Standard Logic Apps are hosted in an **Azure Functions Premium Plan** or **App Service Environment** (ASE), giving you more control over where and how the Logic App runs. This is helpful for sensitive security operations where the workflow needs to be isolated or run within a specific virtual network.

**Best Use Cases for Threat Hunting:**

1. **Continuous Security Monitoring**:
   * If your threat-hunting workflows involve continuously processing logs or scanning for security events in real-time, Standard Logic Apps are ideal due to their stateful capabilities and lower latency.
   * Example: A continuous workflow that monitors firewall logs in real-time for suspicious activity and alerts the security team immediately.
2. **Long-Running Security Workflows**:
   * For scenarios that require tracking and handling complex incidents over time, such as following up on advanced persistent threat (APT) indicators across various systems, a stateful Standard Logic App can maintain the workflow state until all threat-hunting activities are complete.
3. **High-Volume Log Analysis and Threat Detection**:
   * If you need to process large amounts of security data continuously, such as analyzing terabytes of logs from Azure Monitor, Standard Logic Apps provide the performance and scalability needed for large-scale threat-hunting activities.

***

#### **Comparison: Consumption vs. Standard Logic Apps**

| **Feature**                 | **Consumption Logic Apps**                          | **Standard Logic Apps**                                 |
| --------------------------- | --------------------------------------------------- | ------------------------------------------------------- |
| **Pricing Model**           | Pay-per-use (billed per action and trigger)         | Fixed pricing based on plan and resources used          |
| **Triggers**                | Event-driven (e.g., security alerts)                | Event-driven and continuous monitoring                  |
| **Workflows**               | Stateless (state managed by Azure)                  | Stateful and Stateless                                  |
| **Latency**                 | Higher latency, suitable for periodic checks        | Lower latency, ideal for real-time response             |
| **Complexity**              | Simple workflows, ideal for specific security tasks | Advanced workflows for complex threat-hunting           |
| **Hosting**                 | Serverless (fully managed by Azure)                 | Azure Functions environment (more control over hosting) |
| **Development Environment** | Built-in visual designer in Azure portal            | Visual Studio Code integration for local development    |

***

#### **When to Use Consumption-Based Logic Apps:**

* **For Small or Intermittent Workflows**: If your threat-hunting and security workflows are triggered occasionally (e.g., only in response to a detected event or run periodically), Consumption Logic Apps are more cost-effective.
* **When Minimal Customization is Needed**: If the workflow requires basic automation tasks (e.g., sending alerts, querying logs), Consumption Logic Apps will suffice.

**Example**: Automating the response to a suspicious email detected by Microsoft Defender, such as flagging the email, sending a notification to security staff, and logging the incident.

***

#### **When to Use Standard Logic Apps:**

* **For Continuous or High-Volume Security Operations**: Standard Logic Apps are better suited for continuous threat monitoring, processing large volumes of security data, or workflows that need to persist state across multiple steps.
* **When You Need Advanced Capabilities**: If your threat-hunting processes require a complex series of actions, data enrichment, or coordination across multiple systems with low latency, Standard Logic Apps provide the flexibility and performance needed.

**Example**: Running a stateful Logic App to continuously monitor Azure Sentinel for suspicious patterns over time and automatically correlate these with external threat intelligence feeds.
