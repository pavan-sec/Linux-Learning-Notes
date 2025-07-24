# Disk usage

du - estimate file space usage

define it, 
write all options or command with du like du -s or du -sh limilarly all 

alos prove the info of how grep will help in this command. 

df     - report file system space usage
explain this, with all arguments or options and differnt drives we can output. same how grep used in this format 

### Understanding Disk Usage in Linux: `du` & `df`

Knowing how to check disk space is a fundamental skill for any Linux user. The two primary commands for this are `du` (disk usage) and `df` (disk free). While they sound similar, they serve different purposes. This guide breaks them down with their most common options and examples.

---

## `du` - Estimate File & Directory Usage

The `du` command is used to calculate and display the amount of disk space used by **files and directories**. It works from the "bottom-up," meaning it looks at the individual files within a directory to calculate the total size. This is useful for finding out what's taking up all your space.

By default, `du` shows the size in kilobytes and lists every subdirectory.

### Common `du` Options

You can modify the behavior of `du` with various flags (options). Here are the most essential ones:

| Option | Description | Example |
| --- | --- | --- |
| `-h` | **H**uman-readable format. Displays sizes in K (Kilobytes), M (Megabytes), and G (Gigabytes). | `du -h` |
| `-s` | **S**ummarize. Displays only the grand total size for the specified directory, not for each subdirectory. | `du -s /home/user/documents` |
| `-a` | **A**ll. Shows the disk usage for all files, not just directories. | `du -a /home/user/downloads` |
| `-c` | **C**reate a grand total. Adds a "total" line at the very end when processing multiple files or directories. | `du -c /var/log /tmp` |
| `--max-depth=N` | Display the total for a directory only if it is N or fewer levels deep from the starting point. | `du -h --max-depth=1` |

**Combining Options:** The most common and useful combination is `du -sh`:

```bash
# Get a human-readable summary of the current directory's total size
du -sh .

# Example Output:
# 1.2G    .
```

### Filtering `du` with `grep`

The `du` command can produce a lot of output. You can pipe (`|`) its output to the `grep` command to find specific information. This is great for hunting down particular file types or directories.

**Example:** Find the disk usage of all `.log` files in the `/var/log` directory.

Bash

`# First, run 'du' with the -a (all files) and -h (human-readable) flags
#### Then, pipe the result to 'grep' to filter for lines ending in ".log"
du -ah /var/log | grep "\.log$"

#### Example Output:
#### 8.0K    /var/log/boot.log
#### 24K     /var/log/Xorg.0.log
#### 120K    /var/log/kern.log`

## `df` - Report Filesystem Space Usage 💿

The `df` command provides a high-level overview of the **disk space usage for entire filesystems** (like your hard drives, SSDs, and mounted network shares). Think of `df` as checking the total capacity of your storage drives and how much space is free.

### Common `df` Options

Here are the most useful options for the `df` command:

| Option | Description | Example |
| --- | --- | --- |
| `-h` | **H**uman-readable format. Displays sizes in G (Gigabytes), M (Megabytes), etc. | `df -h` |
| `-T` | Show the filesystem **T**ype (e.g., `ext4`, `ntfs`, `apfs`). | `df -hT` |
| `-i` | Show **i**node information instead of block usage. Inodes are used to store file metadata. | `df -i` |
| `-a` | **A**ll. Include pseudo, duplicate, and inaccessible file systems in the output. | `df -a` |

**Checking a Specific Drive:** You can also specify a drive or mount point to see its usage directly.

Bash

`# Check the usage of the root filesystem in a human-readable format
df -h /

#### Example Output:
#### Filesystem      Size  Used Avail Use% Mounted on
#### /dev/sda1       228G   60G  157G  28% /`

### Filtering `df` with `grep`

Just like with `du`, you can pipe the output of `df` to `grep` to quickly find the information you need. This is useful on systems with many mounted drives.

**Example:** Show only the physical disk partitions (like `sda` or `nvme`) and ignore temporary file systems.

Bash

`# Run 'df -h' and pipe it to 'grep' to find lines starting with "/dev/sd" or "/dev/nvme"
# The '^' means "start of the line"
df -h | grep "^/dev/sd"

#### Example Output:
#### /dev/sda1       228G   60G  157G  28% /
#### /dev/sdb2       931G  450G  481G  49% /mnt/data`

**Example 2:** Find all filesystems of a specific type.

Bash

`# Run 'df' with the -T flag and filter for the 'ext4' filesystem type
df -hT | grep "ext4"

#### Example Output:
#### /dev/sda1       ext4    228G   60G  157G  28% /
#### /dev/sdb2       ext4    931G  450G  481G  49% /mnt/data`
