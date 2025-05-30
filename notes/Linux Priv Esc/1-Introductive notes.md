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
