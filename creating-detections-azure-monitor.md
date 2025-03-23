---
hidden: true
---

# Creating Detections: Azure Monitor

## Overview

In this section will create a detection within Azure Monitor that aligns with MITRE Att\&CK.,T1562.008. We will delete the Network Watcher Resource within the tenant and send an email notification group.

### 1. Create a monitoring rule within the Azure Monitor Service and from the drop down select 'Create Rule'

<figure><img src=".gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

### 2. Create the alert rule with the scope details provided

<figure><img src=".gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### 3. Click 'Next' or 'Condition' and Select 'Custom Log Search' from Signal Name

<figure><img src=".gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

### 4. Copy and paste the followng query provided below and select 'Continue Editting Alert'.&#x20;

```kusto
AzureActivity
| where OperationNameValue contains "MICROSOFT.NETWORK/NETWORKWATCHERS/DELETE"
```

<figure><img src=".gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

### 5. Set the following parameters for the rule.

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### 7. Create an Action Group (Notification Group) for alert notification



<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### 8. Fill in the following options highlighted and then hit 'Notifications'



<figure><img src=".gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

### 9. Fill in the appropriate information and ensure to use your own email.&#x20;

<figure><img src=".gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

### 10. Review and Create the Alert Rule

<figure><img src=".gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### 11. Once Created you should see something similar to this.

<figure><img src=".gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

### 12. Select 'Details and fill out the information as shown.

<figure><img src=".gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

### 13. In order to map controls and keep control inventory add the tag below.

<figure><img src=".gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### 14. Verify the configuration of the rule and create it.

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

### 15. Trigger the rule by deleting the associated Network Watcher in the 'Sec-Lab' resource group.



<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

### 16. Confirm deletion as a side pane will appear.

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### 17. An alert will trigger within the Azure Monitor Dashboard

{% hint style="warning" %}
The rule can take up to 30-45 minutes to fully trigger.&#x20;
{% endhint %}

<figure><img src=".gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

### 18. Click on the alert to review it

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

### 19. An email will be sent to the address designated and will look like this.

<figure><img src=".gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
