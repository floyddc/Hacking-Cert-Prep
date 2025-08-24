# 🗂️ COLLECTION TO GET READY FOR HACKING CERTIFICATIONS 
- 🧑‍💻`\THM-machines` collection of some [TryHackMe](https://tryhackme.com/) machines that I was able to compromise.
- 📖`\notes` collection of notes to get ready for a cybersecurity career

## Preliminary steps for exploiting THM machines
- Download your VPN connection config file 
  - `Account`->`Access`->`Download configuration file`
- Connect to the VPN
  - `sudo openvpn <filename>.ovpn`
- Save the IP address of the machine
  - `settarget <IP>` (custom command)
- Create a dedicated directory, create 5 empty directories (`/content` `/credentials` `/exploits` `/nmap` `/scripts` ) and get in
  - `mkhackdir <machine dir>` (custom function)
- Now you're ready to start.
