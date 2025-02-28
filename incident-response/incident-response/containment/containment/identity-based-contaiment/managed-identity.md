# Managed Identity

### Using the Azure Portal

1. **Identify the Resource or Identity:**
   * **System-Assigned Identity:**\
     Navigate to the resource (e.g., a virtual machine, App Service) that uses the identity. Open its **Identity** pane to view details. This is under security in some resources.
   * **User-Assigned Identity:**\
     Search for “Managed Identities” in the portal and select the specific identity resource.
2. **Review and Remove Role Assignments:**
   * Go to the resources or identity’s **Access Control (IAM)** section.
   * Filter the role assignments by the managed identity’s principal to see all its permissions.
   * For each suspicious or excessive role, click on the assignment and select **Remove** (or edit as needed) to revoke access.
3. **Disable or Isolate the Identity:**
   * **For System-Assigned Identities:**\
     If you need to disable the identity entirely, toggle off the managed identity option in the resource’s Identity settings. This will cause Azure to remove the identity’s credentials.
   * **For User-Assigned Identities:**\
     Detach the identity from all associated resources to prevent further usage. Once remediated, you may choose to recreate a new identity and reassign it.
4. **Monitor and Audit:**
   * After making changes, review Entra ID sign-in logs and activity logs to ensure that the identity’s actions have ceased and to further investigate any anomalies.

### Using PowerShell

1.  **Connect to Your Azure Account:**

    ```powershell
    Connect-AzAccount
    ```
2. **Identify the Managed Identity:**
   *   **User-Assigned Identity:**\
       Retrieve the identity details:

       ```powershell
       $identity = Get-AzUserAssignedIdentity -ResourceGroupName "YourResourceGroup" -Name "YourIdentityName"
       ```
   * **System-Assigned Identity:**\
     Since these are tied to a resource, you’ll work directly with the resource (e.g., a virtual machine).
3.  **Remove Role Assignments:**

    *   List and remove role assignments associated with the identity. For example:

        ```powershell
        Remove-AzRoleAssignment -ObjectId "PrincipalID" -Scope "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}" -RoleDefinitionName "Contributor"
        ```

        Adjust the scope and role as appropriate for your scenario.


4. **Verify and Monitor:**
   * After applying changes, check your logs (using either PowerShell commands or via the Azure Portal) to confirm that the identity is no longer performing actions, and that access has been successfully revoked.
