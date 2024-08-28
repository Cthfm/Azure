# Example Azure Cmdlets

## Overview:

The Azure PowerShell module includes a wide range of cmdlets to manage Azure resources. Here are some of the most commonly used cmdlets:

### **Resource Management:**

*   **Get-AzResourceGroup:** Retrieves information about resource groups.

    ```powershell
    Get-AzResourceGroup -Name "ResourceGroupName"
    ```
*   **New-AzResourceGroup:** Creates a new resource group.

    ```powershell
    New-AzResourceGroup -Name "ResourceGroupName" -Location "EastUS"
    ```
*   **Remove-AzResourceGroup:** Deletes a resource group.

    ```powershell
    Remove-AzResourceGroup -Name "ResourceGroupName"
    ```

### **Virtual Machines:**

*   **Get-AzVM:** Retrieves information about virtual machines.

    ```powershell
    Get-AzVM -ResourceGroupName "ResourceGroupName" -Name "VMName"
    ```
*   **New-AzVM:** Creates a new virtual machine.

    ```powershell
    New-AzVM -ResourceGroupName "ResourceGroupName" -Name "VMName" -Location "EastUS"
    ```
*   **Start-AzVM:** Starts a virtual machine.

    ```powershell
    Start-AzVM -ResourceGroupName "ResourceGroupName" -Name "VMName"
    ```
*   **Stop-AzVM:** Stops a virtual machine.

    ```powershell
    Stop-AzVM -ResourceGroupName "ResourceGroupName" -Name "VMName"
    ```

### **Storage Accounts:**

*   **Get-AzStorageAccount:** Retrieves information about storage accounts.

    ```powershell
    Get-AzStorageAccount -ResourceGroupName "ResourceGroupName"
    ```
*   **New-AzStorageAccount:** Creates a new storage account.

    ```powershell
    New-AzStorageAccount -ResourceGroupName "ResourceGroupName" -Name "StorageAccountName" -Location "EastUS" -SkuName "Standard_LRS"
    ```
*   **Remove-AzStorageAccount:** Deletes a storage account.

    ```powershell
    Remove-AzStorageAccount -ResourceGroupName "ResourceGroupName" -Name "StorageAccountName"
    ```

### **Networking:**

*   **Get-AzVirtualNetwork:** Retrieves information about virtual networks.

    ```powershell
    Get-AzVirtualNetwork -ResourceGroupName "ResourceGroupName" -Name "VNetName"
    ```
*   **New-AzVirtualNetwork:** Creates a new virtual network.

    ```powershell
    New-AzVirtualNetwork -ResourceGroupName "ResourceGroupName" -Name "VNetName" -AddressPrefix "10.0.0.0/16" -Location "EastUS"
    ```
*   **Remove-AzVirtualNetwork:** Deletes a virtual network.

    ```powershell
    Remove-AzVirtualNetwork -ResourceGroupName "ResourceGroupName" -Name "VNetName"
    ```



## Documentation Reference:

{% embed url="https://learn.microsoft.com/en-us/powershell/module/az.resources/get-azresourcegroup?view=azps-12.2.0" %}
