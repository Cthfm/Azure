# Scope Azure Policy

## **Scope in Azure Policy**

**Scope in Azure Policy** defines which resources are evaluated for compliance, based on Azure Resource Manager’s scope model.

### **Definition Location**

When creating a policy definition, its location—either a **management group** or **subscription**—determines which resources it can target.

* **Subscription**: The policy applies to resources within that specific subscription.
* **Management Group**: The policy can apply to all resources in child management groups and subscriptions under it. This is ideal for managing multiple subscriptions.

### **Assignment Scope**

A policy assignment has properties that define what resources to evaluate:

* **Inclusion**: The assignment’s `scope` specifies which resources are included in the evaluation.
* **Exclusion**: The `notScopes` property lists resources that shouldn’t be evaluated for compliance.

### **Exemptions**

Exemptions allow specific resources to temporarily bypass compliance checks (e.g., waivers or mitigation). These resources are still tracked but not evaluated for compliance. Exemptions can expire using the `expiresOn` property.

#### **Scope Comparison**

| Resources            | Inclusion | Exclusion (notScopes) | Exemption |
| -------------------- | --------- | --------------------- | --------- |
| Evaluated            | ✔         | -                     | -         |
| Excluded             | -         | ✔                     | -         |
| Temporarily Exempted | -         | -                     | ✔         |

### **When to Use Exclusion or Exemption**

* **Exclusions**: For permanently excluding resources from evaluation (e.g., test environments).
* **Exemptions**: For temporarily excluding resources (e.g., waivers) while still tracking them.
