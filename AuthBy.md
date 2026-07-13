![[Pasted image 20260713154045.png]]
- FTP and RDP open
	- FTP version is zFTPServer 6.0
- HTTP server on 242

![[Pasted image 20260713154135.png]]
- HTTP server requires auth


vFTPServer 6.0 is weak to [directory traversal](https://github.com/advisories/GHSA-3wvj-8r5h-mr3c)
- looks like entire server is locked down the access denied - probably come back after getting creds

![[Pasted image 20260713160100.png]]
- logging in with admin:admin worked :)


after downloading `.htpasswd` and `.htaccess`, found credentials
![[Pasted image 20260713160439.png]]
```
offsec:$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0
```

hashcat says it's an apache `$apr1$ MD5` hash (mode 1600)
![[Pasted image 20260713160630.png]]


`hashcat -m 1600 '$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0' /usr/share/wordlists/rockyou.txt` gives the password 'elite'
![[Pasted image 20260713160815.png]]
```
offsec:elite
```

the creds worked for the website
![[Pasted image 20260713160842.png]]
- still doesn't work for the ftp servers though