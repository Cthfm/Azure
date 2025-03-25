# Enabling Logs for Log Analytics Workspace

Overview:

The following section ensures that you have logging enabled within your storage account, key vault, Entra, and Resource Graph.

### Entra ID Logs:

The following section shows how to enable Entra ID Logging:

#### 1. Search for Microsoft Entra ID

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 2.  Select Diagnostic settings from the left pane.&#x20;

<figure><img src=".gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. Select Add Diagnostic Setting

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 4. Name the Diagnostic Setting 'SecLab' and point it to sec-lab-logs. Ensure to select all options with a blue checkmark.&#x20;

{% hint style="success" %}
Note that Identity based logs were omitted as they require a P2 license. This was done in order to reduce lab costs. You can simply get them enabled by purchasing a P2 licensed user.&#x20;
{% endhint %}



<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Azure Activity Logs

#### 1. Search for Azure Monitor as shown in the screenshot below.&#x20;

<figure><img src=".gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Select Activity Log and  'Export Activity Logs'

<figure><img src=".gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. Select 'Add Diagnostic Setting'

<figure><img src=".gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

#### 4. Name the Diagnostic Setting as 'sec-lab' and point it to 'sec-lab-logs'. Ensure to select all with a blue checkmark.&#x20;

<figure><img src=".gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

### Storage Account Logging

#### 1. Under the Azure Monitor section select 'Diagnostic Settings'.



<figure><img src=".gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Under the current subscription look for the tfstate\<randomnumbers> storage account and select blob storage.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### 3. Name the diagnostic setting 'sec-lab' and forward to sec-lab-logs. Enable those with a blue check mark.&#x20;

<figure><img src=".gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

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

### Flow Logs - VNET

#### 1. Select Network Watcher and select 'flow logs'

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

#### 2. Select Create Flow Log

<figure><img src=".gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

#### 3. Configure a VNET Flow Log with the appropriate 'sec-lab-vnet' in your provisioned flow log storage account

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

### Flow Logs - NSG

{% hint style="success" %}
NSG flow logs were created as part of the Terraform code. As a heads up per Microsoft:

_On September 30, 2027, network security group (NSG) flow logs will be retired. As part of this retirement, you'll no longer be able to create new NSG flow logs starting June 30, 2025. We recommend_ [_migrating_](https://learn.microsoft.com/en-us/azure/network-watcher/nsg-flow-logs-migrate) _to_ [_virtual network flow logs_](https://learn.microsoft.com/en-us/azure/network-watcher/vnet-flow-logs-overview)_, which overcome the limitations of NSG flow logs._&#x20;

These logs are already deployed within the tenant.
{% endhint %}



### DNS Queries

{% hint style="success" %}
This is currently in preview and can confirm that there is no Terraform Support at this time. Thus needs to be created via the portal.&#x20;
{% endhint %}

#### 1. Search for 'DNS Security' in the Azure Portal

<figure><img src=".gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

#### 2. Create a DNS Security Policy by selecting 'Create'

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### 3. Create the Security DNS policy as shown below

<figure><img src=".gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

#### 4. Select the associated VNET as shown.



<figure><img src=".gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

#### 5. Ensure the proper VNET is selected and then hit 'Review+Create''





<figure><img src=".gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>



