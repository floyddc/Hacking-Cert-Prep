# Privileges Escalation - Linux
# Enumeration

During this first step, we are going to get some preliminaries info about the system of the machine we are in.

- [User and groups](#user-and-groups)
- [System](#system)
- [Processes](#processes)
- [Network](#network)
- [Find command](#find-command)
- [Automated tools](#automated-tools)

## User and groups
- `whoami` to check the current user.
- `id` to get info about the current user.
- `groups` to check which groups the user belongs to.

## System
- `hostname` to check the hostname. In some cases, it can provide useful info about the target.
- `uname -a` to get info about the kernel.
- `cat /proc/version` (similar to the previous command) to get the kernel version and check which compiler (GCC) is installed. ([see Kernel exploitation](1.1-(Ex)%20Kernel%20exploitation.md))
- `cat /etc/issue` to check the version of the Operating System.
- `env` to check the environments variables, the default shell... (if the PATH variable includes a compiler or a scripting language, it could be exploited to run code with high privileges)

## Processes
- `ps -a` to check all the processes running on the machine.
- `ps axjd` to check the process tree.
- `ps aux` to check all the processes, which users are running these processes and which processes are not attached to a Terminal.

## Network
- `ip route` to check the network routes.
- `netstat -a` to check all listening ports and established connections.
- `netstat -i` to get interfaces statistics.

## Find command
- `find /home -user <Username>` to look for a specific user in the `/home` directory.
- `find . -name <Filename>` to look for something in the current directory.
- `find / -name <Filename>` to look for something in the entire filesystem.
  - `... -type d ...` to specify that we are looking for a directory.
  - `... -type f ...` to specify that we are looking for a file.

## Automated tools
- **LinPeas**: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
- **LinEnum**: https://github.com/rebootuser/LinEnum
- **LES (Linux Exploit Suggester)**: https://github.com/mzet-/linux-exploit-suggester
- **Linux Smart Enumeration**: https://github.com/diego-treitos/linux-smart-enumeration
- **Linux Priv Checker**: https://github.com/linted/linuxprivchecker 