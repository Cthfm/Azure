# Understanding Powershell Variables

## **Overview:**

The following section explains variables and how they are utilized within PowerShell

### **Declaring and Using Variables**

### **What is a Variable?**

* A variable is a storage location identified by a name, used to hold data that can be referenced and manipulated in a script.

### **Declaring Variables:**

* In PowerShell, variables are declared using the `$` symbol followed by the variable name.
*   Example:

    ```powershell
    $myVariable = "Hello, World!"
    ```

### **Using Variables:**

* Once declared, variables can be used in commands and scripts.
*   Example:

    ```powershell
    $greeting = "Hello, World!"
    Write-Output $greeting
    ```

### **Modifying Variables:**

* Variables can be updated or modified.
*   Example:

    ```powershell
    $counter = 10
    $counter = $counter + 1
    Write-Output $counter
    ```

### **Common Data Types**

**Strings:**

* Text data enclosed in quotes.
*   Example:

    ```powershell
    $name = "John Doe"
    ```

**Integers:**

* Whole numbers.
*   Example:

    ```powershell
    $age = 30
    ```

**Arrays:**

* Ordered collections of values.
*   Example:

    ```powershell
    $colors = @("Red", "Green", "Blue")
    ```

**Hashtables:**

* Collections of key-value pairs.
*   Example:

    ```powershell
    $person = @{
        Name = "John Doe"
        Age = 30
        Occupation = "Developer"
    }
    ```

**Booleans:**

* True/False values.
*   Example:

    ```powershell
    powershellCopy code$isAdmin = $true
    ```

**Examples of Using Different Data Types:**

```powershell
# String
$greeting = "Hello, PowerShell!"

# Integer
$year = 2024

# Array
$fruits = @("Apple", "Banana", "Cherry")

# Hashtable
$book = @{
    Title = "PowerShell Guide"
    Author = "Jane Smith"
    Year = 2024
}

# Boolean
$isComplete = $false
```

### **Variable Scopes**

**Understanding Scope:**

* Scope determines the visibility and lifetime of a variable.
* Common scopes in PowerShell:
  * **Global:** Visible in all scripts and scopes.
  * **Local:** Visible only within the current script or function.
  * **Script:** Visible in the current script file.
  * **Private:** Visible only within the current block or function.

**Example of Variable Scopes:**

```powershell
# Global Scope
$Global:globalVar = "I am global"

# Script Scope
$Script:scriptVar = "I am script"

# Local Scope (default)
$localVar = "I am local"

# Private Scope
function Test-Scope {
    $Private:privateVar = "I am private"
    Write-Output $privateVar
}

Test-Scope
Write-Output $privateVar  # This will not work outside the function
```

**Using Scopes Effectively:**

* Define variables in the appropriate scope based on their intended use.
* Be mindful of scope to avoid conflicts and unexpected behaviors.
