---
hidden: true
---

# Logging Into Windows VM

Overview:

The following provides a overview of how to login to the Azure VM from the Azure Portal.



### 1. Search for the Key Vault Resource as shown in the snapshot

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### 2. Select the secret that includes the Windows Password

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. Select the current version

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### 4. Copy the password and save it to a notepad

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 5. Search for the VM as shown in the snapshot

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 6. Select Connect and Select 'Connect' from Drop Down

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### 7. Select Download RDP File

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### 8. Select the RDP file from downloads and open it

### 9. Follow the prompts and paste your credentials in

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### **10. Once logged confirm Sysmon and view the configuration**

<figure><img src=".gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Sysmon Documentation: [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)



### **Troubleshooting Tips:**



{% hint style="success" %}
You may get an error that you are unable to RDP to the host. Ensure update your NSG with your current IP address. This may change from day to day. Error snapshot provided below.&#x20;
{% endhint %}

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To resolve this add a rule to your existing NSG by selecting 'Add Incoming NSG Port Rule' in the sec-lab-win11 Connect section.
{% endhint %}

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
A dialog box will open where you can ensure that your current IP is updated.&#x20;
{% endhint %}



<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

