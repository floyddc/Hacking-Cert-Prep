# Reconnaissance
# Active recon
Active reconnaissance is based on getting deeper info about our target, engaging it directly.

- [Web Browser](#web-browser)
- [Ping](#ping)
- [Traceroute](#traceroute)
- [Telnet](#telnet)
- [Netcat](#netcat)


## Web Browser
It can be very interesting using its add-ons, for example (Mozilla Firefox):
- `FoxyProxy` to change our proxy server (useful with Burpsuite, to capture packets and analyze them).
- `Wappalyzer` (technology profiler).

## Ping
It helps us to check if a system is reachable: we send an ICMP Echo packet and wait for an ICMP Echo reply.<br>
**NOTE**: MS Windows Firewall will block it by default.<br>
- `ping <Options> <IP/Hostname>`.<br>

**Options:** 
  - `-c <Packets>` (Linux machine).
  - `-n <Packets>` (Windows machine).
  - `-W <Timeout>`.
  - `-i <Interval>`. 
  - `-I <Interface>`.
  - `-s <Packet size>`.<br>