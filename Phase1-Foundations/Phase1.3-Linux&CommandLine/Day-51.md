# Day 51 — Linux File Permissions

## 📅 MyFirstHack 90-Day Journey

**Day:** 51  
**Phase:** Linux  
**Topic:** Linux File Permissions  
**Focus:** Reading, understanding, and changing Linux permissions

---

## 🎯 Objective

The goal of Day 51 was to understand how Linux controls access to files and directories using permissions.

I learned how to:

- Read permission strings using `ls -l`
- Understand `r`, `w`, and `x`
- Understand permissions for the owner, group, and others
- Distinguish regular files, directories, and symbolic links
- Change permissions using `chmod`
- Understand numeric permissions such as `600`, `644`, and `755`
- Understand file ownership with `chown`
- Understand the role of `sudo`
- Connect Linux permissions with the cybersecurity principle of least privilege

---

## 1. Understanding Linux Permissions

Linux permissions determine:

> **Who can access a file or directory and what they are allowed to do with it.**

The three basic permissions are:

| Symbol | Permission | Meaning for a regular file |
|---|---|---|
| `r` | Read | Read the file contents |
| `w` | Write | Modify the file contents |
| `x` | Execute | Run the file as a program/script |
| `-` | No permission | Permission is not granted |

Linux applies these permissions to three categories:

| Category | Meaning |
|---|---|
| User / Owner | The user who owns the file |
| Group | Users belonging to the file's group |
| Others | Everyone else |

---

## 2. Reading `ls -l` Output

The command:

```bash
ls -l
```

displays detailed information about files and directories.

Example:

```text
-rwxr-xr--
```

This can be divided into:

```text
-rwx r-x r--
│    │   │
│    │   └── Others
│    └────── Group
└─────────── Owner
```

The first character represents the file type.

### Common file types

- `-` → Regular file
- `d` → Directory
- `l` → Symbolic link

For:

```text
-rwxr-xr--
```

the permissions mean:

- Owner → `rwx` → read, write, execute
- Group → `r-x` → read and execute
- Others → `r--` → read only

---

## 3. Observing `/bin` on Ubuntu

I ran:

```bash
ls -l /bin
```

My Ubuntu/WSL system returned:

```text
lrwxrwxrwx 1 root root 7 Apr 20 08:46 /bin -> usr/bin
```

The first character is `l`, which means `/bin` is a **symbolic link** to `/usr/bin`.

To inspect the contents rather than the link itself, I used:

```bash
ls -l /bin/ | head
```

This displayed entries inside `/bin`, which points to `/usr/bin` on my system.

One regular file I observed was:

```text
-rwxr-xr-x   1 root root 14720 Apr 8 17:26 aa-enabled
```

Its permissions are:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

Therefore, the owner can read, modify, and execute it, while group and other users can read and execute it but cannot write to it.

---

## 4. File Permissions vs Directory Permissions

The meaning of permissions changes slightly for directories.

### Regular files

| Permission | Meaning |
|---|---|
| `r` | Read contents |
| `w` | Modify contents |
| `x` | Execute the file |

### Directories

| Permission | Meaning |
|---|---|
| `r` | List directory contents |
| `w` | Create/delete entries |
| `x` | Enter/traverse the directory |

Execute permission therefore has a different role on a directory than on a regular file.

---

## 5. Changing Permissions with `chmod`

`chmod` is used to change file permissions.

### Symbolic method

```bash
chmod u+x file
```

Adds execute permission for the user/owner.

```bash
chmod o-r file
```

Removes read permission from others.

```bash
chmod g+w file
```

Adds write permission for the group.

The main symbols are:

```text
u = user/owner
g = group
o = others
```

Operators:

```text
+ = add permission
- = remove permission
```

---

## 6. Numeric Permissions

Linux also represents permissions using numbers:

```text
r = 4
w = 2
x = 1
```

The values are added together.

| Number | Permission |
|---:|---|
| `7` | `rwx` |
| `6` | `rw-` |
| `5` | `r-x` |
| `4` | `r--` |
| `0` | `---` |

### Common examples

```bash
chmod 755 file
```

gives:

