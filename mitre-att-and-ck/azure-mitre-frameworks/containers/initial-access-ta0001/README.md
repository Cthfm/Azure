# Initial Access (TA0001)

#### Initial Access Techniques in Containerized Environments

In Kubernetes and other containerized ecosystems, adversaries use Initial Access techniques to establish a foothold in the environment. This includes exploiting vulnerabilities in exposed services, abusing weak or default credentials, and accessing remote administrative interfaces like Kubernetes dashboards or cloud metadata APIs. Successful initial access provides the entry point needed to deploy containers, execute commands, or escalate privileges within the cluster.

#### Exploit Public-Facing Application (T1190)

**Description**: Exploiting vulnerabilities in containerized web apps or APIs to gain a foothold.

**Container Example**:

* Exploit a vulnerable web app running in a Docker container exposed via Kubernetes Ingress or NodePort.
* Attack outdated CMS apps (e.g., WordPress, Joomla) deployed in containers to drop web shells or reverse shells.
*   Abuse container misconfigurations like exposed `/var/run/docker.sock` on the host:

    ```bash
    curl --unix-socket /var/run/docker.sock http://localhost/containers/json
    ```
* Exploit default or misconfigured Helm charts with known CVEs or unauthenticated dashboards (e.g., Kubeapps, Argo CD).

#### External Remote Services (T1133)

**Description**: Leverage exposed remote access or management services running in or around containers.

**Container Example**:

* Access exposed services like SSH, VNC, or RDP from containers due to poor network segmentation.
*   Abuse Kubernetes API server unauthenticated access if RBAC and network policies are weak:

    ```bash
    curl https://<kube-api-server>:6443/api/v1/pods --insecure
    ```
* Access internal management interfaces exposed externally, like Docker Swarm Manager APIs or Kubernetes dashboards.

***

#### Valid Accounts (T1078)

**🛑 Default Accounts (T1078.001)**

**Description**: Use default container or cluster credentials left unchanged post-deployment.

**Container Example**:

* Log in with default Docker registry credentials (e.g., admin/admin on private Harbor registries).
*   Use Kubernetes with default `kubeconfig` in home directories or publicly exposed GitHub repositories:

    ```bash
    kubectl --kubeconfig ~/Downloads/kubeconfig.yaml get pods
    ```
*   Abusing default service accounts in Kubernetes that have excessive RBAC permissions:

    ```bash
    kubectl auth can-i --as=system:serviceaccount:default:default '*' '*'
    ```

**Local Accounts (T1078.003)**

**Description**: Compromise local user accounts in the container host or management nodes.

**Container Example**:

* Brute-force or steal credentials from `/etc/shadow` if host is compromised via container breakout.
*   Mount host directories (e.g., `/home`, `/etc`) into containers and extract local credentials:

    ```bash
    docker run -v /etc:/mnt alpine cat /mnt/passwd
    ```
* Use local access via compromised pod to escalate and access other nodes in the cluster (pivoting inside the K8s network).
