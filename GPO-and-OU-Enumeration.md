# GPO and OU Enumeration

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
