# AD Manual Enumeration

## Operators to use with Filter

- `-eq`	Equal to
- `-le`	Less than or equal to
- `-ge`	Greater than or equal to
- `-ne`	Not equal to
- `-lt`	Less than
- `-gt`	Greater than
- `-approx`	Approximately equal to
- `-bor`	Bitwise OR
- `-band`	Bitwise AND
- `-recursivematch`	Recursive match
- `-like`	Like
- `-notlike`	Not like
- `-and`	Boolean AND
- `-or`	Boolean OR
- `-not`	Boolean NOT
- Example
  ```
  Get-ADUser -Filter "name -eq 'jane doe'"
  Get-ADUser -Filter {name -eq 'jane doe'}
  Get-ADUser -Filter'name -eq "jane doe"'
  ```

## Example of useful queries

- `Get-ADGroup -Identity "<GROUP NAME" -Properties *` Get information about an AD group
- `whoami /priv` View a user's current rights 
- ` Get-WindowsCapability -Name RSAT* -Online \| Select-Object -Property Name, State` Check if RSAT tools are installed
- `Get-WindowsCapability -Name RSAT* -Online \| Add-WindowsCapability –Online` Install all RSAT tools
- `runas /netonly /user:htb.local\jackie.may powershell`  Run a utility as another user 
- `Get-ADObject -LDAPFilter '(objectClass=group)' \| select cn` LDAP query to return all AD groups
- `Get-ADUser -LDAPFilter '(userAccountControl:1.2.840.113556.1.4.803:=2)' \| select name` List disabled users 
- `Get-ADUser -SearchBase "OU=Employees,DC=INLANEFREIGHT,DC=LOCAL" -Filter *).count` Count all users in an OU
- `get-ciminstance win32_product \| fl` Query for installed software
- `get-ciminstance win32_product -Filter "NOT Vendor like '%Microsoft%'" | fl` Query for software that are not microsoft
- `Get-ADComputer  -Filter "DNSHostName -like 'SQL*'"` Get hostnames with the word "SQL" in their hostname
- `Get-ADGroup -Filter "adminCount -eq 1" \| select Name` Get all administrative groups
- `Get-ADUser -Filter {adminCount -eq '1' -and DoesNotRequirePreAuth -eq 'True'}` Find admin users that don't require Kerberos Pre-Auth
- `Get-ADUser -Filter {adminCount -gt 0} -Properties admincount,useraccountcontrol` Enumerate UAC values for admin users
- `Get-WmiObject -Class win32_group -Filter "Domain='INLANEFREIGHT'"` Get AD groups using WMI
- `([adsisearcher]"(&(objectClass=Computer))").FindAll()` Use ADSI to search for all computers
- `(Get-ADGroup -Identity "Help Desk" -Properties *).Member.Count` Get number of users in Help Desk Group
- `(Get-ADUser -filter * | select Name).count`Get number of Users in domain
- `(Get-ADComputer -filter * | select Name).count` Get number of Computers in domain
- `(Get-ADGroup -filter * | select Name).count` Get number of groups in domain
- `Get-ADUser -Filter {adminCount -eq '1' -and DoesNotRequirePreAuth -eq 'True'}` Filter Admin users

## Resources

- [AD on HTB Academy](https://academy.hackthebox.com/)
- [Get AD User Data via Powershell](http://woshub.com/get-aduser-getting-active-directory-users-data-via-powershell/)
- [Powershell commands for managing AD](https://vschamarti.wordpress.com/2019/11/02/powershell-commands-for-managing-active-directory/)