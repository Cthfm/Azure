# Sign-In Logs

## Overview:

The following is an overview of the Sign-In logs.&#x20;

{% hint style="danger" %}
You need a P2 license to see Risk based information as this information is hidden from view in the logs.&#x20;
{% endhint %}

## Overview Query:

```kusto
SigninLogs
| where UserPrincipalName == "badactor@cthfm.com"
| project UserPrincipalName, Identity, ResultType, AppDisplayName, ResourceDisplayName, Location, UserAgent, AuthenticationRequirement, ClientAppUsed, ConditionalAccessPolicies, DeviceDetail, LocationDetails, IPAddress, Status
```

