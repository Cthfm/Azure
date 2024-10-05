# Mailbox Auditing

## Overview:

Mailbox audit logging is enabled by default in all organizations. This automatically logs specific actions performed by mailbox owners, delegates, and admins. Admins can search these logs using the mailbox audit log.

Key benefits include:

* Auditing is automatically enabled for new mailboxes, requiring no manual setup.
* Default mailbox actions are audited without needing configuration.
* New mailbox actions are added automatically (with the correct license).
* A consistent auditing policy is applied across the organization.

To verify auditing is enabled, run the following PowerShell command:

```powershell
Get-OrganizationConfig | Format-List AuditDisabled
```

A value of `False` means auditing is enabled by default, overriding individual mailbox settings.

You can bypass audit logging for specific users with the following command:

```powershell
Set-MailboxAuditBypassAssociation -Identity <MailboxIdentity> -AuditByPassEnabled $true
```

Audit logs are retained for 90 days, but this can be adjusted using the `AuditLogAgeLimit` parameter.

Mailboxes affected by retention policies or holds have increased quotas for the Recoverable Items folder. However, default auditing has minimal impact on storage.

For a multi-geo environment, cross-geo mailbox auditing isn't supported.

To manage or restore mailbox actions, use PowerShell cmdlets, and to turn auditing off or on for the organization, use:

```powershell
Set-OrganizationConfig -AuditDisabled $true (or $false)
```

