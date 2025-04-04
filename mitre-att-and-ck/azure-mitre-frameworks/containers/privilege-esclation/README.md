# Privilege Esclation

### Privilege Escalation in Containerized Environments

In containerized ecosystems like Kubernetes and Docker, attackers use privilege escalation techniques to move from limited container access to root privileges, host-level compromise, or broader cluster control. These actions often involve escaping containers, abusing default accounts, exploiting misconfigured service roles, or hijacking system processes and orchestration tasks.

#### Account Manipulation → **Additional Container Cluster Roles (T1098.004)**

**Description**: Abuse cluster-role bindings to elevate privileges within Kubernetes.

**Container Example**:

*   A low-privileged service account is granted `cluster-admin`:

    ```bash
    kubectl create clusterrolebinding pe-escalation --clusterrole=cluster-admin --serviceaccount=default:compromised-sa
    ```
* Modify an existing role binding to include attacker identity or service account.

**Impact**:

* Grants full control over the cluster, including node access, secret retrieval, and pod spawning.

#### Create or Modify System Process → **Container Service (T1543.003)**

**Description**: Modify containerized processes or init systems to run with elevated privileges.

**Container Example**:

*   Replace the command in a Deployment or DaemonSet to launch a shell as root:

    ```bash
    kubectl patch deployment app -p '{"spec":{"template":{"spec":{"containers":[{"name":"app","command":["/bin/bash"]}]}}}'
    ```
* Abuse init containers or host-mounted volume paths to inject malicious services.

#### Escape to Host (T1611)

**Description**: Break out of a container to execute commands on the host system.

**Container Example**:

*   Exploit a privileged container to mount the host and chroot:

    ```bash
    docker run -v /:/mnt --privileged --rm -it alpine chroot /mnt
    ```
* Abuse Kubernetes with misconfigured `hostPID`, `hostNetwork`, or `hostPath` mounts.

**Known Tactics**:

* Mount `/proc`, `/sys` from host and inject code into host-level binaries.
* Run container with `--cap-add=SYS_ADMIN` and abuse Linux namespaces to escape.

#### Exploitation for Privilege Escalation (T1068)

**Description**: Exploit container runtime flaws or kernel vulnerabilities to escalate privileges.

**Container Example**:

*   Use dirtypipe, cgroups escape, or misconfigured container runtimes (e.g., containerd or runc vuln):

    ```bash
    gcc -o exploit dirtypipe.c && ./exploit
    ```
* Known exploits:
  * CVE-2019-5736 (runc escape)
  * Dirty Pipe (CVE-2022-0847)
  * cr8escape (containerd bug)

**Post-Exploitation**:

* If running on managed cloud K8s (e.g., EKS/GKE), use host access to extract cloud metadata or tokens.

#### Scheduled Task/Job → **Container Orchestration Job (T1053.007)**

**Description**: Abuse `CronJob` or long-running Job to escalate or maintain root access.

**Container Example**:

*   CronJob is scheduled to restart with elevated privileges or mount host volumes:

    ```yaml
    yamlCopyEditcontainers:
      - name: escalate
        image: busybox
        volumeMounts:
          - mountPath: /host
            name: host-mount
        command: ["sh", "-c", "chroot /host bash"]
    ```

**Impact**:

* Persistent, timed privilege escalation backdoor across cluster lifecycle.

#### &#x20;Valid Accounts → **Default Accounts (T1078.001)**

**Description**: Abuse default service accounts with over-permissioned roles to elevate access.

**Container Example**:

*   Default service account (`default/default`) can list secrets or create pods:

    ```bash
    bashCopyEditkubectl get secrets
    kubectl create pod ...
    ```

**Offensive Tactic**:

* Harvest token at `/var/run/secrets/kubernetes.io/serviceaccount/token` and use `kubectl` or API to escalate.

#### &#x20;Valid Accounts → **Local Accounts (T1078.003)**

**Description**: Use of existing local accounts on container host or inside image to escalate access.

**Container Example**:

*   SSH into container host with known creds, then escalate via `sudo`, suid binaries, or poorly configured PAM:

    ```bash
    bashCopyEditssh user@node
    sudo su -
    ```

**Persistence Path**:

* Add user to `sudoers`, install SSH key, or modify init scripts for future root access.

#### Summary Table

| Technique             | Sub-Technique            | Container Use Case                                 |
| --------------------- | ------------------------ | -------------------------------------------------- |
| Account Manipulation  | Additional Cluster Roles | Grant `cluster-admin` to attacker/service account  |
| Modify System Process | Container Service        | Patch workloads to run as root or launch shell     |
| Escape to Host        | —                        | Use privileged pod + `hostPath` to chroot host     |
| Exploitation for PE   | —                        | Run Dirty Pipe or runc exploits from container     |
| Scheduled Task        | Orchestration Job        | Deploy CronJob to escalate or re-gain host shell   |
| Valid Accounts        | Default Accounts         | Abuse default service account tokens               |
| Valid Accounts        | Local Accounts           | Reuse SSH/root credentials or exploit sudo on host |
