# Azure Policy Rules

## Azure Policy Rules

Azure Policy rules are structured into **if** and **then** blocks.

* **If block**: This contains one or more conditions that determine when the policy is applied. Logical operators can be used to refine these conditions.
* **Then block**: This defines the effect that occurs when the conditions in the if block are met.

Example Policy Rule Structure:

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | modify | deployIfNotExists | append | etc."
  }
}
```

### Logical Operators

* **not**: Inverts the condition.
* **allOf**: Requires all conditions to be true (like a logical AND).
* **anyOf**: Requires at least one condition to be true (like a logical OR).

Example of nested logical operators:

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
}
```

### Conditions

Conditions define criteria for evaluating values. Examples include:

* **equals**: "stringValue"
* **like**: "stringValue" (supports wildcards)
* **greaterOrEquals**: integerValue or dateValue

### Field Expressions

Conditions can reference specific fields like:

* **name**: The resource's name.
* **location**: The resource’s region.
* **id**: The resource's unique ID.

Example condition using a field:

```json
{
  "field": "type",
  "equals": "Microsoft.Network/publicIPAddresses"
}
```

### Count and Value Expressions

You can use count expressions to evaluate arrays, like checking if a field has a specific number of values.

Example:

```json
{
  "count": {
    "field": "Microsoft.Network/networkSecurityGroups/securityRules[*]"
  },
  "equals": 0
}
```

### Policy Functions

Functions can introduce complex logic, such as:

* **utcNow()**: Gets the current date and time.
* **ipRangeContains()**: Checks if an IP range contains a specific address.

Example using `ipRangeContains`:

```json
{
  "if": {
    "count": {
      "field": "Microsoft.Network/virtualNetworks/addressSpace.addressPrefixes[*]",
      "where": {
        "value": "[ipRangeContains('10.0.0.0/24', current('Microsoft.Network/virtualNetworks/addressSpace.addressPrefixes[*]'))]",
        "equals": false
      }
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

####
