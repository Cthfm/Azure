# Virtual Machine Containment

### **Virtual Machine (VM) Containment**

#### **Isolating Compromised VMs**

**Method:** Use Network Security Groups (NSGs) to block external access via portal

**Steps:**

1. Navigate to NSG settings.
2. Block all inbound and outbound traffic for the compromised VM.

#### **Using Just-in-Time (JIT) Access**

* **Objective:** Limit RDP/SSH access to authorized users.
* **Method:** Enable JIT access for VMs.
* **Steps:**
  1. Navigate to **Defender for Cloud > JIT Access**.
  2. Configure JIT policies for critical VMs.

#### **Creating Snapshots for Forensic Investigation**

* **Objective:** Preserve system state for later analysis.
* **Method:** Create a VM snapshot.
* **Steps:**
  1. Navigate to **Disks** in the Azure portal.
  2. Select the disk and create a **snapshot**.

#### **Defender for Cloud VM Threat Detection**

* **Objective:** Identify and contain threats to virtual machines.
* **Method:** Enable Defender for Cloud alerts and take action.
