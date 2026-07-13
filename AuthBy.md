<img width="745" height="744" alt="image" src="https://github.com/user-attachments/assets/7ed00178-f50c-4f9e-9fe5-273d701fe502" />

- FTP and RDP open
	- FTP version is zFTPServer 6.0
- HTTP server on 242

<img width="643" height="202" alt="image" src="https://github.com/user-attachments/assets/daea5ec5-e13e-4ba1-9eb8-8ee64624f3fa" />

- HTTP server requires auth


vFTPServer 6.0 is weak to [directory traversal](https://github.com/advisories/GHSA-3wvj-8r5h-mr3c)
- looks like entire server is locked down the access denied - probably come back after getting creds

<img width="610" height="350" alt="image" src="https://github.com/user-attachments/assets/8c07720c-80c6-45e3-8586-4e49d4d791cf" />

- logging in with admin:admin worked :)


after downloading `.htpasswd` and `.htaccess`, found credentials
<img width="515" height="160" alt="image" src="https://github.com/user-attachments/assets/652e82ab-b592-4166-bfae-f0e1a9e79980" />

```
offsec:$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0
```

hashcat says it's an apache `$apr1$ MD5` hash (mode 1600)
<img width="711" height="230" alt="image" src="https://github.com/user-attachments/assets/523129d2-5ab6-42bc-b51b-b8e3a1fd3d70" />



`hashcat -m 1600 '$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0' /usr/share/wordlists/rockyou.txt` gives the password 'elite'
<img width="861" height="742" alt="image" src="https://github.com/user-attachments/assets/5946a0c9-3b5a-45a1-86b2-74e4b43a7e3e" />

```
offsec:elite
```

the creds worked for the website
<img width="863" height="195" alt="image" src="https://github.com/user-attachments/assets/c616dd70-0726-497d-8077-9867672eadbc" />
- still doesn't work for the ftp servers though
