# Understanding Cmdlets

## Overview:

The following section goes over what cmdlets are and common cmdlets utilized within Powershell.

### **Common Cmdlets**

**What are Cmdlets?**

* Cmdlets are lightweight commands used in the PowerShell environment. They follow a Verb-Noun naming pattern.

**Common Cmdlets:**

*   `Get-Help`: Provides help information for cmdlets.

    ```powershell
    Get-Help Get-Process
    ```
*   `Get-Command`: Lists all available cmdlets and functions.

    ```powershell
    Get-Command
    ```
*   `Get-Service`: Retrieves the status of services on a system.

    ```powershell
    Get-Service
    ```
*   `Get-Process`: Gets the processes that are running on a system.

    ```powershell
    Get-Process
    ```
*   `Set-Variable`: Sets the value of a variable.

    ```powershell
    Set-Variable -Name "testVar" -Value "Hello, PowerShell"
    ```
*   `Remove-Item`: Deletes files, directories, or registry keys.

    ```powershell
    Remove-Item -Path "C:\Temp\test.txt"
    ```

**Examples Using Cmdlets:**

*   Retrieve a list of all services:

    ```powershell
    Get-Service
    ```
*   Get detailed help for a cmdlet:

    ```powershell
    Get-Help Get-Process -Detailed
    ```
*   List all commands available in your PowerShell session:

    ```powershell
    Get-Command
    ```

### **Using the Pipeline**

**What is a Pipeline?**

* The pipeline (`|`) is a powerful feature in PowerShell that allows you to pass the output of one cmdlet as input to another cmdlet.

**Basic Pipeline Usage:**

*   Example:

    ```powershell
    Get-Process | Sort-Object -Property CPU
    ```

**Filtering Output:**

* Use `Where-Object` to filter objects based on property values.
*   Example:

    ```powershell
    Get-Process | Where-Object { $_.CPU -gt 100 }
    ```

**Selecting Properties:**

* Use `Select-Object` to select specific properties of objects.
*   Example:

    ```powershell
    Get-Process | Select-Object -Property Name, CPU
    ```

**Sorting Output:**

* Use `Sort-Object` to sort objects by property values.
*   Example:

    ```powershell
    Get-Process | Sort-Object -Property CPU -Descending
    ```

**Example: Using Multiple Cmdlets in a Pipeline**

```powershell
Get-Service | Where-Object { $_.Status -eq "Running" } | Sort-Object -Property DisplayName
```

### **Filtering and Formatting Output**

**Filtering Data:**

*   `Where-Object`: Filters objects based on a specified condition.

    ```powershell
    Get-Process | Where-Object { $_.CPU -gt 100 }
    ```

**Formatting Data:**

*   `Format-Table`: Formats output as a table.

    ```powershell
    Get-Process | Format-Table -Property Name, CPU -AutoSize
    ```
*   `Format-List`: Formats output as a list.

    ```powershell
    Get-Process | Format-List -Property Name, CPU
    ```

**Examples:**

*   List all running processes using a table format:

    ```powershell
    Get-Process | Format-Table -Property Name, CPU -AutoSize
    ```
*   List all services that are running, sorted by display name:

    ```powershell
    Get-Service | Where-Object { $_.Status -eq "Running" } | Sort-Object -Property DisplayName
    ```

### **Practical Exercises**

**Exercise 1: Using Basic Cmdlets**

*   Retrieve a list of all processes running on your system:

    ```powershell
    Get-Process
    ```
*   Retrieve detailed help for the `Get-Service` cmdlet:

    ```powershell
    Get-Help Get-Service -Detailed
    ```

**Exercise 2: Using the Pipeline**

*   List all running processes and sort them by CPU usage:

    ```powershell
    Get-Process | Sort-Object -Property CPU
    ```
*   Filter the processes to show only those using more than 100 units of CPU:

    ```powershell
    Get-Process | Where-Object { $_.CPU -gt 100 }
    ```

**Exercise 3: Filtering and Formatting Output**

*   List all running services and format the output as a table:

    ```powershell
    Get-Service | Where-Object { $_.Status -eq "Running" } | Format-Table -Property DisplayName, Status -AutoSize
    ```

**Exercise 4: Combining Cmdlets in a Pipeline**

*   Combine `Get-Service`, `Where-Object`, and `Format-Table` to list all running services, sorted by their display names:

    ```powershell
    Get-Service | Where-Object { $_.Status -eq "Running" } | Sort-Object -Property DisplayName | Format-Table -Property DisplayName, Status -AutoSize
    ```

