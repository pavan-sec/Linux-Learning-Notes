# Changing & Setting Permissions in Linux

Managing file permissions is a critical aspect of Linux system administration and security. The `chmod` command is your primary tool for modifying these permissions, while `chown` and `chgrp` handle ownership.

### `chmod` - Change Mode (Permissions)

The `chmod` command is used to **change file mode bits**, which directly control the read, write, and execute permissions of a file or directory. You can use it in two main ways: **Octal (Numeric) Format** or **Symbolic Format**.

#### 1. Octal (Numeric) Format

This method uses the numerical values for permissions (Read=4, Write=2, Execute=1) to set permissions for the User, Group, and Others simultaneously.

| Permission          | Symbol | Value |
| :------------------ | :----- | :---- |
| No permission       | `---`  | 0     |
| Execute             | `--x`  | 1     |
| Write               | `-w-`  | 2     |
| Write & Execute     | `-wx`  | 3 (2+1) |
| Read                | `r--`  | 4     |
| Read & Execute      | `r-x`  | 5 (4+1) |
| Read & Write        | `rw-`  | 6 (4+2) |
| Read, Write, Execute | `rwx`  | 7 (4+2+1) |

**Examples:**

* **`chmod 755 filename.sh`**
    * **Meaning:** Sets permissions to `rwxr-xr-x`.
    * **Breakdown:**
        * User: 7 (`rwx`) - Owner can read, write, execute.
        * Group: 5 (`r-x`) - Group members can read, execute.
        * Others: 5 (`r-x`) - All other users can read, execute.
    * **Common Use Case:** Executable scripts for all users, but only owner can modify.

* **`chmod 700 private_dir/`**
    * **Meaning:** Sets permissions to `rwx------`.
    * **Breakdown:**
        * User: 7 (`rwx`) - Only the owner can read, write, and execute/access.
        * Group: 0 (`---`) - No permissions for the group.
        * Others: 0 (`---`) - No permissions for others.
    * **Common Use Case:** Highly private files/directories accessible only by the owner.

* **`chmod 644 document.txt`**
    * **Meaning:** Sets permissions to `rw-r--r--`.
    * **Breakdown:**
        * User: 6 (`rw-`) - Owner can read and write.
        * Group: 4 (`r--`) - Group members can only read.
        * Others: 4 (`r--`) - All other users can only read.
    * **Common Use Case:** Text documents that the owner can edit, but everyone else can only view.

#### 2. Symbolic Format

This method uses symbols to add (`+`), remove (`-`), or set (`=`) permissions for specific entities: `u` (user), `g` (group), `o` (others), or `a` (all: u+g+o).

**Examples:**

* **`chmod u+x my_script.sh`**
    * **Meaning:** **Adds execute permission** (`x`) only for the **user (owner)** (`u`).
    * **Example Before/After:** If `my_script.sh` was `rw-r--r--`, it becomes `rwxr--r--`.

* **`chmod g-w group_file.txt`**
    * **Meaning:** **Removes write permission** (`w`) for the **group** (`g`).
    * **Example Before/After:** If `group_file.txt` was `rw-rw-r--`, it becomes `rw-r--r--`.

* **`chmod o=r public_doc.pdf`**
    * **Meaning:** **Sets** (equals `=`) **read permission** (`r`) for **others** (`o`), removing any other permissions they might have had.
    * **Example Before/After:** If `public_doc.pdf` was `rw-r--rwx`, it becomes `rw-r--r--`.

* **`chmod a+rx everyone_can_run.sh`**
    * **Meaning:** **Adds read and execute permissions** (`rx`) for **all** (`a`) (user, group, and others).
    * **Example Before/After:** If `everyone_can_run.sh` was `rw-------`, it becomes `rwxr-xr-x`.

#### Recursive Permissions (`-R` or `--recursive`)

* **Purpose:** Apply permission changes to a directory and all its contents (subdirectories and files).
* **Example:**
    ```bash
    chmod -R 755 my_project_folder/
    ```
    This command will set `755` permissions for `my_project_folder` and every file and subdirectory within it. Use with caution!

### File & Directory Ownership (`chown`, `chgrp`)

Beyond permissions, every file and directory in Linux has an **owner user** and an **owner group**. You need superuser (root) privileges to change ownership for files you don't own.

1.  **`chown` - Change Ownership**
    * **Purpose:** Changes the **user owner** of a file or directory. You often need `sudo` or root access to use this command.
    * **Syntax:** `sudo chown <new_owner_username> <file_or_directory>`
    * **Example:**
        ```bash
        sudo chown root test.sh            # Changes owner of test.sh to 'root'
        ```
    * **Changing User and Group Simultaneously:**
        * **Syntax:** `sudo chown <new_owner_username>:<new_group_name> <file_or_directory>`
        * **Example:**
            ```bash
            sudo chown myuser:webgroup index.html # Changes owner to 'myuser' and group to 'webgroup'
            ```
    * **Recursive Ownership Change:**
        * **Syntax:** `sudo chown -R <new_owner> <directory>/`
        * **Example:**
            ```bash
            sudo chown -R www-data /var/www/html # Changes owner of web files to 'www-data'
            ```

2.  **`chgrp` - Change Group Ownership**
    * **Purpose:** Changes the **group owner** of a file or directory. You usually need to be the owner of the file or have root privileges.
    * **Syntax:** `chgrp <new_group_name> <file_or_directory>`
    * **Example:**
        ```bash
        chgrp developers project_docs.txt  # Changes group of project_docs.txt to 'developers'
        sudo chgrp sudo /etc/some_config   # Changes group of /etc/some_config to 'sudo' (requires sudo)
        ```
    * **Note:** As shown above, `chown` can also change both user and group ownership simultaneously, making `chgrp` less frequently used on its own unless you only need to change the group.