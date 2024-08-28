# Recommendation

## Recommendations Overview:

The Recommendation category in the Azure Activity Log records new recommendations generated for your services, such as "Use availability sets for improved fault tolerance." These recommendations are categorized into four types: High Availability, Performance, Security, and Cost Optimization. Security recommendations can be utilized in order to enhance the security of the organization.&#x20;

### Schema

| Element Name                           | Description                                                                                                                         |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| channels                               | Always “Operation”                                                                                                                  |
| correlationId                          | A GUID in the string format.                                                                                                        |
| description                            | Static text description of the recommendation event                                                                                 |
| eventDataId                            | Unique identifier of the recommendation event.                                                                                      |
| category                               | Always "Recommendation"                                                                                                             |
| ID                                     | Unique resource identifier of the recommendation event.                                                                             |
| level                                  | [Severity level](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log-schema#severity-level) of the event. |
| operationName                          | Name of the operation. Always "Microsoft.Advisor/generateRecommendations/action"                                                    |
| resourceGroupName                      | Name of the resource group for the resource.                                                                                        |
| resourceProviderName                   | Name of the resource provider for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE"                     |
| resourceType                           | Name of the resource type for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE/virtualmachines"         |
| resourceId                             | Resource ID of the resource that the recommendation applies to                                                                      |
| status                                 | Always "Active"                                                                                                                     |
| submissionTimestamp                    | Timestamp when the event became available for querying.                                                                             |
| subscriptionId                         | Azure Subscription ID.                                                                                                              |
| properties                             | Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the recommendation.                                   |
| properties.recommendationSchemaVersion | Schema version of the recommendation properties published in the Activity Log entry                                                 |
| properties.recommendationCategory      | Category of the recommendation. Possible values are "High Availability", "Performance", "Security", and "Cost"                      |
| properties.recommendationImpact        | Impact of the recommendation. Possible values are "High", "Medium", "Low"                                                           |
| properties.recommendationRisk          | Risk of the recommendation. Possible values are "Error", "Warning", "None"                                                          |
