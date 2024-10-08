# Alert Category

## Overview:&#x20;

The following section provides an overview of the schema for the Alert Category as well as provides the specific properties for each alert subtype.&#x20;

## Alert Category&#x20;

The Alert category in the Azure Activity Log records all activations of classic Azure alerts. You can customize alerts to meet your operational needs, such as monitoring CPU usage on a virtual machine. When the conditions defined in an alert rule are met, and a notification is triggered, the activation is logged in this category. These alerts come into the form of alerts and metrics.&#x20;



### Schema

| Element Name         | Description                                                                                                                                                             |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| caller               | Always Microsoft.Insights/alertRules                                                                                                                                    |
| channels             | Always “Admin, Operation”                                                                                                                                               |
| claims               | JSON blob with the SPN (service principal name), or resource type, of the alert engine.                                                                                 |
| correlationId        | A GUID in the string format.                                                                                                                                            |
| description          | Static text description of the alert event.                                                                                                                             |
| eventDataId          | Unique identifier of the alert event.                                                                                                                                   |
| category             | Always "Alert"                                                                                                                                                          |
| level                | [Severity level](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log-schema#severity-level) of the event.                                     |
| resourceGroupName    | Name of the resource group for the impacted resource if it's a metric alert. For other alert types, it's the name of the resource group that contains the alert itself. |
| resourceProviderName | Name of the resource provider for the impacted resource if it's a metric alert. For other alert types, it's the name of the resource provider for the alert itself.     |
| resourceId           | Name of the resource ID for the impacted resource if it's a metric alert. For other alert types, it's the resource ID of the alert resource itself.                     |
| operationId          | A GUID shared among the events that correspond to a single operation.                                                                                                   |
| operationName        | Name of the operation.                                                                                                                                                  |
| properties           | Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.                                                                                |
| status               | String describing the status of the operation. Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.                                       |
| subStatus            | Usually null for alerts.                                                                                                                                                |
| eventTimestamp       | Timestamp when the event was generated by the Azure service processing the request corresponding the event.                                                             |
| submissionTimestamp  | Timestamp when the event became available for querying.                                                                                                                 |
| subscriptionId       | Azure Subscription ID.                                                                                                                                                  |

### Activity Log Alert Specific Properties

| Element Name              | Description                                                                                               |
| ------------------------- | --------------------------------------------------------------------------------------------------------- |
| properties.subscriptionId | The subscription ID from the activity log event that caused this activity log alert rule to be activated. |
| properties.eventDataId    | The event data ID from the activity log event that caused this activity log alert rule to be activated.   |
| properties.resourceGroup  | The resource group from the activity log event that caused this activity log alert rule to be activated.  |
| properties.resourceId     | The resource ID from the activity log event that caused this activity log alert rule to be activated.     |
| properties.eventTimestamp | The event timestamp of the activity log event that caused this activity log alert rule to be activated.   |
| properties.operationName  | The operation name from the activity log event that caused this activity log alert rule to be activated.  |
| properties.status         | The status from the activity log event that caused this activity log alert rule to be activated.          |

### Metric Alert Specific Properties

| Element Name                   | Description                                                                     |
| ------------------------------ | ------------------------------------------------------------------------------- |
| properties.RuleUri             | Resource ID of the metric alert rule itself.                                    |
| properties.RuleName            | The name of the metric alert rule.                                              |
| properties.RuleDescription     | The description of the metric alert rule (as defined in the alert rule).        |
| properties.Threshold           | The threshold value used in the evaluation of the metric alert rule.            |
| properties.WindowSizeInMinutes | The window size used in the evaluation of the metric alert rule.                |
| properties.Aggregation         | The aggregation type defined in the metric alert rule.                          |
| properties.Operator            | The conditional operator used in the evaluation of the metric alert rule.       |
| properties.MetricName          | The metric name of the metric used in the evaluation of the metric alert rule.  |
| properties.MetricUnit          | The metric unit for the metric used in the evaluation of the metric alert rule. |
