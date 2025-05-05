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
- Create a dedicated directory, create 5 empty directories (`/content` `/credentials` `/exploits` `/nmap` `/scripts` ) and get in
  - `mkhackdir <machine dir>` (custom function)
- Now you're ready to start.