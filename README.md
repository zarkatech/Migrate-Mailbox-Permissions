# Migrate-Mailbox-Permissions
### PowerShell scripts to audit and migrate existing mailbox and delegate permissions from on-premises Exchange or between Exchange Online tenants.

STEP 1: AUDIT SOURCE MAILBOX PERMISSIONS

Run “Audit-MailboxPermissions.ps1” script in source environment to export mailbox access and delegate permissions so they can be re-applied in the target environment. Script offers the following preference variables which can be toggled or customized depending on scenario requirements:
* $UseImportFile = $true / $false
* $ImportFile = path and filename of CSV user list which includes “PrimarySmtpAddress”
* $UseFilterCriteria = $true / $false
* $FilterBatchName = short string to identify batch process, log, or export content.
* $FilterCriteria = literal filter syntax used to scope audit results
* $IncludeMailboxAccess = $true / $false 
* $IncludeSendAs = $true / $false
* $IncludeSendOnBehalf = $true / $false
* $IncludeFolderDelegates = $true / $false
* $IncludeCommonFoldersOnly - $true / $false
* $IncludeMailboxForwarding = $true / $false
* $DelegatesToSkip = service or built-In accounts which should not be audited
* $ExpandSecurityGroups = $true / $false
* $ExpandDistributionGroups = $true / $false

NOTE: Enumerating and auditing delegate permissions for every mailbox folder can take considerable time, so the preference variable $IncludeCommonFoldersOnly is set to $true by default and only audits delegate permissions for Top of Information Store, Inbox, and Calendar.

NOTE: Any on-premises security groups must be mail-enabled and synchronized to Exchange Online to re-apply mailbox permissions that don't already use distribution groups.

NOTE: Script can expand security or distributions group memberships to re-apply explicit user permissions but is not required or necessarily recommended.

STEP 2: APPLY TARGET MAILBOX PERMISSIONS

Run “Apply-MailboxPermissions.ps1” in target environment to re-apply mailbox access and delegate permissions collected from source environment. Script offers the following preference variables which can be toggled or customized based on scenario requirements:
* $BatchName = short string to identify batch process, log, or export content
* $IncludeMailboxAccess = $true / $false
* $IncludeSendAs = $true / $false
* $IncludeSendOnBehalf = $true / $false
* $IncludeFolderDelegates = $true / $false
* $IncludeMailboxForwarding = $true / $false
* $ApplyGroupPermissionsOnly = $true / $false
* $Debug = $true / $false

NOTE: Script offers detailed logging output and "WhatIf" debugging for dry-run analysis and error remediation by setting $Debug preference variable to $true.
