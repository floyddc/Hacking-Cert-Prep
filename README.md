# 🗂️ TRY HACK ME - personal collection 
- 🧑‍💻`\exploited-machines` collection of some THM machines that I was able to compromise.
- 📖`\notes` collection of notes for every topic of the THM learning path. 

https://tryhackme.com/

## Preliminary steps for exploiting machines

- Download your VPN connection config file 
  - `Account`->`Access`->`Download configuration file`
- Connect to the VPN
  - `sudo openvpn <filename>.ovpn`
- Save the IP address of the machine
  - `settarget <IP>` (custom command)
- Create a dedicated directory
  - `mkdir <machine dir>`
- Create an organized workspace
  - `cd <machine dir>`
  - `mkhackdir` (custom command)
    - This will create 5 empty directories:
      - `/content`
      - `/credentials`
      - `/exploits`
      - `/nmap`
      - `/scripts` 
- Now you're ready to start.