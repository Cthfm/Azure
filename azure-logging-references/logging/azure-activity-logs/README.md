# Azure Activity Logs

## Overview:&#x20;

The following section provides an overview of the Schema of the Azure Activity log.&#x20;

### Activity Log:

The **Azure Activity Log** is a critical tool for monitoring and gaining insights into subscription-level events that occur within your Azure environment. It tracks a wide variety of operations, ranging from administrative actions to service health incidents, and it provides detailed logs that can be used for auditing, troubleshooting, and security monitoring.

### **Key Components of the Azure Activity Log Schema**

1. **Severity Levels**:
   * **Critical**: Events requiring immediate attention, such as application or system failures.
   * **Error**: Events indicating a problem that does not need immediate action but still needs addressing.
   * **Warning**: Events that serve as a forewarning of potential issues, indicating a resource may degrade into a more severe state.
   * **Informational**: Non-critical events that provide useful information, such as successful operations.
2. **Categories of Events**:
   * **Administrative**: Logs all create, update, delete, and action operations performed through Azure Resource Manager. For example, creating a virtual machine or modifying a network security group.
   * **Service Health**: Logs incidents affecting Azure services, such as outages or maintenance events, that impact resources in your subscription.
   * **Resource Health**: Logs the health status of Azure resources, such as a virtual machine transitioning to an unavailable state.
   * **Alert**: Logs the activation of Azure alerts, such as when CPU usage exceeds a certain threshold.
   * **Autoscale**: Logs events related to the automatic scaling of resources based on defined autoscale rules.
   * **Recommendation**: Logs recommendations from Azure Advisor on improving security, performance, or cost-efficiency.
   * **Security**: Logs alerts generated by Microsoft Defender for Cloud, such as the execution of a suspicious file.
   * **Policy**: Logs actions performed by Azure Policy, such as audits or denies based on policy rules.

**Schema Properties**

Each event in the Activity Log has a comprehensive set of properties, including:

* **Authorization**: Information on the permissions and roles involved in the operation.
* **CorrelationId**: A unique identifier linking related events.
* **EventDataId**: The unique identifier for the event itself.
* **ResourceId**: The specific resource impacted by the event.

Category event types are broken down further in subsequent pages.&#x20;
