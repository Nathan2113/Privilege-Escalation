**Access Tokens**
- Primary Access Token
	- given when user logs in, tied to their session, programs run as their privileges
- Impersonation Access Token
	- created when a process needs to run in the context of another user


**Token Duplication**
Windows allows processes/threads to duplicate their access tokens
- impersonation token can be duplicated into a primary access token this way


**Named Pipes**
```
systeminfo | findstr Windows
```
- takes output of systeminfo and provides it as input to the findstr command
	- process can create a named pipe, and other processes can open the named pipe to read or write data from/to it
	- process which created the named pipe can impersonate the security context of a process which connects to the named pipe



**getsystem**
- in metasploit meterpreter shell to get system privileges
	- what does it do?
- [Source Code](https://github.com/rapid7/metasploit-payloads/tree/d672097e9989e0b4caecfad08ca9debc8e50bb0c/c/meterpreter/source/extensions/priv)
	- main files of note are evelate.c, namedpipe.c, and tokendup,c

1. Named Pipe Impersonation (In memory/admin)
	- creates a named pipe controlled by Meterpreter
	- creates a service (running as SYSTEM) which runs a command that interacts directly with the named pipe
	- Meterpreter impersonates the connected process to get an impersonation token
	- access token assigned to all subsequent Meterpreter threads



2. Named Pipe Impersonation (Dropper/Admin)
	- very similar to Named Pipe Impersonation (in memory/admin)
	- only difference is that a DLL is written in disk, and a service is created which runs DLL as SYSTEM
	- DLL connects to the named pipe



3. Token Duplication (in memory/admin)
	- requires `SeDebugPrivilege`
	- finds a service running as SYSTEM which it injects a DLL into
	- DLL duplicates the access token of the service and assigns to Meterpreter
	- currently only works on x86 architectures
	- only technique that does not have to create a service, and operates entirely in memory


![](assets/Pasted%20image%2020260607155132.png)
