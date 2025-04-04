# Defensive Strategies

## **Defensive Strategies Against Persistence in Containerized Environments**

Persistence techniques in Kubernetes and containers allow adversaries to maintain long-term access, even after node restarts or detection. Persistence can come from creating hidden workloads, escalating service account privileges, implanting malicious images, or scheduling CronJobs.\
Your goal is to detect, restrict, and cleanly block persistent footholds.

***

### 🧰 1. **Restrict Creation of New Accounts, Roles, and Bindings**

| Action                                                                     | Why It Matters                                      |
| -------------------------------------------------------------------------- | --------------------------------------------------- |
| 🔒 Monitor and restrict RoleBinding and ClusterRoleBinding creations       | Attackers use new bindings to maintain admin access |
| 🚫 Block ServiceAccounts from being created outside specific namespaces    | Limit service account sprawl                        |
| 📜 Audit ServiceAccounts and role assignments regularly                    | Spot unexpected privilege grants                    |
| 🧠 Use tight RBAC (least privilege) — no cluster-admin unless truly needed | Shrinks persistence paths                           |

✅ Detects and prevents **T1098 – Account Manipulation**.

***

### 🐳 2. **Control and Monitor Workload Changes (Pods, CronJobs, DaemonSets)**

| Action                                                                      | Why It Matters                                      |
| --------------------------------------------------------------------------- | --------------------------------------------------- |
| 📜 Use Admission Control to block creation of CronJobs/Jobs unless needed   | Prevent attacker-triggered scheduled persistence    |
| 🚫 Restrict privileged DaemonSets (no auto-start malware agents)            | DaemonSets persist across node reboots              |
| 🛡️ Protect Deployments with immutable fields                               | Stop attackers from silently replacing running pods |
| 🔎 Monitor for new workload deployments (e.g., kubectl apply, Helm install) | Fresh workloads = potential implants                |

✅ Stops attackers from **implanting internal images** or setting **orchestration jobs** for persistence.

***

### 🔥 3. **Protect and Limit Image Sources**

| Action                                                                                  | Why It Matters                                   |
| --------------------------------------------------------------------------------------- | ------------------------------------------------ |
| 📋 Enforce container image signing (Cosign, Notary)                                     | Block unsigned or tampered images                |
| 🔎 Scan images for hidden persistence implants (reverse shells, cron inside containers) | Catch trojanized container bases                 |
| 🧠 Whitelist trusted registries only                                                    | No pulling images from DockerHub or random repos |

✅ Blocks **implanting malicious internal images** as persistent footholds.

***

### 🛡️ 4. **Service Account and Token Hardening**

| Action                                                              | Why It Matters                      |
| ------------------------------------------------------------------- | ----------------------------------- |
| 📜 Set `automountServiceAccountToken: false` by default on all pods | Reduce service account token sprawl |
| 🔒 Limit access to token secrets and Kubernetes Secrets overall     | Make it harder to reuse tokens      |
| 🛡️ Rotate service account tokens periodically                      | Reduce persistence window if stolen |

✅ Protects against persistent **token-based access reuse**.

***

### 🧠 5. **Monitor Persistence Indicators at Runtime**

| Action                                                                       | Why It Matters                                         |
| ---------------------------------------------------------------------------- | ------------------------------------------------------ |
| 📡 Use Falco to detect creation of new CronJobs, DaemonSets, or unusual pods | Real-time visibility into suspicious workload creation |
| 🔥 Alert on ServiceAccount binding to cluster-admin dynamically              | Huge persistence red flag                              |
| 📜 Parse audit logs for new workload or privileged role creations            | Build forensic trails for post-breach investigations   |

✅ Catch persistence techniques during execution before full compromise.

***

### 📊 Defensive Coverage Table (Persistence)

| Attack Vector                      | Defensive Strategy                                   |
| ---------------------------------- | ---------------------------------------------------- |
| New ServiceAccount creation        | Block in restricted namespaces, monitor RBAC changes |
| ClusterRoleBinding escalation      | Alert on ClusterRoleBinding/RoleBinding events       |
| CronJob/Job deployment             | Admission control to restrict scheduled jobs         |
| Deployment of malicious containers | Enforce image signing and scan pipelines             |
| Unauthorized token usage           | Limit automountServiceAccountToken, rotate tokens    |
