
# An Introduction to Networking in Linux

Linux provides a powerful suite of command-line tools to manage and monitor network connections. This guide will walk you through the most essential commands, from checking your IP address to discovering other devices on your network.

---

## The `ip` Command: The Modern Standard

The `ip` command is the current, all-in-one tool for network configuration in Linux. It is designed to replace older commands like `ifconfig` and `route`.

### `ip addr` - Show Network Addresses

This is the most common subcommand. It shows information about your **network interfaces** (like your Ethernet card `eth0` or Wi-Fi `wlan0`) and their assigned **IP addresses**.

Bash

`ip addr`

**Example Output:**

`1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 0c:9d:92:1f:f2:e5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.10/24 brd 192.168.1.255 scope global dynamic noprefixroute eth0
       valid_lft 85656sec preferred_lft 85656sec`

- `eth0`: The name of the network interface.
- `inet 192.168.1.10/24`: This is the crucial part – your local IPv4 address.

### `ip route show` - Show Routing Table

This command displays the kernel's routing table. Think of this as a **map** that tells your computer where to send network traffic.

Bash

`ip route show`

**Example Output:**

`default via 192.168.1.1 dev eth0 proto dhcp metric 100
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.10 metric 100`

- `default via 192.168.1.1`: This line is the most important. It specifies the **default gateway** (usually your router's IP address) where all outbound internet traffic is sent.

---

While `ip` is the modern tool, you will still find these older commands on many systems.

### `ifconfig`

`ifconfig` (**i**nter**f**ace **config**ure) is the classic command for viewing and managing network interfaces. It is considered **deprecated** but is still useful for a quick IP address check.

Bash

`ifconfig`

### `netstat` - Network Statistics

The `netstat` command is used to display network connections, routing tables, and interface statistics. It's very useful for seeing what services are listening for connections on your machine.

| Option | Description |
| --- | --- |
| `-t` | Show **TCP** connections. |
| `-u` | Show **UDP** connections. |
| `-n` | Show **n**umerical addresses instead of resolving hostnames (much faster). |
| `-l` | Show only **l**istening sockets (i.e., services waiting for a connection). |
| `-p` | Show the **p**rocess ID (PID) and name of the program to which the socket belongs. |
| `-r` | Display the kernel **r**outing table (similar to `ip route`). |

**Most Common Combination:** `sudo netstat -tunlp`
This command is extremely useful for system administrators. It shows all (**t**cp, **u**dp) **l**istening services with **n**umerical ports and the **p**rogram name.

Bash

`sudo netstat -tunlp`

---

## Network Services & Discovery

### `dhclient` - DHCP Client

DHCP (Dynamic Host Configuration Protocol) is the system that automatically assigns an IP address to your computer when it joins a network. `dhclient` is the program that manages this process. You typically don't need to run it manually, as it works automatically in the background. If your network connection is failing, you can try running it to request a new IP address.

Bash

`# Release the current IP address and request a new one for the eth0 interface
sudo dhclient -r eth0 && sudo dhclient eth0`

### `netdiscover` - Network Discovery Tool 📡

`netdiscover` is a simple but effective tool for finding other active devices on your local network. It does this by sending out ARP (Address Resolution Protocol) requests. It's a great way to map out what's connected to your network.

| Option | Description |
| --- | --- |
| `-i device` | Specify the network **i**nterface to scan on (e.g., `eth0`). |
| `-r range` | Scan a specific **r**ange of IP addresses (e.g., `192.168.1.0/24`). |
| `-p` | **P**assive mode. Doesn't send any packets, just quietly listens for traffic. |
| `-s time` | **S**leep time in milliseconds between each request (to be less aggressive). |

**Example:** Scan the `192.168.1.0/24` network range using the `eth0` interface.

Bash

`# You will likely need to run this with sudo
sudo netdiscover -i eth0 -r 192.168.1.0/24`

The command will run continuously, listing every device it finds, including its IP address, MAC address, and hardware vendor. Press `Ctrl+C` to stop it.