# Domain Computers and Servers Enumeration

Enumerate servers in the network:

`Get-DomainComputer`

Enumerate operating systems:

`Get-DomainComputer -OperatingSystem "*server 2016*"`

Check host's connection to the computers in the network:

`Get-DomainComputer -Ping`

Enumerate a specific machine by DNS host name:

`Get-DomainComputer  -Name fileshare.domain.local`

`Get-DomainComputer  -Name web.domain.local`

