# Lateral Movement TA0008

## **Lateral Movement Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure Active Directory), **Lateral Movement** happens when attackers move across accounts, services, tenants, or cloud APIs after initial access.\
Instead of pivoting through networks like traditional attacks, cloud lateral movement is **token-based, session-based, or API-based**.

***

#### 🔀 Use Alternate Authentication Material → Application Access Token

\| MITRE ID | **T1550.001** |

**Description**:\
Steal or forge **Azure OAuth access tokens** or **Managed Identity tokens** to authenticate to other Azure services or Entra ID resources without needing passwords.

**Entra ID Example**:

* Attacker compromises an Azure VM or Function App.
* Extracts a Managed Identity token from the Azure Instance Metadata Service (IMDS).
* Uses the token to access Azure APIs (e.g., Key Vaults, Storage Accounts, Kubernetes clusters, privileged management APIs).

```bash
bashCopyEdit# Retrieve Managed Identity token
curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"

# Use token to query Azure Management APIs
curl -X GET https://management.azure.com/subscriptions/<sub-id>/resourceGroups?api-version=2020-06-01 \
-H "Authorization: Bearer <stolen_token>"
```

✅ **Result**:\
Attacker moves across Azure resources, authenticating with the stolen token invisibly — without triggering password-based detections.

***

## 📊 **Lateral Movement Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique   | MITRE ID  | Entra ID Example                                                          |
| ------------------------ | --------- | ------------------------------------------------------------------------- |
| Application Access Token | T1550.001 | Steal and reuse OAuth or Managed Identity tokens to access cloud services |

***

## 🎯 Final Summary

Defending against Lateral Movement in Entra ID focuses on:

* **Securing tokens and sessions from theft**
* **Restricting token permissions to the minimum necessary (least privilege)**
* **Monitoring token usage for anomalous patterns (e.g., reuse across IPs, geographies)**
* **Revoking tokens quickly when compromise is detected**





