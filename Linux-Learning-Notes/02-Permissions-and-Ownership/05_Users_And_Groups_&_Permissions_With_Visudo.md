# A Guide to Users, Groups & Permissions in Linux

Managing who can do what on a Linux system is a critical security skill. This guide covers the fundamentals of creating users and groups, and granting them administrative privileges safely using the `visudo` command.

---

## Managing Users

Every person who uses a Linux system should have their own user account. This ensures accountability and security.

### How to Create a User

The `useradd` command is used to create a new user account. It's best practice to use options to set up the user correctly from the start.

- `useradd` command syntax:Bash
    
    `sudo useradd [options] username`
    

**Key Options:**

- `m`: **M**ake a home directory for the user (e.g., `/home/username`).
- `c "Comment"`: Add a **c**omment, which is typically the user's full name.
- `s /path/to/shell`: **S**et the user's default login shell (e.g., `/bin/bash`).

**Example:** Let's create a user named `alex` with a home directory and the bash shell.

Bash

`sudo useradd -m -c "Alex Smith" -s /bin/bash alex`

### How to Set a Password

A new user account is locked until you set a password for it. The `passwd` command is used for this.

**Example:** Set the password for the new user `alex`.

Bash

`sudo passwd alex

# You will be prompted to enter and re-enter the new password.
# Enter new UNIX password:
# Retype new UNIX password:
# passwd: password updated successfully`

> Note: To change your own password, just type passwd without any username.
> 

### How to Switch to Another User

The `su` (**s**ubstitute **u**ser) command allows you to temporarily switch to another user's account.

**Example:** Switch from your current account to the `alex` account.

Bash

`# The '-' is important! It ensures you get the user's full environment (shell, path, etc.).
su - alex`

To return to your original user, simply type `exit`.

---

## Managing Groups

Groups are a convenient way to manage permissions for a collection of users at once. Instead of giving permissions to 10 individual users, you can give permissions to one group that all 10 users belong to.

### How to Create a Group

The `groupadd` command is used to create a new group.

**Example:** Create a new group called `developers`.

Bash

`sudo groupadd developers`

### How to Add a User to a Group

The `usermod` (**user** **mod**ify) command is used to change an existing user's properties, including their group memberships.

**Key Options:**

- `a`: **A**ppend. This adds the user to the new group without removing them from their current groups. **Forgetting `a` is a common mistake!**
- `G`: Specifies the secondary **G**roup(s) to add the user to.

**Example:** Add the user `alex` to the `developers` group.

Bash

`sudo usermod -aG developers alex`

You can verify the user's groups with the `groups` command: `groups alex`.

---

## Permissions with `sudo` and `visudo`

You should never log in as the root user for daily tasks. Instead, regular users can be granted temporary administrative powers using the `sudo` (**s**uper**u**ser **do**) command.

### `visudo` - The Right Way to Edit Permissions

The rules for who can use `sudo` are stored in the `/etc/sudoers` file. **You must never edit this file directly with a normal text editor.** A syntax error in this file could lock everyone, including you, out of administrative privileges.

The `visudo` command is the only safe way to edit this file. It opens the `sudoers` file in a text editor and performs a syntax check before saving. If it detects an error, it will not save the broken file.

**To use it, run:**

Bash

`sudo visudo`

### How to Grant `sudo` Privileges

When you run `sudo visudo`, you can add lines to grant permissions to users or groups.

**1. Granting `sudo` to a User**
To give a specific user (like `alex`) full administrative rights, add the following line at the end of the file:

`# User privilege specification
alex    ALL=(ALL:ALL) ALL`

**2. Granting `sudo` to a Group**
This is often the better approach. To give all members of the `developers` group full administrative rights, add this line. Note the `%` prefix, which indicates a group name.

`# Group privilege specification
%developers    ALL=(ALL:ALL) ALL`

After adding the line and saving the file, any user in the `developers` group can now run commands with `sudo` after entering their *own* password.