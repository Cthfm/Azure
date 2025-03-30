---
hidden: true
---

# Detections KQL

{% code overflow="wrap" %}
```kusto
StorageBlobLogs | where SasExpiryStatus startswith "Policy violated" | summarize count() by AccountName, SasExpiryStatus
```
{% endcode %}
