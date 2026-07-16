On older versions of Windows, users could be granted permission to run certain GUI apps with admin privileges
- similar to sandbox escape


**Example**
1. Open MSPaint and run the following in cmd
```
tasklist /V |findstr mspaint.exe
```
![](assets/Pasted%20image%2020260607143836.png)
- running with admin privileges


2. Click File > Open > Click Navigation Bar > type `file:\\C:\windows\system32\cmd.exe`
![](assets/Pasted%20image%2020260607143915.png)
![](assets/Pasted%20image%2020260607143953.png)


