# adaudit
This PowerShell script is designed to conduct a comprehensive audit of Microsoft Active Directory, focusing on identifying common security vulnerabilities and weaknesses. Its execution facilitates the pinpointing of critical areas that require reinforcement, thereby fortifying your infrastructure against prevalent tactics used in lateral movement or privilege escalation attacks targeting Active Directory.
```
_____ ____     _____       _ _ _
|  _  |    \   |  _  |_ _ _| |_| |_
|     |  |  |  |     | | | . | |  _|
|__|__|____/   |__|__|___|___|_|_|
                 by vrushchitalia
```

If you have any decent powershell one liners that could be used in the script please let me know. I'm trying to keep this script as a single file with no requirements on external tools (other than ntdsutil and cmd.exe)

Run directly on a DC using a DA. If you don't trust the code I suggest reading it first and you'll see it's all harmless! (But shouldn't you be doing that anyway with code you download off the net and then run as DA??)

## What this does
 

- Device Information 

> Provides basic information about the computer, like its name, domain, user, Windows version, and IP addresses. 

 

-Domain Audit 

> Checks when the last Windows Update was installed on each domain controller and other update-related details. 

> Collects various details about domain controllers, like their OS versions and roles. 

> Checks the time source settings for each domain controller. 

> Lists members of important security groups. 

> Checks how many machines a regular user can add to the domain. 

> Reviews the security settings for domain controllers. 

> Checks if an older, less secure file-sharing protocol (SMB1) is enabled. 

> Reports the security level settings of the domain and forest. 

> Finds domain controllers not managed by Domain Admins. 

> Checks how domain controllers replicate data (using FRS or DFSR). 

> Checks if the Active Directory Recycle Bin is enabled. 

> Checks the status of critical services on domain controllers. 

> Lists Read-Only Domain Controllers (RODCs). 

- Domain Trust Audit 

> Reviews trust relationships between different domains. 

- User Accounts Audit 

> Finds user accounts that haven’t been used in 180 days. 

> Lists user accounts that are disabled. 

> Lists user accounts that are locked out. 

> Checks the status and security of the Administrator account. 

> Checks for vulnerabilities related to NULL sessions. 

> Lists accounts in important security groups with last logondate. 

> Lists accounts in the Protected Users group. 

- Replication Summary between DC’s 

> This will generate a replication summary and save it to a text file in the specified directory. 
 
- All GPO Names with Count 

> This will gather GPO names and count, save them to a text file in the specified directory. 

- AD Groups with Count 

> This will gather Group names and count, save them to a text file in the specified directory. 

- Host Based Firewall Details for DC’s 

> This provides an efficient way to gather and document the firewall profile settings for all domain controllers in an Active Directory environment. 

- Inactive Computers 

> This provides a list of computers which have been inactive for 180 days (about 6 months). 

- EmptyOUs 

> This searches for empty Organizational Units (OUs) within an Active Directory domain and saves them to a text file. 
 
- Password Information Audit 

> Lists accounts with passwords that never expire. 

> Finds accounts where passwords haven’t been changed in 90 days. 

> Reviews the domain’s password policy. 

## Runtime Args
The following switches can be used in combination
* -installdeps installs optionnal features (DSInternals)
* -hostdetails retrieves hostname and other useful audit info
* -domainaudit retrieves information about the AD such as functional level
* -trusts retrieves information about any doman trusts
* -accounts identifies account issues such as expired, disabled, etc...
* -passwordpolicy retrieves password policy information
* -ntds dumps the NTDS.dit file using ntdsutil
* -oldboxes identified outdated OSs like XP/2003 joined to the domain
* -gpo dumps the GPOs in XML and HTML for later analysis
* -ouperms checks generic OU permission issues
* -laps checks if LAPS is installed
* -authpolsilos checks for existence of authentication policies and silos
* -insecurednszone checks for insecure DNS zones
* -recentchanges checks for newly created users and groups (last 30 days)
* -adcs checks for ADCS vulnerabiltiies, ESC1,2,3,4 and 8.
* -acl checks for dangerous ACL permissions on Users, Groups and Computers. 
* -spn checks for high value kerberoastable accounts 
* -asrep checks for ASREPRoastable accounts
* -ldapsecurity checks for multiple LDAP issues
* -exclude allows you to exclude specific checks when using adaudit.ps1 -all -exclude ouperms,ntds,adcs"
* -select allows you to exclude specific checks when using adaudit.ps1 -all "gpo,ntds,acl"
* -all runs all checks, e.g. AdAudit.ps1 -all
