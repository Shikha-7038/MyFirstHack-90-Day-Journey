# Day 52 — Linux Users, Groups, Root & Sudo

## 📅 Day 52 of the MyFirstHack 90-Day Journey

## 🎯 Topic

**Linux Users, Groups, Root, Sudo, and Access Control**

---

## 1. Objective

Today's lesson focused on understanding **who Linux permissions apply to** and how Linux manages identities and privileges.

The main concepts covered were:

- Linux users and user identities
- User IDs (UIDs)
- Groups and Group IDs (GIDs)
- `/etc/passwd`
- `/etc/group`
- Root and administrative privileges
- `sudo` and controlled privilege elevation
- System and service accounts
- Least privilege
- Security investigation indicators related to users and groups

The overall access-control model can be understood as:

**User → Group → Permissions → Privileges**

---

## 2. Linux Users

Linux is designed as a **multi-user operating system**.

Every account has an identity represented by a **UID (User ID)**.

A Linux system can contain many accounts even when only one person uses the computer. Services, daemons, applications, and background processes may operate under separate accounts.

Using separate identities helps limit what each process or service can access and supports the security principle of **least privilege**.

A Linux user account is an identity; it does not necessarily represent a human.

There can be:

- Human or regular user accounts
- System accounts
- Service accounts

---

## 3. Linux Groups

A **group** is a collection of users that can share access to resources.

A user can belong to:

- One primary group
- Multiple supplementary groups

Groups make access management easier because permissions can be assigned to a group instead of configuring access separately for every user.

### Example

```text
project-team
├── User A
├── User B
└── User C
```

If a resource is assigned to the `project-team` group, its members can receive access according to the permissions assigned to that group.

### Security importance

Group membership is itself an access-control decision.

Membership in a powerful group can provide significant privileges, so unnecessary or unexpected group membership should be investigated.

---

## 4. UID and GID

Linux uses numerical identifiers to identify users and groups.

- **UID** = User ID
- **GID** = Group ID

The numbers are **identifiers, not positions in a list**.

GIDs do not have to be:

```text
1, 2, 3, 4, 5, 6...
```

There can be gaps because different system components and applications may have been assigned different identifiers.

For example:

```text
0
1
2
3
4
5
...
24
27
30
46
100
1000
```

A GID of `27` does **not** mean that the group is the 27th group. It simply identifies that particular group.

> **UID and GID values are identifiers, not rankings or sequence numbers.**

The `id` command can display a user's UID, primary GID, and supplementary group IDs.

---

## 5. `/etc/passwd`

`/etc/passwd` contains information about local user accounts.

A typical entry follows this structure:

```text
username:x:UID:GID:description:home:shell
```

### Fields

| Field | Meaning |
|---|---|
| Username | Name of the account |
| `x` | Placeholder indicating password information is stored separately |
| UID | User ID |
| GID | Primary Group ID |
| Description | User/account information |
| Home | User's home directory |
| Shell | User's login shell |

Example:

```text
user:x:1000:1000::/home/user:/bin/bash
```

### Password information

`/etc/passwd` does not normally contain the actual password hashes.

The `x` field indicates that password information is stored separately, normally in:

```text
/etc/shadow
```

---

## 6. Human Accounts vs System Accounts

A Linux system can contain many accounts that do not represent actual people.

### Human accounts

Accounts used by people to interact with the system.

### System/service accounts

Accounts used by:

- Services
- Daemons
- Background processes
- Applications

Using separate service accounts can help prevent every service from needing to operate with root-level privileges.

Many system accounts use a restricted shell such as:

```text
/usr/sbin/nologin
```

This indicates that the account is not intended for normal interactive login.

### Security relevance

During an investigation, it is important to distinguish expected system accounts from unexpected user accounts.

---

## 7. `/etc/group`

`/etc/group` contains information about local groups.

Its basic structure is:

```text
group_name:x:GID:members
```

### Fields

| Field | Meaning |
|---|---|
| Group name | Name of the group |
| `x` | Placeholder field |
| GID | Group ID |
| Members | Users who belong to the group |

Example:

```text
sudo:x:27:user
```

This indicates:

- Group name = `sudo`
- GID = `27`
- Member = `user`

The file can contain both regular groups and groups associated with system functions.

---

## 8. Root User

**Root** is the Linux superuser.

The root account has extremely powerful administrative privileges and can generally perform system-wide operations that ordinary users cannot.

The root account is identified by:

```text
UID 0
```

Root can generally:

- Modify system configuration
- Install or remove software
- Create or delete accounts
- Change ownership and permissions
- Modify protected files
- Perform administrative operations

### Why not work as root all the time?

Working continuously as root increases the potential impact of:

- Mistakes
- Incorrect commands
- Malicious software
- Compromised processes

A safer approach is to use an ordinary account and request elevated privileges only when necessary.

---

## 9. Root User vs Root Directory

The word **root** can refer to two different things.

### Root user

