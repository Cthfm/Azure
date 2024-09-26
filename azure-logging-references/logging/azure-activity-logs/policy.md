# Policy

### Policy Overview:

This category contains records of all effect action operations performed by [Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview). Examples of the types of events you would see in this category include _Audit_ and _Deny_. Every action taken by Policy is modeled as an operation on a resource.

### Schema:

| Element Name                 | Description                                                                                                                                                                                                                                                                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| authorization                | Array of Azure RBAC properties of the event. For new resources, this is the action and scope of the request that triggered evaluation. For existing resources, the action is "Microsoft.Resources/checkPolicyCompliance/read".                                                                                                       |
| caller                       | For new resources, the identity that initiated a deployment. For existing resources, the GUID of the Microsoft Azure Policy Insights RP.                                                                                                                                                                                             |
| channels                     | Policy events use only the "Operation" channel.                                                                                                                                                                                                                                                                                      |
| claims                       | The JWT token used by Active Directory to authenticate the user or application to perform this operation in Resource Manager.                                                                                                                                                                                                        |
| correlationId                | Usually a GUID in the string format. Events that share a correlationId belong to the same uber action.                                                                                                                                                                                                                               |
| description                  | This field is blank for Policy events.                                                                                                                                                                                                                                                                                               |
| eventDataId                  | Unique identifier of an event.                                                                                                                                                                                                                                                                                                       |
| eventName                    | Either "BeginRequest" or "EndRequest". "BeginRequest" is used for delayed auditIfNotExists and deployIfNotExists evaluations and when a deployIfNotExists effect starts a template deployment. All other operations return "EndRequest".                                                                                             |
| category                     | Declares the activity log event as belonging to "Policy".                                                                                                                                                                                                                                                                            |
| eventTimestamp               | Timestamp when the event was generated by the Azure service processing the request corresponding the event.                                                                                                                                                                                                                          |
| ID                           | Unique identifier of the event on the specific resource.                                                                                                                                                                                                                                                                             |
| level                        | [Severity level](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log-schema#severity-level) of the event. Audit uses "Warning" and Deny uses "Error". An auditIfNotExists or deployIfNotExists error can generate "Warning" or "Error" depending on severity. All other Policy events use "Informational". |
| operationId                  | A GUID shared among the events that correspond to a single operation.                                                                                                                                                                                                                                                                |
| operationName                | Name of the operation and directly correlates to the Policy effect.                                                                                                                                                                                                                                                                  |
| resourceGroupName            | Name of the resource group for the evaluated resource.                                                                                                                                                                                                                                                                               |
| resourceProviderName         | Name of the resource provider for the evaluated resource.                                                                                                                                                                                                                                                                            |
| resourceType                 | For new resources, it's the type being evaluated. For existing resources, returns "Microsoft.Resources/checkPolicyCompliance".                                                                                                                                                                                                       |
| resourceId                   | Resource ID of the evaluated resource.                                                                                                                                                                                                                                                                                               |
| status                       | String describing the status of the Policy evaluation result. Most Policy evaluations return "Succeeded", but a Deny effect returns "Failed". Errors in auditIfNotExists or deployIfNotExists also return "Failed".                                                                                                                  |
| subStatus                    | Field is blank for Policy events.                                                                                                                                                                                                                                                                                                    |
| submissionTimestamp          | Timestamp when the event became available for querying.                                                                                                                                                                                                                                                                              |
| subscriptionId               | Azure Subscription ID.                                                                                                                                                                                                                                                                                                               |
| properties.isComplianceCheck | Returns "False" when a new resource is deployed or an existing resource's Resource Manager properties are updated. All other [evaluation triggers](https://learn.microsoft.com/en-us/azure/governance/policy/how-to/get-compliance-data#evaluation-triggers) result in "True".                                                       |
| properties.resourceLocation  | The Azure region of the resource being evaluated.                                                                                                                                                                                                                                                                                    |
| properties.ancestors         | A comma-separated list of parent management groups ordered from direct parent to farthest grandparent.                                                                                                                                                                                                                               |
| properties.policies          | Includes details about the policy definition, assignment, effect, and parameters that this Policy evaluation is a result of.                                                                                                                                                                                                         |
| relatedEvents                | This field is blank for Policy events.                                                                                                                                                                                                                                                                                               |
