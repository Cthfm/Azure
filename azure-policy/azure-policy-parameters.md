# Azure Policy Parameters

Parameters simplify policy management by reducing the number of policy definitions. Think of parameters like form fields (name, address, etc.) where the values change based on the user. Similarly, by using parameters in policy definitions, you can reuse the same policy for different scenarios by simply changing the values.

### Adding or Removing Parameters:

* **Adding**: When adding a parameter to an existing assigned policy, include the `defaultValue` to avoid breaking the current assignments.
* **Removing**: Parameters cannot be removed if they are part of an existing assignment, as it may break references. Instead, you can create a new policy definition without the parameter.

### Key Parameter Properties:

* **name**: Parameter's name used in the policy rule.
* **type**: Defines the data type (string, array, object, etc.).
* **metadata**: Contains `description`, `displayName`, and optional `strongType`, which helps provide a context-aware list in the portal.
* **defaultValue**: Sets a value if none is provided during assignment.
* **allowedValues**: Lists acceptable values during assignment.
* **deprecated**: Marks a parameter as no longer in use in built-in definitions.

### Case Sensitivity:

Comparisons of parameter values during assignment are case-sensitive. However, evaluation may be case-insensitive based on the condition used.

#### Example:

A policy might limit resource locations. The parameter `allowedLocations` can define which locations are valid for deployment:

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "Allowed resource locations",
      "displayName": "Allowed locations",
      "strongType": "location"
    },
    "defaultValue": ["westus2"],
    "allowedValues": ["eastus2", "westus2", "westus"]
  }
}
```

### Using Parameter Values:

In a policy rule, reference parameters like this:

```json
{
  "field": "location",
  "in": "[parameters('allowedLocations')]"
}
```

### strongType:

This property provides a multiselect list in the portal and can be used for resource types (e.g., `Microsoft.Network/virtualNetworks/subnets`). Supported types include `location`, `resourceTypes`, `storageSkus`, and more.
