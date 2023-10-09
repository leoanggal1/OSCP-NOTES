In situations where we have direct access to an SSH server, behind which is a more complex internal network, classic dynamic port forwarding might be difficult to manage. _sshuttle_[1](https://portal.offsec.com/courses/pen-200-2023/books-and-videos/modal/modules/port-redirection-and-ssh-tunneling/ssh-tunneling/using-sshuttle#fn1) is a tool that turns an SSH connection into something similar to a VPN by setting up local routes that force traffic through the SSH tunnel. However, it requires root privileges on the SSH client and Python3 on the SSH server, so it's not always the most lightweight option. In the appropriate scenario, however, it can be very useful.

In our lab environment, we have SSH access to PGDATABASE01, which we can access through a port forward set up on CONFLUENCE01. Let's run sshuttle through this to observe its capabilities.

First, we can set up a port forward in a shell on CONFLUENCE01, listening on port 2222 on the WAN interface and forwarding to port 22 on PGDATABASE01.

```
confluence@confluence01:/opt/atlassian/confluence/bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
</bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22   
```

> Listing 37 - Forwarding port 2222 on CONFLUENCE01 to port 22 on PGDATABASE01.

Next, we can run **sshuttle**, specifying the SSH connection string we want to use, as well as the subnets that we want to tunnel through this connection (**10.4.50.0/24** and **172.16.50.0/24**).

```
kali@kali:~$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local sudo] Password: 

database_admin@192.168.50.63's password: 

c : Connected to server.
Failed to flush caches: Unit dbus-org.freedesktop.resolve1.service not found.
fw: Received non-zero return code 1 when flushing DNS resolver cache.
```

> Listing 38 - Running sshuttle from our Kali machine, pointing to the forward port on CONFLUENCE01.

Although we don't receive much output from sshuttle, in theory, it should have set up the routing on our Kali machine so that any requests we make to hosts in the subnets we specified will be pushed transparently through the SSH connection. Let's test if this is working by trying to connect to the SMB share on HRSHARES in a new terminal.

```
kali@kali:~$ smbclient -L //172.16.50.217/ -U hr_admin --password=Welcome1234
```