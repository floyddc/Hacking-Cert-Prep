# Privileges Escalation - Linux

## Sensitive files
- `/etc/shadow` contains user password hashes and is usually readable only by the root user.<br>
If it's vulnerable (for example, world-readable)
  - `cat /etc/shadow` to read it
  - Get the hash we are interested into (between the first and second `:`) and save it on a text file
  - `john --wordlist=/usr/share/wordlists/rockyou.txt <file>` to try to brute force the hash and convert it into a plain text password
  - `mkpasswd -m sha-512 <new password>` to generate a new hashed password and then replace it
- `/etc/passwd` contains info about users. It's world-readable, but usually only writable by the root user. Some versions of Linux will still allow password hashes to be stored there. We could exploit it in the same way of before
  - `openssl passwd <new password>` to generate a new hashed password and then place it between the first and second `:`, replacing the `x`

Use `su <user>` to switch between users<br>
Use `id` to get info about the current user