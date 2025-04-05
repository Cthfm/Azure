# Privilege Esclation

## **Privilege Escalation Techniques in Containerized Environments**

In Kubernetes and Docker ecosystems, adversaries use Privilege Escalation techniques to move from limited container access to root privileges, host-level compromise, or full cluster control.\
This escalation is often achieved by escaping containers, abusing default accounts, manipulating roles, or exploiting runtime vulnerabilities.

***

### **Account Manipulation: 1098**

Account Manipulation refers to adversaries creating, modifying, or hijacking legitimate accounts to gain or maintain access to a target environment.\
Instead of exploiting software vulnerabilities, attackers abuse the identity layer — altering permissions, adding backdoor users, or hijacking service accounts.

In containerized ecosystems like Kubernetes or Docker, this often means:

* Creating or modifying Kubernetes ServiceAccounts
* Adding attacker-controlled identities to ClusterRoleBindings
* Adjusting RBAC rules to grant elevated privileges
* Modifying user configurations on the container host

By embedding themselves into the environment’s identity and access management fabric, adversaries ensure long-term persistence and stealthy movement.

#### Additional Container Cluster Roles T1098.004

**Description**:\
Abuse Kubernetes ClusterRoleBindings to elevate privileges from a low-privileged service account or user.

**Container Example**:

* A compromised service account escalates to `cluster-admin`:

```bash
kubectl create clusterrolebinding pe-escalation --clusterrole=cluster-admin --serviceaccount=default:compromised-sa
```

* Modify an existing ClusterRoleBinding to add the attacker's service account.

**Result**:\
Full cluster control — node access, secret retrieval, pod spawning, and administrative actions.

***

### Create or Modify System Process T1543

**Description**

Create or Modify System Process refers to adversaries creating new system-level processes or modifying existing ones to ensure malicious code is automatically executed.

In containerized environments, this technique commonly involves:

* Deploying malicious Kubernetes resources (like Deployments, DaemonSets, InitContainers)
* Patching existing workloads to run attacker-controlled code
* Modifying container startup commands or systemd services (on hosts)

The goal is to embed the attacker's code into normal cluster operations, so it runs automatically during routine activities like pod restarts, node joins, or scaling events.

#### Container Service **T1543.003**

**Description**:\
Modify containerized processes or init systems (e.g., Deployments, DaemonSets) to run attacker-controlled code with elevated privileges.

**Container Example**:

* Patch a Deployment to launch a root shell:

```bash
kubectl patch deployment app -p '{"spec":{"template":{"spec":{"containers":[{"name":"app","command":["/bin/bash"]}]}}}'
```

* Abuse InitContainers to inject pre-startup scripts or access host-mounted volumes.

**Result**:\
Malicious processes run with higher privileges, allowing system modification or breakout.

***

### Escape to Host **T1611**&#x20;

**Description**:\
Break out of the container runtime and execute commands directly on the underlying host system.

**Container Example**:

* Mount and chroot into the host filesystem:

```bash
docker run -v /:/mnt --privileged --rm -it alpine chroot /mnt
```

* Abuse Kubernetes `hostPID`, `hostNetwork`, `hostPath` misconfigurations to interact with host resources.

**Result**:\
Escape container isolation, gaining direct host control for further escalation or persistence.

***

### Exploitation for Privilege Escalation **T1068**

**Description**:\
Exploit container runtime vulnerabilities or Linux kernel flaws to escalate privileges.

**Container Example**:

* Compile and run Dirty Pipe (CVE-2022-0847) to gain root:

```bash
gcc -o exploit dirtypipe.c && ./exploit
```

* Exploit CVE-2019-5736 (runc escape) to break container boundaries.

✅ **Result**:\
Privilege escalation from container user to root on the host system, often leading to full node or cluster compromise.

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
Abuse Kubernetes CronJobs or Jobs to maintain or escalate privileges persistently over time.

**Container Example**:

* Deploy a CronJob that mounts the host and chroots:

```yaml
yamlCopyEditcontainers:
- name: escalate
  image: busybox
  volumeMounts:
    - mountPath: /host
      name: host-mount
  command: ["sh", "-c", "chroot /host bash"]
```

**Result:**\
Persistent, scheduled privilege escalation channel that survives reboots and cluster changes.

***

####

#### 👤 Valid Accounts → Default Accounts

\| MITRE ID | **T1078.001** |

**Description**:\
Abuse default Kubernetes service accounts that are over-permissioned and unprotected.

**Container Example**:

* Use the default service account token to list secrets:

```bash
bashCopyEditcat /var/run/secrets/kubernetes.io/serviceaccount/token
kubectl get secrets
```

✅ **Result**:\
Privilege escalation via unrestricted default service account access.

***

### Valid Accounts T1078

Valid Accounts refers to adversaries leveraging existing, legitimate credentials to gain access to systems or environments.

In containerized environments, this often means attackers abuse Kubernetes service accounts, default or exposed credentials, or previously stolen cloud IAM identities to authenticate and operate without raising immediate suspicion.

By using valid accounts, adversaries bypass traditional security controls (like firewall rules or authentication systems) because they appear to be authorized users or services.

#### Local Accounts **T1078.003**

**Description**:\
Use stolen or existing local Linux user accounts on container hosts to escalate privileges.

**Container Example**:

* SSH into the node and escalate privileges:

```bash
ssh user@node
sudo su -
```

* Add attacker SSH keys or add the user to `sudoers` for persistent root access.

**Result**:\
Persistent, privileged access at the host level beyond the container boundary.

***

### **Privilege Escalation Techniques in Containerized Environments Summary**

| Technique/Subtechnique                | MITRE ID  | Container Example                                    |
| ------------------------------------- | --------- | ---------------------------------------------------- |
| Additional Container Cluster Roles    | T1098.004 | Escalate Kubernetes roles                            |
| Container Service Modification        | T1543.003 | Modify deployments/DaemonSets for elevated execution |
| Escape to Host                        | T1611     | Break out of container to access the host            |
| Exploitation for Privilege Escalation | T1068     | Exploit container runtime or kernel vulnerabilities  |
| Container Orchestration Job           | T1053.007 | Abuse CronJobs for persistent escalation             |
| Default Accounts                      | T1078.001 | Abuse default service account tokens                 |
| Local Accounts                        | T1078.003 | SSH and escalate via local host accounts             |

***

### Final Summary

Defending against Privilege Escalation in container environments focuses on:

* **Locking down Kubernetes RBAC** to prevent role abuse
* **Hardening container configurations** (no privileged containers, minimal capabilities)
* **Patching container runtimes and Linux kernels quickly**
* **Monitoring CronJob, DaemonSet, and deployment modifications**
* **Restricting host filesystem access from containers**
