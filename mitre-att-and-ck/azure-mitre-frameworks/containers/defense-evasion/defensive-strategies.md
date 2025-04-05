# Defensive Strategies

## **Defensive Strategies Against Defense Evasion in Containerized Environments**

Defense Evasion techniques are how attackers hide their activities, disable security tooling, masquerade as legitimate services, or avoid detection. In Kubernetes, this could mean disabling Falco, abusing pod names, hiding malicious containers, or tampering with audit logs.

Your goal is to detect tampering early, enforce strict controls, and prevent attackers from blending in.

***

### 1. **Protect Security Controls and Logging Agents**

| Action                                                                          | Why It Matters                                       |
| ------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Run security agents (Falco, Fluentd, Prometheus) in hardened DaemonSets         | Make tampering harder                                |
| Use read-only file systems for monitoring agents                                | Prevent runtime modification or deletion of binaries |
| Block pods from modifying `/var/log`, `/proc`, or `/etc` via volumes            | Protect logs and runtime configs                     |
| Monitor for process kills (`pkill`, `kill`) targeting Falco, auditd, or fluentd | Detect and alert on tampering attempts               |

Prevents attackers from compromising monitoring.&#x20;

***

### &#x20;2. **Enforce Strong Naming Conventions and Admission Controls**

| Action                                                                                                    | Why It Matters                                            |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Block pods that mimic system names (e.g., `kube-`, `etcd-`, `metrics-server`) unless in system namespaces | Stop attackers from blending in                           |
| Validate namespace placement for system pods (only kube-system for system services)                       | Attackers can't drop fake system pods in other namespaces |
| Enforce strict labeling (e.g., `app=trusted`) and require signed deployments                              | Make legitimate workloads verifiable                      |

Prevents masquerading from occuring

***

### 3. **Protect Secrets and Authentication Materials**

| Action                                                                                                 | Why It Matters                             |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
|  Use encrypted secrets management (Azure Key Vault, HashiCorp Vault) instead of raw Kubernetes Secrets | Secrets shouldn't sit unprotected          |
| Rotate secrets and service account tokens regularly.                                                   | Shorten window if stolen                   |
| Limit pod access to metadata APIs (IMDS) with network policies or Pod Identity restrictions            | Prevent stealing Azure, GCP, or AWS tokens |

Defends against stealing and using tokens to evade normal auth paths.

***

### 4. **Harden API Server and Audit Infrastructure**

| Action                                                                     | Why It Matters                                             |
| -------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Enable Kubernetes audit logging at the API server levels.                  | Track all role changes, token access, and exec events      |
| Restrict who can access `/logs`, `/metrics`, and `/debug` endpoints        | These endpoints can leak sensitive information             |
| Parse and alert on suspicious logins, privilege grants, and token accesses | Immediate detection of lateral movement or privilege abuse |

Detects and deters attempts at Indicator Removal or Audit Tampering.

***

### 5. **Deploy Runtime Threat Detection**

| Action                                                                                  | Why It Matters                    |
| --------------------------------------------------------------------------------------- | --------------------------------- |
| Deploy Falco with rules to monitor for execs, pod creations, and system file tampering  | Catch runtime stealth activities  |
| Alert on unexpected outbound network connections from system pods                       | Data exfil and C2 channels        |
| Integrate Falco with SIEMs (e.g., Elastic, Splunk) for centralized threat intelligences | Fast, scalable incident detection |

Catches late stage execution.

***

### Defensive Coverage Table (Defense Evasion)

| Attack Vector                               | Defensive Strategy                                            |
| ------------------------------------------- | ------------------------------------------------------------- |
| Disabling logging/monitoring agents         | Harden DaemonSets, monitor process kills                      |
| Masquerading via pod names                  | Block kube- prefix names outside kube-system namespace        |
| Stealing tokens for silent lateral movement | Protect metadata APIs, rotate tokens, enforce least privilege |
| Tampering with Kubernetes audit logs        | Enable audit logging, restrict access to logs/metrics         |
| Hiding C2 traffic                           | Monitor unexpected outbound connections and DNS requests      |

***

## Final Summary

Defending against Defense Evasion focuses on:

* **Protecting monitoring and logging** so attackers can't blind you
* **Stopping attackers from blending into legitimate services**
* **Securing secrets and tokens** to prevent stealthy access
* **Detecting tampering attempts early** before an attack goes critical
