# Bloodhound

> Tool's GitHub repo https://github.com/BloodHoundAD/BloodHound

```powershell

PS C:\AD> powershell -ep bypass

PS C:\AD> import-module .\SharpHound.ps1

PS C:\AD> Invoke-BloodHound -CollectionMethod All -Verbose -Domain marvel
```

After the script finishes open up the bloodhound.exe and upload the zip file to the program.

> A good [tutorial](https://youtu.be/_Mo9RjCMYLU) on BloodHound 
