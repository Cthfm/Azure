# Containers

The MITRE ATT\&CK Containers matrix outlines adversarial techniques specific to containerized environments, with a strong emphasis on Kubernetes, the dominant orchestration platform. In Kubernetes contexts—such as those deployed in Azure Kubernetes Service (AKS)—attackers may exploit misconfigured RBAC, exposed API servers, or compromised container images to gain initial access. From there, they can escalate privileges by compromising service accounts, abusing mounted secrets, or escaping container boundaries. Techniques like Pod Enumeration, Credential Dumping via mounted volumes, and accessing the Kubernetes API Server are central to lateral movement and privilege escalation. Adversaries may also persist by deploying malicious Pods or DaemonSets, or by modifying admission controllers. Logging blind spots, ephemeral workloads, and multi-tenant complexity make detection challenging, especially in dynamic AKS clusters. As such, defending containerized environments requires securing control plane components, hardening node configurations, and monitoring runtime behavior to detect deviations from expected workloads.



## **⚠️🚧 This section is under construction ⚠️🚧**&#x20;
