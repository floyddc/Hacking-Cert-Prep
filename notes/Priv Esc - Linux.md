# Privileges Escalation - Linux

## Sensitive files
- `/etc/shadow` contains user password hashes and is usually readable only by the root user.<br>
If it's vulnerable (for example, world-readable)
  - `cat /etc/shadow` to read it
  <img src="../imgs/shadow.png" alt="shadowImg" />
  That complex string between the first and second `:` is the hashed password of user "diego"
  - `john --wordlist=/usr/share/wordlists/rockyou.txt <hash.txt>` to try to brute force the hash and convert it into a plain text password
    - if any worldlist is specified, the default one is `/usr/share/john/password.lst`
    - UPDATE: probably John The Ripper could return an error message because it doesn't recognize modern hashes, like `yescrypt`. Check it with `john <file> --format=crypt`
  - `mkpasswd -m sha-512 <new password>` to generate a new hashed password and then replace it
<br><br>

- `/etc/passwd` contains info about users. It's world-readable, but usually only writable by the root user. 
Some versions of Linux will still allow password hashes to be stored there. We could exploit it in the same way of before
  - `cat /etc/shadow` to read it
  <img src="../imgs/passwd.png" alt="passwdImg" />
  That `x` means that any hash is set for user "diego"<br>
  That `/home/diego` is his home directory<br>
  That `/bin/zsh` is his default shell<br><br>
  - `openssl passwd <new password>` to generate a new hashed password and then place it between the first and second `:`, replacing the `x`

- `/etc/sudoers` contains info about permissions of users and groups. Its usually readable only by the root user.
  - `cat /etc/sudoers` to read it
  <img src="../imgs/sudoers.png" alt="sudoersImg" />

Use `su <user>` to switch between users<br>
Use `id` to get info about the current user