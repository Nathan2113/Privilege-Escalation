**Listing Privileges**
```
whoami /priv
```
- "disabled" in the state column is irrelevant here, you user has it, but the current process restricts it


**SeImpersonatePrivilege**
- impersonate access tokens
- if any access token from SYSTEM is obtained, then a new process can be spawned using that token
	- JuicyPotato



**SeAssignPrimaryPrivilege**
- similar to SeImpersonate
- enabled a user to assign an access token
	- JuicyPotato



**SeBackupPrivilege**
- grants read access to all objects on the system
- SAM/SYSTEM extraction
- reading registry



**SeRestorePrivilege**
- write access to all objects on the system
- multiple ways to exploit
	- modify service binaries
	- overwrite DLLs used by SYSTEM processes
	- modify registry settings
	- and so on...


**SeTakeOwnershipPrivilege**
- take ownership over an object via WRITE_OWNER
	- modify ACL and grant write access
- then use same methods as SeRestorePrivilege after setting write access



**Other Privileges (More Advanced)**
- SeTcbPrivilege
- SeCreateTokenPrivilege
- SeLoadDriverPrivilege
- SeDebugPrivilege (used by getsystem)