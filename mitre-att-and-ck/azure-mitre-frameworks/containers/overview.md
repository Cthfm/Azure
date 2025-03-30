---
hidden: true
---

# Overview

### 🔐 **Initial Access**

| Technique                                 | Sub-Technique    | Containerized Use Case                                              |
| ----------------------------------------- | ---------------- | ------------------------------------------------------------------- |
| T1190 – Exploit Public-Facing Application | —                | Exploit vulnerable web apps (e.g., NodePort, Ingress) to gain shell |
| T1133 – External Remote Services          | —                | Access exposed dashboards (ArgoCD, Jenkins) or SSH into cloud node  |
| T1078 – Valid Accounts                    | Default Accounts | Use default dashboard creds (`admin:admin`) or Helm chart secrets   |
|                                           | Local Accounts   | SSH using weak host credentials (`ubuntu:ubuntu`)                   |

***

### ⚙️ **Execution Techniques (Corrected Table)**

| Technique                                    | Sub-Technique               | Containerized Use Case                                                                                            |
| -------------------------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **T1609** – Container Administration Command | —                           | Use `kubectl exec`, `docker exec`, or unauthenticated Kubelet API (`/exec`, `/run`) to spawn shells in containers |
| **T1610** – Deploy Container                 | —                           | Launch attacker-controlled containers (e.g., `kubectl run` with reverse shell or crypto miner)                    |
| **T1053.007** – Scheduled Task/Job           | Container Orchestration Job | Create `CronJob` or `Job` that periodically executes commands (e.g., curl payloads, persistence scripts)          |
| **T1204.003** – User Execution               | Malicious Image             | Trick CI/CD pipelines or users into pulling and running malicious images from public or private registries        |

***

### 🔒 **Persistence**

| Technique                         | Sub-Technique               | Containerized Use Case                                     |
| --------------------------------- | --------------------------- | ---------------------------------------------------------- |
| T1098.004 – Account Manipulation  | Cluster Roles               | Add attacker to `cluster-admin` via `clusterrolebinding`   |
| T1136.001 – Create Account        | Local Account               | Create system user via host escape or privileged container |
| T1543.003 – Modify System Process | Container Service           | Patch DaemonSets/Deployments to run attacker code          |
| T1133 – External Remote Services  | —                           | SSH or reverse shell listener inside pod                   |
| —                                 | Implant Internal Image      | Push backdoored image to internal registry                 |
| T1053.007 – Scheduled Task        | Container Orchestration Job | Persistent CronJob used to regain access                   |
| T1078 – Valid Accounts            | Default Accounts            | Exploit over-permissioned default service accounts         |
|                                   | Local Accounts              | Use host SSH account to retain shell                       |

***

### 🚀 **Privilege Escalation**

| Technique                         | Sub-Technique               | Containerized Use Case                                            |
| --------------------------------- | --------------------------- | ----------------------------------------------------------------- |
| T1098.004 – Account Manipulation  | Cluster Roles               | Elevate permissions via RoleBinding/ClusterRoleBinding            |
| T1543.003 – Modify System Process | Container Service           | Modify pod/daemon specs to run as root or with added capabilities |
| T1611 – Escape to Host            | —                           | Privileged pod with `hostPath` or `chroot` into host FS           |
| T1068 – Exploitation for PE       | —                           | DirtyPipe, runc escape, or host kernel exploit                    |
| T1053.007 – Scheduled Task        | Container Orchestration Job | CronJob that auto-runs escalated commands or mounts host          |
| T1078 – Valid Accounts            | Default Accounts            | Abuse default token for full cluster access                       |
|                                   | Local Accounts              | `sudo su -` on cloud VM or host node                              |

***

### 🫥 **Defense Evasion**

