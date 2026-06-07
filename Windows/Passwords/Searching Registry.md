**Searching Registry**
```
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```
- searches registry entries for any string containing "password"
	- very noisy, so often more fruitful to look in known locations