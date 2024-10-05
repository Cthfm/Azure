# Azure Policy Components

## **Key Components of Azure Policy**

Azure Policy is made up of several core components that help you define, assign, and enforce security standards within your environment. As a threat hunter, it’s crucial to understand how these components interact and how they can be tailored to your security needs.

### **1. Policy Basics - Policy Definition**

A **Policy Definition** is the core rule that specifies what is allowed or disallowed within your environment. This is where you define the conditions that a resource must meet to be considered compliant or non-compliant.

* **Example**: You can create a policy definition that requires **all virtual machines (VMs) to use managed disks**. If a VM is created without a managed disk, the policy will flag it as non-compliant.
* **Structure of a Policy Definition**:

1. **Display Name and Description**:
   * These identify the policy and provide context.
   * _Display Name_: Max 128 characters.
   * _Description_: Max 512 characters.
2. **Policy Type**:
   * There are three policy types:
     * **Builtin**: Provided by Microsoft.
     * **Custom**: Created by users.
     * **Static**: Regulatory Compliance policies based on Microsoft audits.
3. **Mode**:
   * **Resource Manager modes**:
     * `all`: Evaluates all resource types.
     * `indexed`: Evaluates only resource types that support tags and locations.
   * **Resource Provider modes**:
     * Different modes manage specific resource types, such as Kubernetes clusters, Key Vaults, Virtual Network Managers, and others, with varying levels of compliance and enforcement capabilities.
     * Example: `Microsoft.Kubernetes.Data` for managing Kubernetes components.
4. **Versioning** (Preview):
   * Policies can support versioning using a {Major}.{Minor}.{Patch} format, indicating the level of changes in the policy.
   * Different states, such as deprecated or preview, indicate the status of policy versions.
5. **Metadata**:
   * An optional field that tracks information about the policy definition.
   * Common properties include `version`, `category`, `preview`, and `deprecated`.
6. **Policy Rule**:
   * Core logic defined under `if-then` conditions.
   * Example: In the policy for "Allowed Locations," it checks if a resource’s location is within a list of allowed locations, and if not, applies a "deny" effect.
7. **Effect**:
   * The action to take when a resource is non-compliant, such as `deny`, `audit`, or `deployIfNotExists`.

**Example of a Policy Rule**:

```json
{
  "if": {
    "field": "Microsoft.Compute/virtualMachines/storageProfile.osDisk.managedDisk.id",
    "exists": "false"
  },
  "then": {
    "effect": "deny"
  }
}
```

### **2. Policy Assignment**

Once a policy is defined, it needs to be assigned to a **scope** where it can enforce or audit resources. The scope can be a **subscription**, **resource group**, or **management group**.

* **Example**: You can assign a policy that enforces **encryption** on all storage accounts within a specific subscription, ensuring that all storage resources are compliant with your security requirements.
* **Scope**: The range at which the policy will apply. This can be:
  * **Management Group**: Applies the policy across multiple subscriptions.
  * **Subscription**: Applies the policy across all resource groups and resources in a specific subscription.
  * **Resource Group**: Applies the policy to all resources within a specific resource group.
* **Exclusions**: You can exclude specific resources or resource groups from the policy assignment, allowing for flexibility in environments with different requirements.

### **3. Initiative Definition**

An **Initiative** is a collection of related policies grouped together to achieve a broader compliance goal. By grouping policies into initiatives, you can manage and apply multiple policies more efficiently.

* **Example**: You could create an initiative called **"Security Best Practices"**, which includes policies for:
  * Enforcing encryption on all storage accounts.
  * Applying Network Security Groups (NSGs) to all VMs.
  * Auditing public-facing resources.

Initiatives simplify management by allowing you to assign a set of policies with one action, rather than managing individual policies separately.

### **4. Policy Effects**

Every policy has an **Effect** that defines what happens when a resource does not comply with the policy. The effect is how the policy enforces or audits the rules.

**Common Effects**:

* **Deny**: Prevents a resource from being created if it doesn’t comply with the policy.
  * **Example**: A policy can deny the creation of a virtual machine that lacks disk encryption.
* **Audit**: Allows the resource to be created but logs the non-compliance, so you can review it later.
  * **Example**: A policy can audit all VMs that don’t have NSGs, logging these for further review by the threat hunting team.
* **Append**: Adds specific properties to a resource to make it compliant.
  * **Example**: Appends a required tag (like “costCenter”) to a resource that is missing it.
* **Modify**: Changes the resource configuration automatically to enforce compliance.
  * **Example**: Modifies a storage account’s configuration to enable encryption automatically if it wasn’t enabled during creation.
* **DeployIfNotExists**: Deploys a resource or configuration if it doesn’t exist.
  * **Example**: If a VM is created without a monitoring agent, Azure Policy can automatically deploy the agent to ensure compliance.

**Choosing the Right Effect**: As a threat hunter, you might use **Audit** or **Deny** for different scenarios. For instance, you could start with an **Audit** effect to see which resources are non-compliant, then switch to **Deny** once you’ve ensured that the policy won’t block legitimate resource creation.

### **5. Parameters**

Policies and initiatives can include **parameters** to make them more flexible and reusable. Parameters allow you to customize the policy when assigning it to different scopes.

* **Example**: You could create a policy that requires VMs to be located in a specific region. By using parameters, you can assign this policy to different resource groups and specify different allowed regions for each one.

## **How These Components Work Together**

Here’s how you can leverage these components as a threat hunter:

1. **Define a Policy**: You start by defining a policy to address a specific security concern (e.g., ensuring all VMs have encryption enabled).
2. **Assign the Policy**: You assign the policy to the appropriate scope (e.g., all VMs in a specific subscription).
3. **Monitor Compliance**: As resources are created and updated, Azure Policy continuously monitors compliance. Any non-compliant resources are flagged for review or automatically remediated.
4. **Use Initiatives**: For broader security objectives, you can create an initiative that combines multiple policies (e.g., encryption, MFA enforcement, NSG application) into a single package.
5. **Review Logs**: You use the compliance logs generated by Azure Policy to identify misconfigurations or vulnerabilities that need further investigation.

## **Real-World Example: Ensuring Network Security Groups (NSGs) on All VMs**

You are tasked with securing an Azure environment where multiple teams deploy virtual machines. A major risk is that some teams might create VMs without Network Security Groups (NSGs), leaving them vulnerable to unrestricted inbound and outbound traffic.

**Step-by-Step Approach:**

1. **Define the Policy**: Create a policy that requires every VM to have an NSG applied. If a VM is created without an NSG, the policy will either deny its creation or log it as non-compliant.
2. **Assign the Policy**: Apply this policy to all production resource groups.
3. **Monitor Compliance**: If any team deploys a VM without an NSG, Azure Policy will detect it. You can choose to audit these violations initially, then shift to denying the creation of non-compliant VMs once you’ve evaluated the policy’s impact.
4. **Automate Remediation**: Use the **Modify** effect to automatically attach a default NSG if a VM is created without one, ensuring that all VMs are protected without manual intervention.
