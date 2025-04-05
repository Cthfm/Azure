# Defensive Strategies

## **Defensive Strategies Against Impact in Containerized Environments**

Impact techniques focus on disrupting availability, destroying data, exhausting resources, or causing lasting damage. In Kubernetes, attackers may delete storage, flood services, mine crypto, or corrupt recovery processes.

Your goal is to protect data, maintain service resilience, limit resource abuse, and detect destructive behaviors fast.

***

### 1. **Protect Storage and Critical Resources**

| Action                                                                                       | Why It Matters                                      |
| -------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| Apply RBAC to restrict who can delete PVCs, Secrets, ConfigMaps, and workloads               | Only authorized users can delete critical resources |
| Use Kubernetes ResourceQuotas and PodDisruptionBudgets to protect against mass deletions     | Stop runaway delete operations                      |
| Regularly back up Kubernetes cluster state (etcd) and Persistent Volumes (PV snapshots)      | Fast recovery after destructive attacks             |
| Disable wildcard deletion permissions (e.g., `kubectl delete all --all`) for non-admin users | Prevent mass deletion attacks                       |

Defends against Data Destruction and Inhibit System Recovery.

***

### 2. **Detect and Prevent Resource Exhaustion (Denial of Service)**

| Action                                                                            | Why It Matters                                      |
| --------------------------------------------------------------------------------- | --------------------------------------------------- |
| Enforce resource requests/limits on all pods (CPU, memory)                        | Pods can't overconsume node resources               |
| Implement Kubernetes Horizontal Pod Autoscaler and Cluster Autoscaler protections | Prevent scaling disasters during DDoS/flood attacks |
| Monitor service latency and error rates using Prometheus/Grafana/Datadog          | Detect early signs of overload or DoS conditions    |
| Use rate limiting, WAFs, and API gateways on public-facing services               | Block request floods at the edge                    |

Defends against Endpoint DoS and Network DoS attacks.

***

### 3. **Prevent Resource Hijacking (Crypto Mining / Bandwidth Abuse)**

| Action                                                                                           | Why It Matters                                                 |
| ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| Scan container images for known crypto miners (Trivy, Dockle, Clair)                             | Catch hidden miners at build time                              |
| Block `privileged` containers and `hostNetwork` pods                                             | Prevent stealth mining or proxy tunneling workloads            |
| Set tight egress network policies to prevent bandwidth abuse (TOR, SOCKS5, exfiltration tunnels) | Protect your cloud bill and reputation                         |
| Monitor unexpected CPU spikes, outbound connections, and anomalous traffic patterns              | Crypto miners and proxy relays are noisy if you watch for them |

Defends against Compute Hijacking and Bandwidth Hijacking.

***

### 4. **Monitor and Alert on Destructive Actions**

| Action                                                                                                               | Why It Matters                              |
| -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
|  Enable Kubernetes audit logging for destructive verbs (`delete`, `patch`, `update`)                                 | Full visibility into destructive actions    |
| Deploy Falco to detect mass deletion of resources, mass file deletions, and suspicious binaries (e.g., `rm`, `mkfs`) | Real-time detection of destruction attempts |
| Set cloud alerts on sudden drops in resource counts (e.g., missing nodes, missing services, mass pod crashes)        | Detect cluster degradation quickly          |

Real-time detection of attacks attempting cluster or workload sabotage.

***

### 5. **Resilience and Recovery Hardening**

| Action                                                                                       | Why It Matters                                         |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| Set up automated regular backups of Kubernetes etcd, Persistent Volumes, and Secrets         | Recovery becomes a push-button operation               |
| Protect backup storage (Azure Recovery Vault, AWS Backup, etc.) with separate IAM identities | Attackers shouldn’t be able to wipe backups easily     |
| Regularly test disaster recovery procedures in controlled exercises                          | Ensure teams know how to recover if an attack succeeds |
| Implement immutable backups or write-once storage if available                               | Protect against ransomware and mass deletion attacks   |

Ensures recovery from Impact tactics like destruction, corruption, or resource exhaustion.

***

### Defensive Coverage Table (Impact)

| Attack Vector                            | Defensive Strategy                                                   |
| ---------------------------------------- | -------------------------------------------------------------------- |
| Data destruction (PVCs, Secrets)         | RBAC restrictions, ResourceQuotas, regular backups                   |
| Service denial (DoS attacks)             | Resource limits, HPA scaling protections, WAFs                       |
| Recovery inhibition                      | Secure backup storage, immutable backups, DR testing                 |
| Compute hijacking (crypto mining)        | Image scanning, limit resource overconsumption, detect CPU anomalies |
| Bandwidth hijacking (proxy/tunnel abuse) | Egress controls, traffic monitoring, rate limiting                   |

### Final Summary

Defending against Impact focuses on:

* **Protecting critical resources from deletion or corruption** (RBAC, quotas, backups)
* **Containing and detecting resource abuse** (compute and network monitoring)
* **Detecting destructive behaviors in real time** (audit logs + Falco)
* **Ensuring rapid recovery even if an attack succeeds** (tested DR plans)