| Technique                               | Sub-Technique            | Containerized Use Case                                      |
| --------------------------------------- | ------------------------ | ----------------------------------------------------------- |
| T1610.001 – Build Image on Host         | —                        | Build malicious image locally to bypass scanning            |
| T1610 – Deploy Container                | —                        | Launch shell using trusted image name (`alpine`, `busybox`) |
| T1562.001 – Impair Defenses             | Disable/Modify Tools     | Kill `Falco`, disable audit logs, remove AppArmor           |
| T1070 – Indicator Removal               | —                        | Delete shell history, logs inside container, wipe PVCs      |
| T1036.005 – Masquerading                | Match Legit Name         | Name pod `metrics-server` or image `nginx:latest`           |
| T1036.003 – Masquerade Account Name     | —                        | Use SA name like `grafana-agent`, `backup-admin`            |
| T1550.001 – Use Alternate Auth Material | App Token                | Steal Kubernetes SA token or cloud metadata IAM token       |
| T1078 – Valid Accounts                  | Default & Local Accounts | Leverage unrotated passwords or SSH keys on host            |

***

### 🔑 **Credential Access**

| Technique                         | Sub-Technique        | Containerized Use Case                                             |
| --------------------------------- | -------------------- | ------------------------------------------------------------------ |
| T1110.001 – Brute Force           | Password Guessing    | Use Hydra to brute exposed web UIs                                 |
| T1110.003 – Password Spraying     | —                    | Attempt common passwords across multiple usernames                 |
| T1110.004 – Credential Stuffing   | —                    | Use breached creds from pastebins or source code leaks             |
| T1528 – Steal App Access Token    | —                    | Grab SA token from `/var/run/...` or metadata APIs                 |
| T1552.001 – Unsecured Credentials | Credentials in Files | Read `.env`, kubeconfig, secret volumes                            |
| T1552.007 – Unsecured Credentials | Container API        | Query Docker socket or Kubelet API for container info and env vars |

***

### 🚗 **Lateral Movement**

| Technique                               | Sub-Technique    | Containerized Use Case                                                                        |
| --------------------------------------- | ---------------- | --------------------------------------------------------------------------------------------- |
| T1550.001 – Use Alternate Auth Material | App Access Token | Use stolen K8s SA or cloud metadata token to access other pods, namespaces, or cloud services |

***

### 📦 **Collection**

| Technique                      | Sub-Technique | Containerized Use Case                                 |
| ------------------------------ | ------------- | ------------------------------------------------------ |
| T1005 – Data from Local System | —             | Read mounted volumes, log files, config secrets        |
| T1119 – Automated Collection   | —             | Use `kubectl get all`, scripts, or tools like Peirates |
| T1056 – Input Capture          | —             | Deploy sidecars with MITM, tcpdump, or reverse proxies |

***

### 📤 **Exfiltration**

| Technique                    | Sub-Technique | Containerized Use Case                             |
| ---------------------------- | ------------- | -------------------------------------------------- |
| T1041 – Over C2 Channel      | —             | Use `curl` or `nc` to send data to attacker server |
| T1567.002 – To Cloud Storage | —             | Push data to S3/GCS with compromised tokens        |
| T1048 – Over Alt Protocol    | —             | Use DNS tunneling, FTP, IRC, or nonstandard ports  |

***

### 💥 **Impact**

| Technique                       | Sub-Technique | Containerized Use Case                                   |
| ------------------------------- | ------------- | -------------------------------------------------------- |
| T1485 – Data Destruction        | —             | `rm -rf /mnt/data`, delete Secrets, wipe backups         |
| T1499 – Endpoint DoS            | —             | Flood API/Ingress with large payloads or recursive calls |
| T1490 – Inhibit Recovery        | —             | Delete PVCs, revoke IAM backup access, wipe logs         |
| T1498 – Network DoS             | —             | Flood Kube-proxy or service mesh with traffic            |
| T1496.001 – Compute Hijacking   | —             | Deploy crypto miner pods, abuse CI/CD runners            |
| T1496.002 – Bandwidth Hijacking | —             | Host TOR proxy or exfiltrator to consume egress traffic  |
