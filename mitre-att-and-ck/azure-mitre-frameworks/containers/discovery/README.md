# Discovery

## **Discovery Techniques in Containerized Environments**

In Kubernetes and containerized ecosystems, adversaries use Discovery techniques to map the environment, understand configurations, and identify potential lateral movement paths. This includes enumerating running containers, resources like Secrets or ConfigMaps, network services between pods, and discovering permission groups (like RBAC roles and bindings). Effective discovery allows attackers to plan privilege escalation, lateral movement, or exfiltration.

#### Container and Resource Discovery&#x20;

Container and Resource Discovery refers to adversaries enumerating information about containerized environments after gaining access.\
Attackers perform discovery activities to map the cluster, identify valuable resources, and plan lateral movement or privilege escalation.

In Kubernetes, Docker, and other orchestrated environments, this typically involves:

* Listing running pods, containers, nodes, or namespaces
* Querying Kubernetes APIs to enumerate secrets, ConfigMaps, and workloads
* Inspecting the cloud provider environment (e.g., metadata APIs for AWS, Azure, GCP)
* Identifying cluster roles, service accounts, and network configurations

Discovery is usually one of the first steps post-compromise, helping attackers understand what control they have and where to pivot next.

**Container Example**:\
After gaining access to a compromised pod, the attacker enumerates all pods across namespaces:

```bash
kubectl get pods --all-namespaces
```

They also list ConfigMaps, Secrets, and Services:

```bash
kubectl get configmaps --all-namespaces
kubectl get secrets --all-namespaces
kubectl get services --all-namespaces
```

This provides detailed visibility into the workloads, sensitive data (Secrets), and service architecture of the cluster.

#### Network Service Discovery **T1046**

**Description**:\
Identify open ports, internal services, and inter-pod communication paths to plan lateral movement or C2 channels.

**Container Example**:\
The attacker scans the Kubernetes network from the compromised pod:

```bash
nmap -sT -p- 10.0.0.0/16
```

Or uses `curl` or `wget` to check common internal service ports manually:

```bash
curl http://10.0.0.5:8080
```

Additionally, they may query Kubernetes Services directly:

```bash
kubectl get svc --all-namespaces
```

This helps map pod-to-pod services, internal load balancers, and potentially exposed web applications that could be targeted next.

#### Permission Groups Discovery **T1069**

**Description**:\
Enumerate Kubernetes RBAC permissions, ServiceAccounts, Roles, and RoleBindings to understand privilege assignments and identify escalation paths.

**Container Example**:\
The attacker queries RBAC settings:

```bash
kubectl get clusterrolebindings
kubectl get rolebindings --all-namespaces
kubectl get serviceaccounts --all-namespaces
```

They also describe specific roles to view associated permissions:

```bash
kubectl describe clusterrole cluster-admin
```

By discovering which accounts have elevated privileges (like access to Secrets, Nodes, or the API server), the attacker can identify ways to escalate access or impersonate more privileged identities.

***

### 📊 Summary Table

| Technique                                | Containerized Use Case                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------ |
| T1613 – Container and Resource Discovery | `kubectl get pods`, `kubectl get secrets`, `kubectl get services`                    |
| T1046 **-** Network Service Discovery    | `nmap`, `curl`, `kubectl get svc` to map internal services                           |
| T1069 - Permission Groups Discovery T    | `kubectl get rolebindings`, `kubectl describe roles` to map RBAC and ServiceAccounts |
