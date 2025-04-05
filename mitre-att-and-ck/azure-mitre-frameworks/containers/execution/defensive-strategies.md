# Defensive Strategies

## **Defensive Strategies Against Execution in Containerized Environments**

Once adversaries gain initial access, Execution techniques allow them to run commands, deploy malicious containers, or execute scripts inside your Kubernetes cluster.&#x20;

**Outcome:** The goal of your defenses here is to prevent unauthorized code execution at runtime and restrict execution paths even if attackers get a toehold.

### 1. **Harden Container Runtime Controls**

| Action                                                                 | Why It Matters                                      |
| ---------------------------------------------------------------------- | --------------------------------------------------- |
| Enforce container security contexts (no privilege escalation)          | Prevent attackers from gaining extra runtime rights |
|  Use AppArmor/SELinux/ seccomp profiles on pods                        | Restrict syscalls containers can execute            |
| Block containers with `privileged: true` or host namespace access      | Stop easy host-level attacks                        |
| Use read-only root filesystems and drop unnecessary Linux capabilities | Make persistence harder                             |

Enforced by OPA Gatekeeper, Kyverno, or PodSecurity Admission.

### &#x20;2. **Control Container Deployment Sources**

| Action                                                                | Why It Matters                                     |
| --------------------------------------------------------------------- | -------------------------------------------------- |
| Only allow images from trusted, signed registries (Cosign, Notary)    | Prevent pulling malicious containers               |
| Block `kubectl run` or `kubectl create` in restricted namespaces      | No ad-hoc deployments by compromised users or pods |
|  Enforce tight workload identity controls (Azure Workload Identity)   | Only trusted identities can deploy workloads       |
| Scan container images for malware pre-deployment (Trivy, Clair, Aqua) | Block malicious images at CI/CD pipelines          |

Defeats attackers who attempt to deploy backdoored or trojanized pods.

***

### 3. **Restrict Kubernetes Native Execution Paths**

| Action                                                         | Why It Matters                                                        |
| -------------------------------------------------------------- | --------------------------------------------------------------------- |
| Restrict `kubectl exec` usage to cluster admins only           | Block podshell access for compromised accounts                        |
| Monitor Kubernetes API server for exec events (`kubectl exec`) | Detect real-time container execution attempts                         |
| Block or heavily restrict CronJobs/Jobs creation               | Prevent scheduled malicious execution via Kubernetes-native resources |

Stops abuse of kubectl exec, jobs, CronJobs, or pods as execution vehicles.

***

### 4. **Detect Suspicious Execution in Real Time**

| Action                                                                             | Why It Matters                                                   |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Deploy Falco to monitor container execution                                        | Catch reverse shells, suspicious binaries, or runtime injections |
|  Use anomaly detection to spot sudden spikes in process launches inside containers | Attackers tend to run unexpected commands                        |
| Log Kubernetes audit events for pod creation, exec, and new deployments            | Creates forensic trail of suspicious execution activities        |

Visibility into execution helps detect and respond quickly if preventive controls fail.

***

### 5. **Limit Runtime Behavior**

| Action                                                     | Why It Matters                                                         |
| ---------------------------------------------------------- | ---------------------------------------------------------------------- |
| Enforce Network Policies                                   | Pods can only talk to what they need, blocks C2 channels               |
| Use PodDisruptionBudgets and resource quotas               | Limit blast radius of runaway pods and malicious Jobs eating resources |
| Enable PodSecurity Standards (Baseline or Restricted mode) | Blocks most dangerous pod specs (privileged, host mounts, etc.)        |

Even if execution happens, it is sandboxed and contained.

***

### Defensive Coverage Table (Execution)

| Attack Vector                            | Defensive Strategy                                             |
| ---------------------------------------- | -------------------------------------------------------------- |
| `kubectl exec` abuse                     | Block exec, monitor API server, restrict RBAC permissions      |
| Malicious container deployment           | Enforce image signing, scan images, restrict `kubectl run`     |
| Scheduled Task/CronJob abuse             | Admission control to restrict CronJobs/Jobs creation           |
| Privileged container execution           | Enforce seccomp, AppArmor, restrict hostPath/hostNetwork       |
| Runtime code execution inside containers | Falco, anomaly detection on process trees and network behavior |

***

### Final Summary

Defending against Execution focuses on:

* **Blocking dangerous pod specs** (before they run)
* **Restricting who can execute commands** (and how)
* **Detecting unauthorized execution quickly** (at runtime)
* **Containing any execution that does happen** (sandbox + network restrict)
