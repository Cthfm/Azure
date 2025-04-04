# Defensive Strategies

## **Defensive Strategies Against Lateral Movement in Containerized Environments**

**Lateral Movement** techniques allow adversaries to pivot inside a compromised environment, moving from one pod, namespace, or node to another, or even into the cloud control plane. In Kubernetes, lateral movement often happens through stolen tokens, over-permissive networking, weak RBAC permissions, or abuse of internal services.

Your goal is to **contain blast radius**, **restrict internal communication**, **lock down tokens and identities**, and **detect unauthorized movements quickly**.

***

### 🧰 1. **Restrict Internal Networking Between Pods and Namespaces**

| Action                                                                                        | Why It Matters                                             |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 🛡️ Enforce Kubernetes Network Policies (Calico, Cilium) to restrict pod-to-pod communication | Only allow necessary communication paths                   |
| 🚫 Default-deny all pod ingress and egress traffic, whitelist needed traffic explicitly       | No "open" networks for attackers to move freely            |
| 📜 Segment sensitive workloads into separate namespaces                                       | Control who can even "see" critical services               |
| 🔒 Use service mesh tools (Istio, Linkerd) with mTLS                                          | Encrypt pod-to-pod traffic and authenticate pod identities |

✅ Blocks **T1021 – Remote Services** and **T1550 – Use Alternate Authentication Material** based lateral movement.

***

### 🔐 2. **Lock Down Kubernetes RBAC and Cloud IAM**

| Action                                                                                   | Why It Matters                                              |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| 🔒 Use strict RoleBindings scoped only to namespaces — no broad cluster-wide permissions | Attackers can’t easily move from one namespace to another   |
| 📜 Prevent token reuse across namespaces                                                 | ServiceAccounts should only be valid in their own namespace |
| 🛡️ Implement Azure AD or workload identity for finer-grained cloud permissions          | Prevent lateral movement into Azure resources               |

✅ Defends against stealing and reusing valid tokens for lateral pivoting.

***

### 📦 3. **Protect Service Account Tokens and Metadata Access**

| Action                                                                                                              | Why It Matters                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| 📜 Set `automountServiceAccountToken: false` unless necessary                                                       | No automatic credential exposure                       |
| 🚫 Use Azure Managed Identity exceptions or egress policies to block pod access to Instance Metadata Service (IMDS) | Prevent cloud privilege escalation through token theft |
| 🔒 Rotate tokens frequently and use projected tokens with short TTLs                                                | Limit window for stolen credentials to be abused       |

✅ Prevents attacks similar to stealing tokens and using them to impersonate services (T1550.001 – Application Access Token).

***

### 📡 4. **Detect Lateral Movement Attempts at Runtime**

| Action                                                                                              | Why It Matters                                             |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 📜 Enable Kubernetes API audit logs to detect unexpected token use, namespace access, and API calls | Early detection of abnormal behavior                       |
| 📡 Use Falco to detect internal scanning (e.g., mass curl, wget, nmap from pods)                    | Catch discovery and pivoting attempts live                 |
| 🔥 Alert on creation of new pods or Jobs in unexpected namespaces                                   | Attackers often deploy malicious workloads to move further |

✅ Provides real-time detection if attackers attempt lateral moves inside the cluster.

***

### 🛡️ 5. **Isolate Cloud Access and Cluster Boundaries**

| Action                                                                                               | Why It Matters                                                 |
| ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| 🧠 Use separate Service Principals / Managed Identities for nodes and pods                           | Cloud resource access should not be uniform across the cluster |
| 🛡️ Apply cloud IAM policies (Azure RBAC) to restrict what a compromised node or pod can do in Azure | Prevent pivot into control plane, subscriptions, storage, etc. |
| 🔒 Separate Kubernetes clusters for production, staging, and dev                                     | Harder for attackers to pivot across environments              |

✅ Limits the blast radius if cloud credentials are compromised through lateral movement.

***

### 📊 Defensive Coverage Table (Lateral Movement)

| Attack Vector                        | Defensive Strategy                                       |
| ------------------------------------ | -------------------------------------------------------- |
| Pod-to-pod communication abuse       | Enforce strict Network Policies, mTLS between pods       |
| RBAC/token reuse across namespaces   | Limit token scopes, namespace isolation, rotate tokens   |
| Internal network discovery           | Falco detection on nmap, curl, wget across pods          |
| Stolen metadata tokens (cloud pivot) | Block IMDS access, implement Azure Pod Identity securely |
| Unauthorized pod/job creation        | Audit logs + Falco alerts on new resource creation       |

***

## 🎯 Final Summary

Defending against Lateral Movement focuses on:

* **Locking down network paths inside the cluster** (Network Policies, mTLS)
* **Restricting identity usage and access scopes** (tight RBAC, workload identity)
* **Detecting unauthorized internal movements fast** (Falco, audit logs)
* **Segregating environments and cloud access** (blast radius control)
