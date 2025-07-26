# 14_LINUX_COMMAND_LINE_CHEAT_SHEET

### SYSTEM INFORMATION

| **Command** | **Description** |
| --- | --- |
| `uname -a` | Display Linux system information |
| `uname -r` | Display kernel release information |
| `lsb_release -a` | Show which version of Ubuntu is installed |
| `uptime` | Show how long the system has been running along with load info |
| `hostname` | Show system host name |
| `hostname -I` | Display the IP addresses of the host |
| `last reboot` | Show system reboot history |
| `date` | Show the current date and time |
| `cal` | Show this month's calendar |
| `w` | Display who is online |
| `whoami` | Show the current logged-in user |

### HARDWARE INFORMATION

| **Command** | **Description** |
| --- | --- |
| `cat /proc/cpuinfo` | Display CPU information |
| `cat /proc/meminfo` | Display memory information |
| `free -h` | Display free and used memory in human-readable format |
| `lspci -tv` | Display PCI devices in a tree view |
| `lsusb -tv` | Display USB devices in a tree view |
| `dmidecode` | Display DMI/SMBIOS hardware info from BIOS |
| `hdparm -i /dev/sda` | Show detailed info about disk `sda` |
| `hdparm -tT /dev/sda` | Perform a read speed test on disk `sda` |

### PERFORMANCE MONITORING AND STATISTICS

| **Command** | **Description** |
| --- | --- |
| `top` | Display and manage the top processes |
| `mpstat 1` | Display processor related statistics |
| `vmstat 1` | Display virtual memory statistics |
| `iostat 1` | Display I/O statistics |
| `tcpdump -i eth0` | Capture/display all packets on interface eth0 |
| `tcpdump -i eth0 'port 80'` | Monitor all traffic on port 80 (HTTP) |
| `lsof` | List all open files on the system |
| `lsof -u user` | List files opened by user |
| `free -h` | Show memory usage in human readable format |
| `watch df -h` | Continuously monitor disk usage |

### USER INFORMATION AND MANAGEMENT

| **Command** | **Description** |
| --- | --- |
| `id` | Display user and group ids of the current user |
| `last` | Show the last users who logged onto the system |
| `who` | Show who is logged into the system |
| `w` | Show who is logged in and what they're doing |
| `groupadd test` | Create a group named "test" |
| `useradd -c "John Smith" -m john` | Create user john with home directory and comment |
| `userdel john` | Delete the john account |
| `usermod -aG sales john` | Add john account to the sales group |

### FILE AND DIRECTORY COMMANDS

| **Command** | **Description** |
| --- | --- |
| `ls -al` | List all files in detailed format |
| `pwd` | Display current working directory |
| `mkdir directory` | Create a new directory |
| `rm file` | Remove a file |
| `rm -r directory` | Recursively delete a directory |
| `rm -f file` | Force delete a file |
| `rm -rf directory` | Forcefully delete directory and contents |
| `rmdir` | Delete a directory |
| `cp file1 file2` | Copy file1 to file2 |
| `cp -r source destination` | Recursively copy source to destination |
| `mv file1 file2` | Rename or move file |
| `ln -s /path/to/file linkname` | Create symbolic link |
| `touch file` | Create an empty file or update timestamp |
| `cat file` | View file contents |
| `less file` | Browse through a text file |
| `head file` | Show first 10 lines of a file |
| `tail file` | Show last 10 lines of a file |
| `tail -f file` | Monitor file as it grows |

### MANIPULATING DATA

| **Command** | **Description** |
| --- | --- |
| `awk`, `perl` | Text/data processing tools |
| `cmp`, `diff` | Compare contents of two files |
| `cut`, `tr` | Cut or translate characters |
| `sort`, `uniq` | Sort or remove duplicate lines |
| `paste`, `join` | Merge or join file contents |
| `sed` | Stream editor |
| `split` | Split large file into smaller files |
| `expand`, `unexpand` | Convert between tabs and spaces |
| `wc` | Count words, lines, characters |
| `look` | Find lines in sorted data |
| `gzip`, `gunzip` | Compress or decompress files |
| `zcat`, `zmore` | View compressed file contents |
| `zcmp`, `zdiff` | Compare compressed files |

