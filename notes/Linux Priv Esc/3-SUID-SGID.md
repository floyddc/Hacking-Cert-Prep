# Privileges Escalation - Linux
# Exploiting SUID/SGID 

## Executables
- `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null` to look for executables, hoping some of them have an obsolete (so vulnerable) version.
- Search those versions on https://exploit-db.com or somewhere else, for example Github.
- If you find something interesting, copy the exploit and paste it on a `.sh` file, to make it runnable.
- Then run it to escalate privileges. Check if you became **root** with `whoami`.

## Shared objects
Some binaries could be vulnerable to shared objects injections.
- `strace <BINARY PATH> 2>&1 | grep -iE "open|access|no such file"` to look for missing dependencies.
- If you find a missing file from an accessible location (for example the `/home` directory), you could create it and place a root shell in it.



