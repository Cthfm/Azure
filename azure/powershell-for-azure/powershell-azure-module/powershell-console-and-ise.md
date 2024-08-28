# Powershell Console & ISE

## **Overview:**&#x20;

The following section goes over the Powershell Console and introduction to the Integrated Scripting Environment (ISE).

### **PowerShell Console vs. Integrated Scripting Environment (ISE)**

**PowerShell Console:**

* A command-line interface where you can run PowerShell commands and scripts interactively.
* Best for quick tasks and one-off commands.
* Limited in terms of script editing and debugging capabilities.

### **Integrated Scripting Environment (ISE):**

* A graphical host application for PowerShell that provides an environment for writing, running, and debugging scripts.
* Features include syntax highlighting, multiline editing, and a script pane for creating and testing scripts.
* Ideal for writing, testing, and debugging longer scripts.

#### **How to Open:**

* **PowerShell Console:**
  * Windows: Search for "PowerShell" in the Start menu.
  * macOS/Linux: Open your terminal and type `pwsh`.
* **PowerShell ISE (Windows only):**
  * Search for "Windows PowerShell ISE" in the Start menu.

### **Configuring the PowerShell Environment**

**Changing the Execution Policy:**

* PowerShell’s execution policy determines the conditions under which PowerShell loads configuration files and runs scripts.
*   To check the current execution policy:

    ```powershell
    Get-ExecutionPolicy
    ```
*   To set the execution policy to allow running scripts:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

    (This allows scripts downloaded from the internet to run if they are signed by a trusted publisher.)

**Customizing the Console:**

* You can customize the appearance and behavior of the PowerShell console.
* To change properties such as font, colors, and layout:
  * Right-click the title bar of the PowerShell console window.
  * Select "Properties" and adjust settings as desired.

**Using Aliases:**

* Aliases are shortcuts for cmdlets and can make your work faster.
*   To list all aliases:

    ```powershell
    Get-Alias
    ```
*   To create a new alias:

    ```powershell
    Set-Alias -Name ll -Value Get-ChildItem
    ```

**Understanding Profiles**

**What is a PowerShell Profile?**

* A PowerShell profile is a script that runs when PowerShell starts. It can be used to customize your environment.
* There are different types of profiles, including user-specific and host-specific profiles.

**Profile Locations:**

*   To view all profile paths:

    ```powershell
    $PROFILE | Format-List -Property *
    ```

**Creating and Editing a Profile:**

*   To create a profile if it doesn’t exist:

    ```powershell
    if (!(Test-Path -Path $PROFILE)) {
        New-Item -Type File -Path $PROFILE -Force
    }
    ```
*   To open and edit your profile:

    ```powershell
    notepad $PROFILE
    ```
*   Add customizations, such as aliases or functions, to your profile. For example:

    ```powershell
    # Add an alias
    Set-Alias -Name ll -Value Get-ChildItem

    # Add a custom function
    function Show-DateTime {
        Get-Date
    }
    ```