### PROCESS MANAGEMENT

| **Command** | **Description** |
| --- | --- |
| `ps`, `ps -ef` | Show currently running processes |
| `ps -ef | grep processname` |
| `top`, `htop` | Show live CPU/memory usage |
| `kill pid`, `killall processname` | Terminate process |
| `program &` | Run a process in background |
| `bg`, `fg`, `fg n` | Manage background/foreground jobs |

### FILE PERMISSIONS

| **Permission String** | **chmod Command** |
| --- | --- |
| `rwxrwxrwx` | `chmod 777 filename` |
| `rwxrwxr-x` | `chmod 775 filename` |
| `rwxr-xr-x` | `chmod 755 filename` |
| `rw-rw-r--` | `chmod 664 filename` |
| `rw-r--r--` | `chmod 644 filename` |

**Legend:**

- `r` = Read
- `w` = Write
- `x` = Execute
- = No permission
- **U** = User
- **G** = Group
- **O** = Others

### NETWORKING

| Command | Description |
| --- | --- |
| `ip a` | Show IP addresses |
| `ifconfig` | Show network interfaces (older systems) |
| `ip link` | Show link-layer info |
| `netstat -tuln` | List open ports and listening services |
| `ss -tulwn` | Modern alternative to netstat |
| `ping <host>` | Test network connectivity |
| `traceroute <host>` | Trace route to a host |
| `dig <domain>` | DNS lookup |
| `host <domain>` | Find IP of a domain |
| `nslookup <domain>` | DNS info (older) |
| `curl ifconfig.me` | Get public IP |
| `wget <url>` | Download from URL |

### ARCHIVES (TAR FILES)

| Command | Description |
| --- | --- |
| `tar -cvf file.tar dir/` | Create tar archive |
| `tar -xvf file.tar` | Extract tar archive |
| `tar -czvf file.tar.gz dir/` | Create gzip compressed archive |
| `tar -xzvf file.tar.gz` | Extract gzip archive |
| `zip file.zip file1 file2` | Create zip archive |
| `unzip file.zip` | Extract zip archive |
|  |  |

### USERS & GROUPS

| Command | Description |
| --- | --- |
| `id` | Show current user UID and GID |
| `whoami` | Show current logged in user |
| `groups` | Show groups of current user |
| `useradd <user>` | Add a new user |
| `passwd <user>` | Set user password |
| `usermod -aG <group> <user>` | Add user to a group |
| `deluser <user>` | Remove user |
| `groupadd <group>` | Add new group |
| `groupdel <group>` | Delete a group |

### FILE PERMISSIONS & OWNERSHIP

| Command | Description |
| --- | --- |
| `chmod 755 <file>` | Change permissions |
| `chown user:group <file>` | Change ownership |
| `umask` | Show default permissions |

### SYSTEM SERVICES

| Command | Description |
| --- | --- |
| `systemctl status` | Show systemd status |
| `systemctl start <service>` | Start a service |
| `systemctl stop <service>` | Stop a service |
| `systemctl restart <service>` | Restart a service |
| `systemctl enable <service>` | Enable at boot |
| `systemctl disable <service>` | Disable at boot |
| `journalctl -xe` | Show systemd logs |

### PACKAGE MANAGEMENT (APT)

| Command | Description |
| --- | --- |
| `apt update` | Update package lists |
| `apt upgrade` | Upgrade packages |
| `apt install <pkg>` | Install a package |
| `apt remove <pkg>` | Remove a package |
| `apt purge <pkg>` | Remove with config |
| `apt autoremove` | Remove unused deps |
| `dpkg -i <file.deb>` | Install .deb file |