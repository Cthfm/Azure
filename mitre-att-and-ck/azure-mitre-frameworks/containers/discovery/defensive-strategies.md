# Defensive Strategies

## **Defensive Strategies Against Discovery in Containerized Environments**

Discovery techniques help adversaries map the environment after gaining initial access. They enumerate pods, services, secrets, network paths, and RBAC permissions to plan lateral movement, privilege escalation, or exfiltration.

Your goal is to minimize unnecessary visibility, control information exposure, log and detect reconnaissance activities, and restrict discovery powers.

***

### 1. **Restrict Kubernetes API Permissions**

| Action                                                                                     | Why It Matters                                           |
| ------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| Enforce strict RBAC controls — least privilege modes                                       | Only trusted identities can list pods, services, secrets |
| Deny pod/service/secret listing (`get`, `list`, `watch`) to low-privileged ServiceAccounts | Attackers can't enumerate cluster resources easily       |
| Regularly audit RoleBindings and ClusterRoleBindings                                       | Remove over-permissioned accounts and stale bindings     |

&#x20;Prevents wide spread ability to discover resources

***

### 2. **Limit Internal Service Discovery**

| Action                                                                                           | Why It Matters                                   |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------ |
| Apply Kubernetes Network Policies (Calico, Cilium) to block unnecessary pod-to-pod communication | Attackers can't scan the internal network easily |
| Default-deny egress/ingress traffic and whitelist allowed communications                         | Minimize attack surface across services          |
| Use service meshes (Istio, Linkerd) with authenticated service-to-service communication (mTLS)   | Authenticate pods before allowing communication  |

Defends against network service discovery&#x20;

***

### 3. **Protect Secrets and Metadata**

| Action                                                                              | Why It Matters                                                   |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
|  Encrypt Kubernetes Secrets at rest (Azure Key Vault / Azure KMS)                   | Secrets remain protected even if listed                          |
| Block containers from accessing cloud metadata APIs (IMDS) unless explicitly needed | Prevent stealing cloud credentials for additional reconnaissance |
| Use external secrets management instead of Kubernetes Secrets when possible         | Secrets aren’t even stored inside the cluster                    |

Reduces damage if an attacker lists secrets (T1552 – Unsecured Credentials).

***

### 4. **Audit and Monitor Discovery Attempts**

| Action                                                                                                    | Why It Matters                                             |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Enable Kubernetes API audit logging (capture `list`, `get`, `watch` verbs)                                | See discovery attempts via Kubernetes API                  |
| Deploy Falco to detect mass listing of pods, services, secrets (`kubectl get all`, `kubectl get secrets`) | Detect bulk enumeration from compromised pods              |
| Alert on suspicious pod-to-pod communications, nmap, mass curls, or DNS abuse                             | Discovery often precedes lateral movement and exfiltration |

Catch discovery in real time before escalation.

***

### 5. **Segregate and Isolate Sensitive Resources**

| Action                                                                               | Why It Matters                                                            |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| Use separate namespaces for sensitive workloads (e.g., `prod`, `security`, `vault`)  | Logical separation reduces visibility                                     |
| Enforce namespace-specific RBAC (no cross-namespace reads unless explicitly allowed) | No "one pod sees everything" setups                                       |
| Create network segmentation between critical and non-critical applications           | Even if discovered, sensitive systems are protected by network boundaries |

Adds friction to discovery and pivot attempts.

***

### Defensive Coverage Table (Discovery)

| Attack Vector                       | Defensive Strategy                                             |
| ----------------------------------- | -------------------------------------------------------------- |
| Kubernetes API resource enumeration | Strict RBAC, audit logging on `list`, `get`, `watch` API calls |
| Internal network scanning           | Network Policies, service mesh mTLS, alert on scanning tools   |
| Secret discovery                    | Encrypt secrets, externalize secrets management, limit access  |
| Metadata service enumeration        | Block pod access to metadata APIs, monitor IMDS queries        |
| Pod/service enumeration             | Namespace isolation, no cross-namespace access by default      |

***

### Final Summary

Defending against Discovery focuses on:

* Controlling what identities can see and list (strict RBAC + logging)
* Locking down network visibility (NetworkPolicies + mTLS)
* Protecting critical secrets and metadata endpoints
* Detecting reconnaissance early (Falco + Kubernetes audit logs)
