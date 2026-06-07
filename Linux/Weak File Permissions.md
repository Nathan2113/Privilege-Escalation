**Readable /etc/shadow**
- extract hash and crack it
	- may not have to unshadow, just take the hash between the first and second colon


**Writable /etc/shadow**
- backup the file to restore later
- generate a new hash so we know the password
	- `mkpasswd -m sha-512 newpassword`
		- change algorithm accordingly
- inject into `/etc/shadow` file (between two colons)


**/etc/passwd**
historically contained hashes
- if we can write to it, we can inject a hash into backwards compatible systems
	- or create a user with uid 0


configuration of file
- root account in `/etc/passwd` is usually configured like this
	- `root:x:0:0:root:/root:/bin/bash`
	- the 'x' instructs linux to look for the password hash in `/etc/shadow`
	- in some versions of linux, if we get rid of the 'x' it interprets the user as nopasswd
	- `root::0:0:root:/root:/bin/bash`


Changing user password with `/etc/passwd`
- create new password for root
	- `openssl passwd "password"`
![](assets/Pasted%20image%2020260531150355.png)

- edit `/etc/passwd/` - enter hash into second field where 'x' is
![](assets/Pasted%20image%2020260531150425.png)

- switch to root user using new password


OR create alternative user
![](assets/Pasted%20image%2020260531150507.png)
- "newroot" on bottom
- works because username is different, but uid is still 0



**Backups**
Common locations
- user home directories
- `/`
- `/tmp`
- `/var/backups`


**SSH**
- ALWAYS look for hidden ssh folders
	- such as in `/`

- check if root login is permitted for SSH
	- `grep PermitRootLogin /etc/ssh/sshd_config`
![](assets/Pasted%20image%2020260531150743.png)

- copy key over to kali and give correct permissions
`chmod 600 root_key`

- use key to ssh
`ssh -i root_key root@<IP>`


