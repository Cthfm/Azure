---
hidden: true
---

# Enabling Logs for Log Analytics Workspace

## Overview:

The following section ensures that you have logging enabled within your storage account, key vault, Entra, and Resource Graph.

### Entra ID Logs:

The following section shows how to enable Entra ID Logging:

#### 1. Search for Microsoft Entra ID

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

#### 2.  Select Diagnostic settings from the left pane.&#x20;

<figure><img src=".gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. Select Add Diagnostic Setting

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

#### 4. Name the Diagnostic Setting 'SecLab' and point it to sec-lab-logs. Ensure to select all options with a blue checkmark.&#x20;

<figure><img src=".gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### Azure Activity Logs

#### 1. Search for Azure Monitor as shown in the screenshot below.&#x20;

<figure><img src=".gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Select Activity Log and  'Export Activity Logs'

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

#### 3. Select 'Add Diagnostic Setting'

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

#### 4. Name the Diagnostic Setting as 'sec-lab' and point it to 'sec-lab-logs'. Ensure to select all with a blue checkmark.&#x20;

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### Storage Account Logging

#### 1. Under the Azure Monitor section select 'Diagnostic Settings'.



<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### 2. Under the current subscription look for the tfstate\<randomnumbers> storage account and select blob storage.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### 3. Name the diagnostic setting 'sec-lab' and forward to sec-lab-logs. Enable those with a blue check mark.&#x20;

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Key Vault Logging

{% hint style="warning" %}
Terraform has already deployed the associated logs but here are instructions on how to do it in the portal.
{% endhint %}

#### 1. Select the associated subscription and permission

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

#### 2. Select the 'sec-lab-keyvault'

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

3. Name the Diagnostic Setting as 'sec-lab' forwarding to 'sec-lab-logs' configured with the associated blue check marks.&#x20;

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### Flow Logs

#### 1. Select Network Watcher and select 'flow logs'

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

#### 2. Select Create Flow Log

<figure><img src=".gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

#### 3. Configure a VNET Flow Log with the appropriate 'sec-lab-vnet' in your provisioned flow log storage account

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
