# Powershell Basics

## **Overview:**&#x20;

**The following goes over Powershell and the basics**&#x20;

### **What is PowerShell?**

PowerShell is a powerful task automation and configuration management framework from Microsoft. It includes a command-line shell and scripting language, designed to help  professionals control and automate the administration of Windows and applications.

**Key Features:**

* **Cmdlets:** Lightweight commands within PowerShell.
* **Pipelines:** Pass outputs from one cmdlet as inputs to another.
* **Scripting Language:** Create scripts to automate tasks.
* **Automation:** Simplify complex and repetitive tasks.
* **Object-Oriented:** Operates with objects, not just text.

### **Installing and Updating PowerShell**

**For Windows Users:**

1. **Check for Pre-Installed PowerShell:**
   * Most Windows versions come with Windows PowerShell pre-installed.
   * Open PowerShell: Search for "PowerShell" in the Start menu and launch it.
2. **Install PowerShell Core:**
   * Download the latest version from the [PowerShell GitHub releases page](https://github.com/PowerShell/PowerShell).
   * Follow the installation prompts.

#### **For macOS and Linux Users:**

1. **Download and Install:**
   * Visit the [PowerShell GitHub page](https://github.com/PowerShell/PowerShell).
   * Follow platform-specific installation instructions provided.

### **Updating PowerShell:**

* Download and run the latest installer from the PowerShell GitHub releases page to update.

### **Basic Command Syntax and Structure**

PowerShell commands, or cmdlets, use a Verb-Noun naming convention:

```mathematica
Verb-Noun -Parameter <Value>
```

**Examples:**

```arduino
Get-Process -Name "notepad"
```

**Common Verbs:**

* `Get`: Retrieve data
* `Set`: Change data
* `New`: Create a new resource
* `Remove`: Delete a resource
* `Start`: Begin an operation

### **Practical Examples to Get Started**&#x20;

**Exercise 1: Open PowerShell**

* **Windows:** Search for "PowerShell" in the Start menu and open it.
* **macOS/Linux:** Open your terminal and type `pwsh` to start PowerShell Core.

**Exercise 2: Run Basic Commands**

*   **List all running processes:**

    ```powershell
    Get-Process
    ```
*   **Get help for a cmdlet:**

    ```powershell
    Get-Help Get-Process
    ```
*   **Retrieve the current date and time:**

    ```powershell
    Get-Date
    ```

**Exercise 3: Explore PowerShell Help**

*   **Update the help system:**

    ```powershell
    Update-Help
    ```
*   **Get detailed help for a cmdlet:**

    ```powershell
    Get-Help Get-Process -Detailed
    ```

**Exercise 4: Check Parameters of a Given Command**

```powershell
Get-Help Get-Process -Parameter *
```
