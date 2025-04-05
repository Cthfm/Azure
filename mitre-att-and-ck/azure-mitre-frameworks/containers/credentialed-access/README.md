# Credentialed Access

### Credential Access in Containerized Environments

In containerized infrastructures, adversaries may seek credentials to escalate privileges, move laterally, or maintain persistence. This involves brute-forcing login interfaces (T1110), extracting secrets from files or mounted volumes, and stealing application-level access tokens from metadata services or pods.

***

### **Brute Force T1110**

**Description**

Brute Force refers to adversaries systematically attempting multiple password guesses against authentication mechanisms to gain unauthorized access.

Rather than exploiting vulnerabilities, attackers use guessing techniques (manual or automated) to crack passwords by:

* Trying different passwords for a single user (classic brute-force)
* Trying a single password across multiple users (password spraying)
* Replaying leaked credentials from data breaches (credential stuffing)

In containerized environments like Kubernetes or Docker, brute-force attacks commonly target:

* Exposed web interfaces (e.g., Kubernetes Dashboard, ArgoCD, Grafana)
* Internal authentication portals (e.g., GitLab, Keycloak, Jenkins)
* Private registries (Harbor, Docker Registries)

#### **Password Guessing (T1110.001)**

**Description**: Attempt to guess passwords through repeated login attempts.

**Container Example**:

*   Attacker brute-forces internal services like Redis, MySQL, Jenkins, or dashboards exposed via NodePort/Ingress:

    ```bash
    hydra -l admin -P rockyou.txt http://<service-ip>/login
    ```
* Common targets: ArgoCD, Grafana, Kubeapps, Harbor, Kubernetes Dashboard.

**Goal**: Gain access to exposed services with weak authentication mechanisms.

#### **Password Spraying (T1110.003)**

**Description**: Attempt the same password across multiple accounts to avoid lockout.

**Container Example**:

*   Spray `Password123!` across all known usernames (e.g., from ConfigMaps or public repos):

    ```bash
    hydra -L users.txt -p Password123! http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
    ```

**Realistic Targets**:

* Internal GitLab, Keycloak, internal dashboards with multiple users.

**Credential Stuffing (T1110.004)**

**Description**: Use leaked or stolen username/password pairs to access services.

**Container Example**:

*   Try known breached credentials from `haveibeenpwned`, GitHub leaks, or phishing:

    ```bash
    crackmapexec http <target-ip> -u users.txt -p passwords.txt
    ```

**Kubernetes Specific**:

* Use credentials to authenticate against exposed services, private registries, or web UIs.

***

#### Steal Application Access Token (T1528)

**Description**: Steal cloud provider metadata tokens or service account tokens to impersonate applications.

**Container Example**:

*   Inside compromised container:

    ```bash
    cat /var/run/secrets/kubernetes.io/serviceaccount/token
    ```
*   Azure (from VM, AKS pod):

    ```bash
    curl -H "Metadata:true" "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"
    ```

**Outcome**: Access APIs, Kubernetes clusters, or cloud services without valid user credentials.

***

### Unsecured Credentials T1552

#### **Description**

Unsecured Credentials refers to adversaries searching for and extracting sensitive authentication material stored insecurely across systems.\
Instead of stealing credentials in transit, attackers find secrets at rest — sitting unprotected inside files, containers, mounted volumes, environment variables, APIs, or cloud storage.

In containerized environments, this typically means:

* Finding hardcoded passwords, API keys, or tokens in container images
* Harvesting secrets from mounted Kubernetes volumes
* Pulling environment variables with embedded credentials
* Abusing exposed Docker or Kubernetes APIs to access secret data

Secrets management mistakes are very common in Kubernetes and Docker setups, making this one of the easiest and most damaging attack paths.

#### &#x20;**Credentials in Files (T1552.001)**

**Description**: Extract hardcoded or mounted credentials from known file locations.

**Container Example**:

*   Scan image or mounted volume for:

    ```bash
    find / -name "*.env" -o -name "*.yaml" -o -name "*config*" 2>/dev/null | xargs grep -Ei "pass|token|api_key|secret"
    ```

**Common Targets**:

* Kubernetes secrets accidentally mounted in `/etc/secrets/`, `/var/run/secrets/`, or embedded in container images.

***

#### **Container API (T1552.007)**

**Description**: Abuse exposed container APIs (e.g., Docker API or Kubernetes API) to retrieve secrets or container environment data.

**Container Example**:

*   Access the Docker socket:

    ```bash
    curl --unix-socket /var/run/docker.sock http://localhost/containers/json
    ```
*   Query environment variables with embedded credentials:

    ```bash
    kubectl exec -it <pod> -- env | grep -Ei "secret|key|token"
    ```

**Impact**:

* Retrieve secrets from environment variables, configurations, or even mounted volumes used for automation/authentication.

***

### **Credential Access Techniques in Containers Summary**

| Technique/Subtechnique         | MITRE ID  | Container Example                                     |
| ------------------------------ | --------- | ----------------------------------------------------- |
| Password Guessing              | T1110.001 | Brute-force internal web services                     |
| Password Spraying              | T1110.003 | Spray common passwords across accounts                |
| Credential Stuffing            | T1110.004 | Replay known credential dumps                         |
| Steal Application Access Token | T1528     | Steal service account tokens or cloud metadata tokens |
| Credentials in Files           | T1552.001 | Extract secrets from config files or mounted volumes  |
| Container API                  | T1552.007 | Abuse Docker/Kubernetes APIs to extract secrets       |

***

### Final Summary

Defending against Credential Access in containers focuses on:

* Locking down metadata services and service account token access
* Auditing and securing all credential storage paths
* Enforcing strong passwords and MFA across internal services
* Monitoring for suspicious token or API usage
