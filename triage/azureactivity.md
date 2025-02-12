# AzureActivity

## Overview:

The following provides insights into any subscription-level or management group level events that have occurred in Azure. We will look at key fields we can use to create triage searches.



### Overview Query:

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

### Administrative Actions:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com" and CategoryValue == 'Administrative'
| project ResourceProviderValue, ResourceGroup, OperationNameValue, ActivityStatusValue, Properties
```

CallerIP:

```kusto
AzureActivity
| where Caller == "badactor@cthfm.com" 
| summarize count() by CallerIpAddress
```

