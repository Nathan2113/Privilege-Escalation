**Using ExploitDB**
use all the following filters
![](assets/Pasted%20image%2020260607144649.png)
- most of the exploits rely on the same misconfigurations covered earlier in the course


1. Manually enumerate all running programs using tasklist or seatbelt
```
# Tasklist
tasklist /V

# Seatbelt used for non-standard processes
.\seatbelt.exe NonstandardProcesses
```
![](assets/Pasted%20image%2020260607145409.png)
- seatbelt gives full paths - can tell you version number


1. WinPEAS can do it too with `procesinfo` flag
	- `procesinfo` is misspelled in the tool
```
.\winPEASany.exe quiet procesinfo
```
![](assets/Pasted%20image%2020260607145532.png)
![](assets/Pasted%20image%2020260607145552.png)
- use exploitDB on interesting programs found here

