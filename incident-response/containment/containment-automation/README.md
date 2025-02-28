# Containment Automation

### **Automated Containment with Microsoft Sentinel Playbooks**

#### **Auto-Disabling High-Risk Entra ID Accounts**

* **Objective:** Automate security responses.
* **Method:** Use Sentinel Playbooks.
* **Example Playbook JSON:**

```
{
  "Trigger": "Microsoft Sentinel Alert",
  "Condition": "SigninLogs: RiskLevel = 'High'",
  "Action": "Disable Entra ID User"
}
```

#### **Blocking Malicious IPs Automatically**

* **Objective:** Use Sentinel Playbooks to dynamically update NSG rules.
* **Steps:**
  1. Create a **Logic App** in Sentinel.
  2. Define a trigger for high-risk IP detection.
  3. Add an action to block the IP.
