# AzureActivity

## Overview:

The following provides insights into any subscription-level or management group level events that have occurred in Azure. We will look at key fields we can use to create triage searches.

### Overview Query:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com"
| project TimeGenerated, ResourceProviderValue, OperationNameValue, SubscriptionId, Caller, CallerIpAddress, Authorization, _ResourceId, Properties
```

### Specific Actions by Subscription:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com"
| summarize count() by SubscriptionId, ResourceProviderValue, OperationNameValue
```

### Resource Interactions:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com"
| summarize count() by OperationNameValue, _ResourceId
```

### Policy Based Actions:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com" and CategoryValue == 'Policy'
| project ResourceProviderValue, ResourceGroup, OperationNameValue, ActivityStatusValue, Properties
```

Microsoft.Authorization/policies/audit/action - operation to the activity log and marks the resource as non-compliant. Policy the resource was evaluated against, and the finding can be found in properties.

Microsoft.Authorization/policies/auditIfNotExists/action - logged operation that checks whether a resource exists or has a specific configuration. Policy the resource was evaluated against, and the finding can be found in properties.

{% hint style="info" %}
When deploying a new tenant Azure Security Center Compliance Checks are enabled (Now Defender for Cloud). These are in an audit only state.
{% endhint %}

### Administrative Actions:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com" and CategoryValue == 'Administrative'
| project ResourceProviderValue, ResourceGroup, OperationNameValue, ActivityStatusValue, Properties
```

### IP address of the Caller:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com" 
| summarize count() by CallerIpAddress
```

