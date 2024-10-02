# Initiative Definition

The structure of an Azure Policy **initiative definition** allows you to group multiple related policy definitions into a single entity, making it easier to manage and apply policies to your resources. Here's a detailed breakdown of the key elements involved in creating and managing a policy initiative definition:

#### 1. **Display Name and Description**

* **Display Name:** A human-readable name that identifies the initiative in the Azure portal.
* **Description:** A brief explanation of the initiative’s purpose.

#### 2. **Metadata**

* The metadata field provides additional information about the initiative. Common properties include:
  * **Version:** Tracks the version of the initiative definition.
  * **Category:** Specifies where the initiative is categorized within the Azure portal (e.g., Security, Networking, etc.).
  * **Preview:** Boolean value indicating if the initiative is in preview.
  * **Deprecated:** Boolean value indicating if the initiative is deprecated.

#### 3. **Version (Preview)**

* Initiatives can have multiple versions (like policies). Versioning allows you to track and use different iterations of an initiative and its underlying policies.
  * **Major Version:** Indicates significant changes that may affect the initiative's behavior.
  * **Minor Version:** Represents smaller changes like additional parameters or logic adjustments.
  * **Patch Version:** Covers bug fixes, text changes, or emergency security patches.

#### 4. **Parameters**

* Parameters in initiatives allow you to customize the policies within the initiative when applying them to different scopes. They help reduce the need for duplicating policy definitions.
* Properties include:
  * **Name:** The name of the parameter.
  * **Type:** The type of data expected (e.g., string, array, object, boolean, integer, etc.).
  * **Metadata:** Contains sub-properties like `description` and `displayName` for portal display.
  * **defaultValue:** A default value if none is specified.
  * **allowedValues:** A list of acceptable values for the parameter during assignment.

**Example:**

```json
"parameters": {
    "init_allowedLocations": {
        "type": "array",
        "metadata": {
            "description": "The list of allowed locations for resources.",
            "displayName": "Allowed locations",
            "strongType": "location"
        },
        "defaultValue": ["westus2"],
        "allowedValues": [
            "eastus2",
            "westus2",
            "westus"
        ]
    }
}
```

#### 5. **Policy Definitions**

* The `policyDefinitions` section defines which policies are part of the initiative. Each policy can receive parameters defined at the initiative level.
* Properties include:
  * **policyDefinitionId:** The full path to the policy definition (custom or built-in).
  * **policyDefinitionReferenceId:** A short identifier for the policy within the initiative.
  * **Parameters:** (Optional) The parameters passed to the individual policy definition.
  * **definitionVersion:** (Optional) The version of the policy definition being referenced.
  * **groupNames:** (Optional) Allows grouping policies for easier management.

**Example:**

```json
"policyDefinitions": [
    {
        "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/0ec8fc28-d5b7-4603-8fec-39044f00a92b",
        "policyDefinitionReferenceId": "allowedLocationsSQL",
        "parameters": {
            "sql_locations": {
                "value": "[parameters('init_allowedLocations')]"
            }
        }
    },
    {
        "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/aa09bd0f-aa5f-4343-b6ab-a33a6a6304f3",
        "policyDefinitionReferenceId": "allowedLocationsVMs",
        "parameters": {
            "vm_locations": {
                "value": "[parameters('init_allowedLocations')]"
            }
        }
    }
]
```

#### 6. **Policy Groups**

* Policy groups allow you to categorize policies within an initiative, which is particularly useful for regulatory compliance. Grouping helps organize related policies into a logical structure, such as by security controls or compliance domains.

**Example:**

```json
"policyDefinitionGroups": [
    {
        "name": "NIST_SP_800-53_R4_AC-1",
        "additionalMetadataId": "/providers/Microsoft.PolicyInsights/policyMetadata/NIST_SP_800-53_R4_AC-1"
    }
]
```

#### **Putting It All Together: Example of Initiative Definition**

Here’s a sample JSON that groups tagging policies using initiative parameters:

```json
code{
  "properties": {
    "displayName": "Billing Tags Policy",
    "policyType": "Custom",
    "description": "Specify cost Center tag and product name tag",
    "version": "1.0.0",
    "metadata": {
      "version": "1.0.0",
      "category": "Tags"
    },
    "parameters": {
      "costCenterValue": {
        "type": "String",
        "metadata": {
          "description": "required value for Cost Center tag"
        },
        "defaultValue": "DefaultCostCenter"
      },
      "productNameValue": {
        "type": "String",
        "metadata": {
          "description": "required value for product Name tag"
        },
        "defaultValue": "DefaultProduct"
      }
    },
    "policyDefinitions": [
      {
        "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
        "parameters": {
          "tagName": {
            "value": "costCenter"
          },
          "tagValue": {
            "value": "[parameters('costCenterValue')]"
          }
        }
      },
      {
        "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
        "parameters": {
          "tagName": {
            "value": "productName"
          },
          "tagValue": {
            "value": "[parameters('productNameValue')]"
          }
        }
      }
    ]
  }
}
```

#### **Key Takeaways**

* **Initiatives** simplify policy management by grouping multiple policy definitions into a single entity.
* **Parameters** are critical in ensuring reusability and flexibility.
* **Versioning** allows you to manage different iterations of policies within initiatives.
* **Policy Groups** help structure the policies within the initiative, especially useful for regulatory compliance.
