# Azure Remediation Task Structure

Azure Policy remediation tasks help bring non-compliant resources into compliance based on policy definitions and assignments. Resources not compliant with a `deployIfNotExists` or `modify` definition can be remediated by deploying templates or making modifications, using the identity specified in the policy assignment.

New or updated resources that match a `deployIfNotExists` or `modify` assignment are automatically remediated. Remediation tasks are automatically deleted 60 days after the last modification.

Remediation tasks are created using JSON, containing elements such as:

* **Policy Assignment ID**: Full path of the policy or initiative.
* **Policy Definition ID**: Specifies the policy definition if the assignment is part of an initiative.
* **Resource Count & Parallel Deployments**: Defines how many resources to remediate and how many can be handled simultaneously.
* **Failure Threshold**: Optionally stops remediation if failures exceed a specified percentage.
* **Remediation Filters**: Optional, such as filtering by region.
* **Resource Discovery Mode**: Identifies non-compliant resources, with options like `ExistingNonCompliant` or `ReEvaluateCompliance`.
* **Provisioning State & Deployment Summary**: Provides status and deployment details for the task.

For example, the following JSON represents a remediation task:

```json
{
  "id": "/subscriptions/{subId}/resourceGroups/{resourceGroupName}/providers/Microsoft.PolicyInsights/remediations/remediateNotCompliant",
  "apiVersion": "2021-10-01",
  "name": "remediateNotCompliant",
  "type": "Microsoft.PolicyInsights/remediations",
  "properties": {
    "policyAssignmentId": "/subscriptions/{subID}/providers/Microsoft.Authorization/policyAssignments/resourceShouldBeCompliantInit",
    "policyDefinitionReferenceId": "requiredTags",
    "resourceCount": 42,
    "parallelDeployments": 6,
    "failureThreshold": { "percentage": 0.1 }
  }
}
```