```text
rwxr-xr-x
```

```bash
chmod 644 file
```

gives:

```text
rw-r--r--
```

```bash
chmod 600 file
```

gives:

```text
rw-------
```

---

## 7. Why `600` Can Be Used for Private Files

For a file containing sensitive information, such as a private password file:

```bash
chmod 600 password.txt
```

gives:

```text
Owner  → Read + Write
Group  → No access
Others → No access
```

A password data file normally does not need execute permission because execute permission on a regular file means allowing it to be run as a program or script.

This demonstrates the **least privilege** principle: give only the permissions that are actually needed.

---

## 8. `chmod` vs `chown`

### `chmod`

Changes **what permissions** a file has.

```bash
chmod 600 file.txt
```

Think:

> **What can users do with this file?**

### `chown`

Changes **who owns** the file.

```bash
chown user file.txt
```

Think:

> **Who owns this file?**

Ownership changes generally require appropriate administrative privileges.

---

## 9. Understanding `sudo`

`sudo` allows an authorized user to run a command with elevated privileges.

Examples:

```bash
sudo chmod 600 file.txt
```

```bash
sudo chown user file.txt
```

`sudo` is a separate command. It is not part of `chmod` or `chown`.

---

## 10. Hands-on Practice

I practiced permissions using a test file in my home directory.

### Create the test file

```bash
cd ~
touch testfile
ls -l testfile
```

The exact default permissions can vary depending on the system's `umask`, so I checked the permissions shown by my own terminal.

### Symbolic permission changes

```bash
chmod o-r testfile
ls -l testfile

chmod u+x testfile
ls -l testfile

chmod g+w testfile
ls -l testfile
```

These commands demonstrated how individual permissions can be added or removed.

### Numeric permission changes

```bash
chmod 644 testfile
ls -l testfile

chmod 600 testfile
ls -l testfile

chmod 755 testfile
ls -l testfile
```

I observed how the permission string changed after each command.

### Cleanup

```bash
rm testfile
```

---

## 11. Cybersecurity Connection

Linux permissions are an important part of access control.

Incorrect permissions can expose sensitive information or allow unauthorized modification.

Examples include:

- Sensitive configuration files readable by everyone
- Private keys accessible to other users
- Privileged scripts writable by untrusted users
- Sensitive files with excessive permissions

The goal is not to give everyone maximum access.

The goal is:

> **Give each user only the permissions they actually need.**

This is the principle of **least privilege**.

---

## 12. Key Takeaways

1. Linux permissions control access to files and directories.
2. `r`, `w`, and `x` represent read, write, and execute.
3. Permissions are assigned to the owner, group, and others.
4. `ls -l` is used to inspect permissions.
5. The first character of the permission string indicates the file type.
6. `/bin` on my Ubuntu system is a symbolic link to `/usr/bin`.
7. `chmod` changes permissions.
8. `chown` changes ownership.
9. `sudo` can provide authorized elevated privileges.
10. File and directory permissions have different meanings.
11. Numeric permissions use `4` for read, `2` for write, and `1` for execute.
12. `600` can be appropriate for private files that should only be accessible by their owner.
13. Execute permission on a regular file means it can be run as a program/script.
14. Linux permissions are a practical example of **least privilege**.

---

## 💡 Personal Learning Reflection

Day 51 helped me understand that Linux permissions are more than a collection of letters and numbers.

A string such as:

```text
-rwxr-xr--
```

contains information about **who can access a file and what they can do with it**.

The biggest takeaway for me was the connection between Linux permissions and cybersecurity:

> **Security is not about giving everyone access or blocking everyone. It is about giving the right users the right level of access.**

This is a practical example of the **least privilege principle**, an important concept in cybersecurity.

---

## 🛠️ Commands Practiced

```bash
ls -l
ls -l /bin
ls -l /bin/ | head
ls -l /etc

cd ~
touch testfile

chmod o-r testfile
chmod u+x testfile
chmod g+w testfile

chmod 644 testfile
chmod 600 testfile
chmod 755 testfile

rm testfile
```

---

**Progress: Day 51/90 ✅**  
**Days Remaining: 39**
