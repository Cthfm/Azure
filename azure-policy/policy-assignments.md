# Policy Assignments

## Azure Policy Assignments

Azure Policy assignments allow you to apply policies to a specific scope, such as subscriptions, resource groups, or individual resources, while managing compliance across those resources. Here's an overview of key components within an Azure Policy assignment:

### 1. **Scope**

* The scope defines which resources the policy applies to. You can assign policies at different levels, including management groups, subscriptions, resource groups, and individual resources.

### 2. **Policy Definition ID and Version**

* This is the unique identifier for a specific policy or initiative (a collection of policies). The policy definition can either point to a built-in policy or a custom one. You can pin the version to control which updates are auto-ingested (e.g., `1.*.*` for major version).

### 3. **Display Name and Description**

* These fields help identify the policy assignment. `displayName` (max 128 characters) provides a human-readable name, and `description` (max 512 characters) gives context on the policy’s purpose.

### 4. **Metadata**

* Metadata stores additional information about the policy assignment. Common metadata properties include `assignedBy`, `createdBy`, `createdOn`, and more. Organizations can also store custom metadata properties.

### 5. **Resource Selectors**

* Resource selectors enable fine-grained control over which resources are evaluated by the policy based on factors like resource location or type. You can use these selectors for gradual rollout or to narrow down compliance checks.

### 6. **Overrides**

* Overrides allow you to change the effect of a policy without modifying the original definition. This is useful for initiatives containing multiple policies, where different effects might be needed for certain policy definitions.

### 7. **Enforcement Mode**

* `enforcementMode` defines whether the policy is enforced or just evaluated. For instance, setting `DoNotEnforce` allows you to evaluate a policy without triggering its effects, enabling "What If" testing.

### 8. **Excluded Scopes**

* This property specifies resources or resource containers (such as resource groups) that should be excluded from the policy assignment, even if they are within the main scope.

### 9. **Non-compliance Messages**

* Non-compliance messages provide custom feedback when a resource does not meet policy requirements. These messages can be defined per policy within an initiative or at the assignment level.

### 10. **Parameters**

* Parameters enable reuse of policy definitions by allowing input values to be customized at assignment time. For example, a policy could enforce a naming convention using a customizable prefix and suffix for resource names.

### 11. **Identity**

* Policies that use `deployIfNotExists` or `modify` effects need an identity to remediate non-compliant resources. You can assign either a system-assigned or user-assigned managed identity.

**Example JSON for a Policy Assignment:**

```json
{
  "properties": {
    "displayName": "Enforce resource naming rules",
    "description": "Force resource names to begin with DeptA and end with -LC",
    "definitionVersion": "1.*.*",
    "metadata": {
      "assignedBy": "Cloud Center of Excellence"
    },
    "enforcementMode": "DoNotEnforce",
    "notScopes": [],
    "policyDefinitionId": "/subscriptions/{mySubscriptionID}/providers/Microsoft.Authorization/policyDefinitions/ResourceNaming",
    "nonComplianceMessages": [
      {
        "message": "Resource names must start with 'DeptA' and end with '-LC'."
      }
    ],
    "parameters": {
      "prefix": {
        "value": "DeptA"
      },
      "suffix": {
        "value": "-LC"
      }
    },
    "identity": {
      "type": "SystemAssigned"
    },
    "resourceSelectors": [],
    "overrides": []
  }
}
```

