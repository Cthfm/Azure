# Defense Strategies

## **Defensive Strategies Against Execution in Azure Environments**

In Azure, defending against Execution means restricting what code can be run, who can deploy workloads, securing serverless and container platforms, and monitoring cloud-native command execution at scale.

You want to trap, restrict, and catch any adversary trying to go active.

***

### Cloud Administration Command (T1651)

| Defensive Action                                                                                                              | Why It Matters                                       |
| ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Apply strict Role-Based Access Control (RBAC) in Azure — only admins can deploy resources or run scripts                      | Least privilege reduces risk of abuse                |
| Require Privileged Identity Management (PIM) for admin roles with Just-in-Time (JIT) activation                               | Attackers can't live on privileged roles permanently |
| Enable Microsoft Defender for Cloud to detect risky operations (e.g., VM extensions, script execution)                        | Alerts when common execution paths are abused        |
| Apply Azure Policy to deny creation of high-risk extensions (CustomScript, RunCommand) unless necessary                       | Block mass deployment of RCE scripts via extensions  |
| Monitor Resource Manager (ARM) activity logs for deployment operations (`Microsoft.Compute/virtualMachines/extensions/write`) | Real-time execution tracking                         |

&#x20;Restricts who can perform cloud-native administrative execution.

***

### Command and Scripting Interpreter → Cloud API T1059.009

Controls who can execute code via direct API interaction.

***

### Serverless Execution

| Defensive Action                                                                                              | Why It Matters                                          |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Apply Azure Policy to restrict serverless deployments to trusted resource groups                              | Attackers can't scatter functions everywhere            |
| Enforce CI/CD pipeline validations for Azure Functions — no direct function edits in production               | Blocks rogue code injection                             |
| Require Azure AD Authentication on Azure Function endpoints                                                   | Stop unauthenticated function trigger abuse             |
| Deploy Functions in VNET-integrated plans whenever possible                                                   | Private execution only — no public serverless endpoints |
| Monitor App Service/Function App deployment events and trigger anomalies (new function, sudden traffic spike) | Detects rapid serverless-based C2 channels              |

Makes serverless code execution safe, validated, and auditable.

***

### User Execution → Malicious Image (T1204.003)

| Defensive Action                                                                                            | Why It Matters                                      |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 📜 Enforce container image signing (e.g., Azure Container Registry + Cosign + Notary)                       | Only signed, trusted images can be deployed         |
| 🔒 Enable Microsoft Defender for Containers (Defender for AKS, ACR) for runtime image scanning              | Detect backdoors at rest and runtime                |
| 🚫 Restrict who can push to Azure Container Registry via RBAC                                               | Block attackers from uploading malicious containers |
| 🛡️ Use Kubernetes admission controllers (Gatekeeper, Kyverno) to validate image sources and configurations | Block unauthorized images before they run           |
| 🔍 Monitor ACR push logs and AKS deployment logs for unapproved images                                      | Detect compromised supply chains                    |

Stops malicious container images from ever reaching execution in AKS, ACI, or App Services.

***

## Defensive Coverage Table (Execution in Azure)

| Attack Vector                     | Defensive Strategy                                                               |
| --------------------------------- | -------------------------------------------------------------------------------- |
| Azure CLI/Portal/PowerShell abuse | Strict RBAC, PIM with JIT, Defender alerts on script execution                   |
| Cloud API exploitation            | Azure Policy resource controls, Defender for APIs, Conditional Access for APIs   |
| Serverless function execution     | Restrict serverless deployment scopes, CI/CD validation, authenticated functions |
| Malicious container images        | Enforce image signing, runtime scanning with Defender, admission controls on AKS |

***

## Final Summary

Defending against Execution in Azure focuses on:

* **Locking down who can run or deploy anything** (RBAC + JIT + Policy)
* **Validating code before it runs** (CI/CD gates, signed images, serverless restrictions)
* **Detecting execution quickly at the control plane and runtime** (Defender, Azure Monitor, Sentinel)
* **Making serverless and container platforms resilient to abuse**
