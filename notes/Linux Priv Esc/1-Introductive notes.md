# Privileges Escalation - Linux
# Introductive notes

## Useful commands explained
`sudo` is a command that can be used only by users specified in `/etc/sudoers` file ([see Sensitive files](2-Sensitive%20files.md)). Everytime a user run a command preceded by `sudo`, he runs it as the **root user**.<br>
Other useful commands:
- `whoami` to check the current user.
- `id` to get info about the current user.
- `groups` to check which groups the user belongs to.
- `sudo usermod -aG sudo <user>` to add a specific user to the sudo group (so he can use sudo command.)
- `sudo -s` to become superuser (**root**).
- `sudo -u <user> <command>` to run a command impersonating the specified user.
- `su <user>` to switch between users (password needed).
- `sudo -l` to list commands and programs which the current user is allowed to run with `sudo`.

## Finding SUID/SGID executables

- `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`, explained:
  - `find /` finds in the entire filesystem
  - `-type f` only files
  - `-a` and (it links commands)
  - `\( -perm -u+s -o -perm -g+s \)` find files with SUID or SGID of **any user** (also root)
  - `-exec ls -l {}` executes the `ls -l` command
  - `2> /dev/null` ignores error messages

- `find / -type f -perm -4000 -user root 2>/dev/null`, explained:
  - `find /` finds in the entire filesystem
  - `-type f` only files
  - `-perm -4000 -user root` find files with SUID of **root**
  - `2> /dev/null` ignores error messages

- `strace <BINARY PATH> 2>&1 | grep -iE "open|access|no such file"` to look for missing dependencies, or open/access attempts.





