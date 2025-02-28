# User

## **Overview:**

The following are specific steps and commands that can be used to contain a compromised user.&#x20;

### **1. Revoke Active Sessions & Access Tokens**

Even after a password reset, active tokens may persist. **Revoke all sessions** to log out the user.

**Option 1: Microsoft Entra ID Portal**

1. **Go to Microsoft Entra ID > Users**.
2. Select the **compromised user**.
3. Click **Revoke sessions** (this logs them out immediately).

**Option 2: PowerShell**

```powershell
Revoke-AzureADUserAllRefreshToken -ObjectId "<UserObjectID>" Revoke-MgUserSignInSession -UserId $User.Id
```

### 2. Conduct a User Password Reset

Force the user to log out and reset the password.

**Option 1: Manually Reset Password in Entra ID**

1. Go to **Microsoft Entra ID** (Azure Portal).
2. Navigate to **Users > Select Compromised User**.
3. Click **Reset Password** and generate a strong password.
4. Require **password reset on next login**.
5. Save changes.

**Option 2: Use PowerShell**

```powershell
$UserUPN = "compromised_user@domain.com"
$NewPassword = "NewSecurePassword!123"
Set-MsolUserPassword -UserPrincipalName $UserUPN -NewPassword $NewPassword -Force
```

### **Step 4: Disable the User (Optional)**

If necessary, **disable the user account** to prevent further access.

**Option 1: Microsoft Entra ID Portal**

1. Navigate to **Microsoft Entra ID > Users**.
2. Select the compromised user.
3. Click **Block sign-in**.

**Option 2: PowerShell**

```powershell
Set-AzureADUser -ObjectId "<UserObjectID>" -AccountEnabled $false
```
