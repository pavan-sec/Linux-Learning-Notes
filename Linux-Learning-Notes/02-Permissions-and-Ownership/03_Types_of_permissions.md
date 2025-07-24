# Types of permissions

# Understanding Linux File Permissions

Linux file permissions are a fundamental security mechanism that determines who can read, write, or execute files and directories. Every file and directory on a Linux system has associated permissions that control access for the **owner**, the **group**, and **others**.

### Three Types of Permissions

There are three primary types of permissions you can apply:

1.  **Read (`r`)**:
    * **Files:** Allows you to **view the contents** of the file.
    * **Directories:** Allows you to **list the contents** of the directory (i.e., see what files/subdirectories are inside).

2.  **Write (`w`)**:
    * **Files:** Allows you to **modify, save, or delete** the file.
    * **Directories:** Allows you to **create, delete, or rename files** within that directory.

3.  **Execute (`x`)**:
    * **Files:** Allows you to **run the file** as a program or script.
    * **Directories:** Allows you to **enter or traverse** the directory (i.e., `cd` into it) and access its subdirectories and files.

### Permission String Breakdown

Permissions are typically displayed in a 10-character string, for example, `drwxr-xr-x`. Let's break down what each part signifies:

drwxr-xr-x
│ │   │  └── Others (everyone else)
│ │   └───── Group
│ └──────── User (owner)
└────────── File type ('d' means directory)

* **1st character:** Indicates the **file type**.
    * `d`: Directory
    * `-`: Regular file
    * `l`: Symbolic link
    * (and others like `c` for character device, `b` for block device)

* **Characters 2-4 (`rwx`):** Represent the **permissions for the User (Owner)**. This is the user account that owns the file or directory. In `drwxr-xr-x`, the owner has read, write, and execute permissions.

* **Characters 5-7 (`r-x`):** Represent the **permissions for the Group**. The "group" refers to a Linux group (e.g., `users`, `sudo`, `kali`, `developers`). Any user who is a member of this specific group will have these permissions. In `drwxr-xr-x`, the group has read and execute permissions (but no write).

* **Characters 8-10 (`r-x`):** Refer to the **permissions for Others**. "Others" means any user on the system who is **neither** the owner of the file/directory **nor** a member of the group associated with that file/directory. In `drwxr-xr-x`, others have read and execute permissions (but no write).

### Permission Shortcuts (Octal Values)

Each permission type (`r`, `w`, `x`) has a numerical value, allowing you to represent permissions concisely using octal (base-8) numbers.

| Permission          | Symbol | Value |
| :------------------ | :----- | :---- |
| Read                | `r`    | 4     |
| Write               | `w`    | 2     |
| Execute             | `x`    | 1     |
| No                  | `-`    | 0     |

To determine the numerical permission for a specific set (User, Group, or Others), you **add the values** of the permissions granted.

* `rwx` (Read, Write, Execute) &rarr; 4 + 2 + 1 = **7**
* `r-x` (Read, Execute) &rarr; 4 + 0 + 1 = **5**
* `rw-` (Read, Write) &rarr; 4 + 2 + 0 = **6**
* `r--` (Read only) &rarr; 4 + 0 + 0 = **4**
* `---` (No permissions) &rarr; 0 + 0 + 0 = **0**

For example, `drwxr-xr-x` translates to:
* User: `rwx` &rarr; **7**
* Group: `r-x` &rarr; **5**
* Others: `r-x` &rarr; **5**

So, `drwxr-xr-x` is often referred to as **`755`** permissions.

### Special Permissions (Brief Overview)

Beyond the standard `rwx` permissions, there are three special permission bits that can be applied:

1.  **SetUID (SUID - 4)**: If set on an executable file, the file will run with the permissions of the file owner (e.g., `root`), not the user executing it. `s` replaces `x` in the user's permission.
2.  **SetGID (SGID - 2)**: If set on an executable file, the file runs with the permissions of the file's group. If set on a directory, new files/directories created within it will inherit the group of the parent directory. `s` replaces `x` in the group's permission.
3.  **Sticky Bit (1)**: If set on a directory, only the owner of a file (or the directory's owner, or root) can delete or rename files within that directory, even if they have write permissions to the directory. `t` replaces `x` in the others' permission.

These special permissions are represented by an additional leading digit in the octal notation (e.g., `4755` for SUID `rwxr-xr-x`).