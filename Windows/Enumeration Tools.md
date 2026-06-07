**PowerUp and SharpUp**
-  [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/SharpUp.exe)
```
.\PowerUp.ps1
Invoke-AllChecks
```
```
# Similar to PowerUp with Invoke-AllChecks
.\SharpUp.exe
```
![](assets/Pasted%20image%2020260607104318.png)

- some examples of findings
![](assets/Pasted%20image%2020260607104351.png)



**[Seatbelt](https://github.com/GhostPack/Seatbelt)**
- [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Seatbelt.exe)
- outputs information about system by default
- does not automatically search for privilege escalation techniques - leaves it to user
```
.\Seatbelt.exe
```
- brings up help menu with each of the checks



**WinPEAS**
before running WinPEAS add the following registry key
```
reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1
```
- then open a new command prompt
- enabled colors

running with -h shows all the checks available
```
.\winPEASny.exe -h
```
![](assets/Pasted%20image%2020260607105106.png)
- can help since winPEAS gives way too much output


**Accesschk.exe**
old tool, but trusted for checking access permissions
- can check if a user or group has perms over groups, files, registries, or processes
- first run requires `/accepteula` flag (only on older versions)