`root` is the superuser account.

### Root directory

`/` is the top-level directory of the Linux filesystem.

They are related by name but are **not the same thing**.

> `/` = root directory  
> `root` = root user

---

## 10. `sudo`

`sudo` provides a controlled way for an authorized user to execute a command with elevated privileges.

General model:

```text
Ordinary user
      ↓
     sudo
      ↓
Elevated privileges
      ↓
Specific command
```

After the command finishes, the user's normal identity remains unchanged.

Being allowed to use `sudo` does **not** mean the user is permanently root. It means the account is authorized to request elevated privileges according to the system's sudo configuration.

`sudo` is therefore an example of **controlled privilege elevation**.

---

## 11. The `sudo` Group

On Ubuntu, membership in the `sudo` group is commonly used to grant users permission to use `sudo`.

This makes the group security-sensitive.

An unnecessary or unexpected member of a privileged group could indicate:

- Excessive privileges
- Poor access control
- Misconfiguration
- Unauthorized access
- Possible attacker activity

### Security principle

> Privileged group membership should be granted only when it is actually required.

---

## 12. `whoami` vs `sudo whoami`

The difference between these commands demonstrates temporary privilege elevation.

### Normal command

```text
whoami
```

Reports the current user identity.

### With sudo

```text
sudo whoami
```

The command is executed with elevated privileges and normally reports:

```text
root
```

The important concept is:

```text
Normal session → ordinary user
Specific sudo command → elevated privileges
After command → ordinary user again
```

This is safer than operating with root privileges continuously.

---

## 13. Least Privilege

**Least privilege** means giving a user, process, service, or application only the privileges required to perform its legitimate tasks.

It applies to:

- Users
- Groups
- Processes
- Applications
- Services
- Administrators

### Why it matters

More unnecessary privileges can mean a larger potential impact if:

- A mistake occurs
- An account is compromised
- Malware executes
- A service is exploited

With least privilege:

```text
Required access only
        ↓
Smaller potential impact
```

---

## 14. Security Investigation Perspective

Users and groups can provide useful evidence during a Linux security investigation.

### 🚨 Unexpected user accounts

A newly created account that should not exist could indicate unauthorized access.

### 🚨 Unexpected privileged-group membership

A user unexpectedly added to a group such as `sudo` could indicate privilege escalation or unauthorized access.

### 🚨 Unnecessary administrative access

An existing user receiving administrative privileges without a legitimate reason could indicate excessive permissions or suspicious activity.

### 🚨 Changes to account or group configuration

Unexpected changes to users, groups, ownership, or permissions can help investigators understand what happened during a compromise.

---

## 15. Step 5 Reasoning

### Question 1
**Why is it safer to work as an ordinary user and use `sudo` when needed instead of working as root all the time?**

It is safer to work as an ordinary user because it limits what commands and processes can change. `sudo` provides elevated privileges only when they are needed for a specific administrative task. This reduces the potential damage caused by mistakes or malicious commands.

### Question 2
**On a company server, why would an investigator want to check the `sudo` group early during an investigation?**

An investigator should check the `sudo` group because its members are authorized to request elevated privileges. An unexpected user in this group could indicate excessive permissions, poor access control, misconfiguration, or possible attacker activity.

### Question 3
**If an attacker compromised a Linux system, what change involving users or groups might be a suspicious indicator?**

A suspicious indicator could be a newly created user account or an existing user unexpectedly added to a privileged group such as `sudo`. An attacker could use this to gain or maintain privileges they should not have.

---

## 16. Key Commands and Files

| Command/File | Purpose |
|---|---|
| `whoami` | Shows the current user |
| `id` | Shows UID, GID, and group membership information |
| `groups` | Shows groups associated with the current user |
| `cat /etc/passwd` | Displays local user-account information |
| `cat /etc/group` | Displays local group information |
| `sudo whoami` | Demonstrates command-level privilege elevation |

---

## 17. Key Takeaways

- Linux is designed to manage multiple identities.
- A **UID identifies a user**.
- A **GID identifies a group**.
- Users can belong to multiple groups.
- Group membership can provide access to resources.
- `/etc/passwd` contains local user-account information.
- `/etc/group` contains local group information.
- Many Linux accounts are system/service accounts rather than human accounts.
- **Root** is the superuser with powerful administrative privileges.
- **`sudo`** allows authorized users to request elevated privileges for specific commands.
- Being in the `sudo` group does not mean the user is permanently root.
- Working as an ordinary user and elevating privileges only when necessary supports **least privilege**.
- Unexpected users or privileged-group membership can be important security-investigation clues.

---

## 🔐 Final Security Insight

Linux access control is not only about **what permissions exist**.

It is also about:

> **Who is the user, which groups do they belong to, what privileges can they obtain, and do they actually need those privileges?**

Understanding users, groups, root, and `sudo` provides an important foundation for analyzing **access control, privilege escalation, and suspicious account activity**.