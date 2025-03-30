# Sigma Rule Structure

## Overview

The following section gives you overview of Sigma. What Sigma is and what it specifically does.&#x20;

### What is Sigma

Sigma is the YAML-based generic signature format for writing detection rules for logs.\
Think of it like the "Sigma = YARA for logs".

* Created to be platform-agnostic.
* Translates into SIEM-specific queries (like Splunk SPL, KQL, Elastic DSL).
* Makes detection-as-code portable, version-controlled, and scalable.

### Sigma Rule Structure

```yaml
title: Suspicious PowerShell EncodedCommand
id: abc12345-6789-def0-1234-56789abcdef0
status: experimental
description: Detects use of EncodedCommand in PowerShell
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    CommandLine|contains: 'EncodedCommand'
  condition: selection
fields:
  - CommandLine
  - ParentImage
falsepositives:
  - Legitimate administrative scripts
level: medium
tags:
  - attack.execution
  - attack.t1059.001
```

### Key Sections

| Section          | Description                                                                     |
| ---------------- | ------------------------------------------------------------------------------- |
| `title`          | Human-friendly name of the rule                                                 |
| `id`             | Unique rule ID (UUID)                                                           |
| `status`         | `stable`, `experimental`, `deprecated`                                          |
| `logsource`      | Where the rule applies (e.g., Windows, Linux, category like `process_creation`) |
| `detection`      | The detection logic                                                             |
| `fields`         | Fields to show in alert                                                         |
| `falsepositives` | Known benign triggers                                                           |
| `level`          | Severity (`low`, `medium`, `high`, `critical`)                                  |
| `tags`           | MITRE ATT\&CK mappings (other other key tags based on your organization)        |

### Sigma Documentation

{% embed url="https://sigmahq.io/docs/basics/rules.html" %}

### Rules Repository

{% embed url="https://github.com/SigmaHQ/sigma" %}
