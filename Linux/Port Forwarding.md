If for some reason, an exploit cannot run locally on the target machine, the port can be forwarded to SSH to **your local machine**
- `ssh -R <local-port>:127.0.0.1:<service-port> <user>@<local-machine>`
	- exploit code can now be run on your local machine at whichever port you use


**MySQL Client Example**
want to run mysql commands on our local machine - for some reason they aren't working on theirs

check that mysql is running
- `netstat -nl`
![](assets/Pasted%20image%2020260531145116.png)
- showing localhost address - can't use it remotely

set up the port forward
- `ssh -R 4444:127.0.0.1:3306 root@<kali_ip>`
	- forwarding mysql (3306) to OUR port 4444


connect to user in Kali
- `mysql -u <user> -h 127.0.0.1 -P 4444`


confirm by viewing hostname
`select @@hostname`
