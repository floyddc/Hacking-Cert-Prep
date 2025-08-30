# Reconnaissance
# Passive recon
Passive reconnaissance is based on getting public info about our target, without engaging it.

- [Whois](#whois)
- [Nslookup](#nslookup)
- [Dig](#dig)
- [DNSDumpster and Shodan](#dnsdumpster-and-shodan)


## Whois
It's a request and response protocol. The Whois server stores all registered records.
- `whois <Domain>` to get various info related to the domain requested.

## Nslookup
It stands for Name Server Lookup.
- `nslookup -type=<Type> <Domain> <Server>` to get the IP address and other DNS info related to the domain requested.<br>

**Types:** 
  - `A` (IPv4 addresses).
  - `AAAA` (IPv6 addresses).
  - `CNAME` (canonical name).
  - `MX` (mail servers).
  - `SOA` (Start of Authority).
  - `TXT` (TXT records).<br>

**DNS servers:** 
  - `1.1.1.1` (Cloudflare).
  - `1.0.0.1` (Cloudflare).
  - `8.8.8.8` (Google).
  - `8.8.4.4` (Google).
  - `9.9.9.9` (Quad9).
  - `149.112.112.112` (Quad9).

## Dig
It returns more detailed info than Nslookup.
- `dig @<Server> <Domain> <Type>` to get detailed DNS info related to the domain requested.<br>

## DNSDumpster and Shodan
These websites provides us interesting info without actively connecting to the target, such as:
- IP address.
- DNS info.
- Geographic location.
- Server type and version.
