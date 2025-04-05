# Defensive Strategies

## **Defensive Strategies Against Privilege Escalation in Containerized Environments**

Privilege Escalation techniques allow adversaries to move from low-privileged users or pods to higher privileges — gaining control over more resources, nodes, or the entire cluster.\
Your goal is to block escalation paths, detect suspicious privilege changes, and enforce least privilege everywhere.

***

### 1. **Enforce Strong Pod Security Standards**

| Action                                                                      | Why It Matters                                               |
| --------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Enforce PodSecurity Admission "restricted" mode (or OPA/Kyverno equivalent) | Blocks privileged containers, hostPath, hostPID, hostNetwork |
| Disallow adding Linux capabilities (`capAdd`) like `SYS_ADMIN`, `NET_ADMIN` | No unnecessary kernel-level powers                           |
| Force non-root users in containers                                          | No `USER 0` in container images                              |

Stops container-based privilege escalation through misconfigured security contexts (T1611 – Escape to Host).

***

### 2. **Tighten RBAC and Role Assignment**

| Action                                                                       | Why It Matters                                         |
| ---------------------------------------------------------------------------- | ------------------------------------------------------ |
| Grant only necessary permissions at namespace and cluster levels             | Enforce least privilege — deny broad access by default |
| Prevent `cluster-admin` bindings unless absolutely necessary                 | Attackers love landing on cluster-admin                |
| Monitor for creation or modification of RoleBindings and ClusterRoleBindings | Detect escalations in progress                         |

Blocks abuse of account manipulation and exploitation to cause privilege escalation. &#x20;

***

### 3. **Restrict Sensitive Kubernetes API Access**

| Action                                                                  | Why It Matters                                                      |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Block pod creation/update permissions to low-trust service accounts     | Attackers can't deploy their own privileged pods                    |
| Restrict `create pods/exec` to trusted users only                       | Stops using kubectl exec for hidden privilege escalation            |
| Use Azure Entra ID Pod Identity or Workload Identity with tight scoping | Azure AKS best practice for least privilege at cloud identity layer |

Defends against privilege escalation via Kubernetes-native resources like new pods, Jobs, or access tokens.

***

### 4. **Restrict Node Access and Protect Node Components**

| Action                                                            | Why It Matters                                                    |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| Block hostPath mounts in pods unless strictly needed              | Prevent access to `/etc/kubernetes`, `/proc`, or host filesystems |
| Harden kubelet API access — require client certs, IP whitelisting | Kubelet abuse = escalate node control                             |
| Enable AuditD/eBPF monitoring at the node level (Falco, Tracee)   | See escalation attempts on the OS level                           |

Limits lateral movement into the node host, stops container escape attacks.

***

### 5. **Monitor and Detect Escalation Behavior**

| Action                                                                                            | Why It Matters                                        |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Audit Kubernetes API for new RoleBindings, ClusterRoleBindings, or ServiceAccount elevation       | Early warning for privilege escalation                |
| Use Falco to detect high-risk container activity: `privileged: true`, hostPath, hostNetwork usage | Runtime alerts on suspicious containers               |
| Alert on new deployments of pods with `privileged: true` or added `capabilities`                  | Attackers hiding inside scheduled jobs or deployments |

Gives real-time visibility when an attacker attempts escalation.

***

### Defensive Coverage Table (Privilege Escalation)

| Attack Vector                                          | Defensive Strategy                                          |
| ------------------------------------------------------ | ----------------------------------------------------------- |
| Privileged container abuse                             | Enforce PodSecurity restricted mode, block privileged specs |
| RBAC escalation (RoleBinding/ClusterRoleBinding abuse) | Audit and alert on new bindings or broad permissions        |
| HostPath escape                                        | Block hostPath, enforce read-only volumes                   |
| Kubelet API abuse                                      | Harden Kubelet access, require client auth                  |
| Token/service account escalation                       | Rotate and tightly scope Kubernetes ServiceAccounts         |

***

### Final Summary

Defending against Privilege Escalation focuses on:

* **Stopping containers from becoming root on the host** (runtime hardening)
* **Preventing RBAC privilege grants** (tight access control + auditing)
* **Restricting who can deploy powerful workloads** (Admission + Identity hardening)
* **Catching escalation behaviors fast** (Falco + audit log alerts)
