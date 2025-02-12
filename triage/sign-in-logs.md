# Sign-In Logs







Overview Query:

```kusto
SigninLogs
| where UserPrincipalName == "badactor@cthfm.com"
| project UserPrincipalName, Identity, ResultType, AppDisplayName, ResourceDisplayName, Location, UserAgent, AuthenticationRequirement, ClientAppUsed, ConditionalAccessPolicies, DeviceDetail, LocationDetails, IPAddress
```

