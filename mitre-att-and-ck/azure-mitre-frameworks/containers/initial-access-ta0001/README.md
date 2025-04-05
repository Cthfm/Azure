# Initial Access (TA0001)

## **Initial Access Techniques in Containerized Environments**

In Kubernetes and other containerized ecosystems, adversaries use Initial Access techniques to establish a foothold within container clusters or hosts.\
This is often achieved by exploiting exposed services, abusing weak or default credentials, or accessing misconfigured remote administrative interfaces like Kubernetes APIs, Docker sockets, or dashboards.

Successful initial access enables the attacker to deploy containers, execute code, steal secrets, or move laterally inside the containerized environment.

***

### Exploit Public-Facing Application **T1190**&#x20;

**Description**:\
Exploit vulnerabilities in containerized web applications, APIs, or services exposed to the public internet to gain unauthorized access.

**Container Example**:

* Exploit a vulnerable containerized web app exposed via Kubernetes Ingress, LoadBalancer, or NodePort services.
* Attack outdated CMS applications (e.g., WordPress, Joomla) running inside containers to upload web shells or initiate reverse shells.
* Abuse misconfigured Docker API sockets exposed to the network:

```bash
curl --unix-socket /var/run/docker.sock http://localhost/containers/json
```

* Exploit misconfigured or unauthenticated Helm charts and dashboards (e.g., Kubeapps, Argo CD) to gain control of workloads.

**Result**: External foothold into container workloads, pods, or underlying infrastructure.

***

### External Remote Services **T1133**&#x20;

**Description**:\
Leverage exposed remote management or access services running inside or near containers to gain entry.

**Container Example**:

* Access externally exposed SSH, VNC, RDP, or database services that should be internally restricted.
* Abuse misconfigured Kubernetes API server allowing unauthenticated requests due to weak RBAC or missing network policies:

```bash
curl https://<kube-api-server>:6443/api/v1/pods --insecure
```

* Connect to exposed Docker Swarm APIs, Kubernetes dashboards, or other internal management interfaces mistakenly exposed to the public.

**Result**: Unauthorized access through weak external service exposure.

***

### Valid Accounts **T1078**&#x20;

**Description**:\
Leverage valid credentials to authenticate to container registries, Kubernetes clusters, or cloud-native management interfaces without needing to exploit vulnerabilities.

Attackers seek to abuse legitimate access paths  either by using default, leaked, or stolen credentials to blend into normal operations and avoid detection.

**Result**:\
Move through container environments unnoticed, posing as legitimate users or workloads.

**🛑 Default Accounts** **T1078.001**&#x20;

**Description**:\
Use default container or cluster credentials left unchanged after deployment to authenticate.

**Container Example**:

* Log in with default Docker registry credentials (e.g., `admin/admin` on private Harbor registries).
* Use Kubernetes cluster configurations found on public GitHub repositories:

```bash
kubectl --kubeconfig ~/Downloads/kubeconfig.yaml get pods
```

* Abuse Kubernetes default service accounts with overly broad permissions:

```bash
kubectl auth can-i --as=system:serviceaccount:default:default '*' '*'
```

**Result**: Access through overlooked, insecure default credentials.

***

### **Local Acccounts T1078**

**Description**:\
Use legitimate credentials to gain unauthorized access to containerized environments or orchestration platforms.

Adversaries may obtain default, leaked, stolen, or exposed credentials for container registries, Kubernetes clusters, Docker APIs, or cloud-native management consoles.\
By using valid credentials, attackers can blend into normal activity, evade detection, and bypass perimeter defenses without exploiting vulnerabilities.

✅ **Result**:\
Silent, authorized access to container workloads, management APIs, and sensitive resources — enabling further actions like deployment, privilege escalation, or data theft.

### **Local Accounts** **T1078.003**&#x20;

**Description**:\
Compromise local accounts on the container host or nodes managing the cluster to escalate access.

**Container Example**:

* Brute-force or steal credentials from `/etc/shadow` if the host is compromised through a container escape.
* Mount sensitive host directories into a container and extract credentials:

```bash
docker run -v /etc:/mnt alpine cat /mnt/passwd
```

* Use pod-level compromise to pivot laterally inside the Kubernetes cluster via compromised local accounts or node-level access.

**Result**: Move deeper into the container environment and underlying infrastructure.

***

## **Initial Access Techniques in Containerized Environments Summary**

| Technique/Subtechnique            | MITRE ID  | Container Example                              |
| --------------------------------- | --------- | ---------------------------------------------- |
| Exploit Public-Facing Application | T1190     | Exploit web apps, Docker socket, Helm charts   |
| External Remote Services          | T1133     | Access exposed SSH, Kubernetes API server      |
| Default Accounts                  | T1078.001 | Abuse default Docker or Kubernetes credentials |
| Local Accounts                    | T1078.003 | Compromise local host accounts via containers  |

***

## Final Summary

Defending against Initial Access in containerized environments focuses on:

* **Patching containerized apps and platforms** (Kubernetes, Docker, registries)
* **Securing exposed services with strict network segmentation**
* **Enforcing strong credential management (no defaults!)**
* **Hardening the Kubernetes API server and internal management interfaces**
