# First Party Sign-In Activity

Provided below is a reference to First Party Sign-In to correlate activity in the Sign-In logs.&#x20;

{% embed url="https://learn.microsoft.com/en-us/troubleshoot/azure/entra/entra-id/governance/verify-first-party-apps-sign-in" %}

## CLI Commands

Obtain a list of the Service Principals within a given tenant.&#x20;

```bash
az ad sp list --all --query '[].{description:tags[0], displayName:displayName, id:id appid:appid}' -o json
```

### Azure CLI: Search by DisplayName

```bash
az ad sp list --display-name Azure
```

### Azure CLI: Search by ID

```bash
az ad sp show --id 00000000-0000-0000-0000-000000000000
```

### Powershell Command

```powershell
et-AzureADServicePrincipal -Filter "DisplayName eq '<display-name>'" | fl *
```
