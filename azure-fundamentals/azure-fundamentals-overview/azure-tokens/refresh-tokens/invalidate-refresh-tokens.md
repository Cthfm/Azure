# Invalidate Refresh Tokens

## Invoke-MgBetaInvalidateAllUserRefreshToken&#x20;

The Invoke-MgBetaInvalidateAllUserRefreshToken cmdlet is used to invalidate all refresh tokens issued to a user, forcing them to re-authenticate for all previously consented applications. This operation is typically performed when a user has lost a device, to prevent unauthorized access to organizational data. The cmdlet resets the refreshTokensValidFromDateTime property to the current date-time, invalidating session cookies and all refresh tokens.

### Key usage:

* You need to provide the UserId to identify the user.
* Common scenarios include lost or stolen devices.
* Applications attempting to use an invalidated refresh token will receive an error, requiring the user to sign in again.

Example usage:

```powershell
Invoke-MgBetaInvalidateAllUserRefreshToken -UserId $userId
```

This cmdlet requires permissions such as User.RevokeSessions.All for delegated work/school accounts. Optional parameters include headers, confirmation prompts, and the ability to preview changes using -WhatIf.

### Cmdlet Reference

{% embed url="https://learn.microsoft.com/en-us/powershell/module/microsoft.graph.beta.users.actions/invoke-mgbetainvalidatealluserrefreshtoken?view=graph-powershell-beta&preserve-view=true" %}
