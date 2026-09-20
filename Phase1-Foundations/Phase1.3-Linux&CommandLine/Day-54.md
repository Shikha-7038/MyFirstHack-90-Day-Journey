# Day 54 — Finding Files in Linux 🔎

## 📌 Overview

Today I learned how to search for files and directories in Linux using the `find` command.

At first, finding a file may seem like a simple task. But in cybersecurity, file searching can become an important part of an investigation. An analyst may need to determine:

- Where a file is located
- What type of file it is
- What files were modified recently
- How large a file is
- What permissions a file has
- Which user owns a file

I also learned how `find` differs from `locate` and why the starting directory matters when performing a search.

---

## 🔎 The `find` Command

The `find` command searches the Linux filesystem tree for files and directories that match specific criteria.

### Basic syntax

```bash
find [starting_directory] [criteria]
```

The **starting directory** determines where the search begins.

### Search the entire filesystem

```bash
find /
```

- `/` represents the root of the filesystem.
- This searches across the entire system.
- It can be slower because there may be a large number of files and directories to examine.

### Search from the current directory

```bash
find .
```

- `.` represents the current directory.
- The search begins from the directory where I am currently located.
- This is generally faster than searching the entire filesystem.

### Key idea

> The broader the starting location, the more the command may need to search.

---

## 📁 Search by File Name

The `-name` option searches for files using their name.

### Exact filename

```bash
find ~ -name "findme.txt"
```

This searches the home directory for a file named:

```text
findme.txt
```

### Search using a pattern

```bash
find /home -name "*.log"
```

The `*` wildcard means **anything**.

Therefore, this can match files such as:

```text
notes.log
system.log
error.log
```

The command searches for `.log` files anywhere under `/home`.

---

## 🗂️ Search by File Type

The `-type` option allows the search to be restricted to a particular type of filesystem object.

### Find regular files

```bash
find ~ -type f
```

`f` means **regular file**.

### Find directories

```bash
find ~ -type d
```

`d` means **directory**.

Some common file types include:

| Option | Meaning |
|---|---|
| `-type f` | Regular file |
| `-type d` | Directory |
| `-type l` | Symbolic link |

---

## ⏱️ Search by Modification Time

The `-mtime` option searches based on when a file or directory was last modified.

### Find items modified within the last day

```bash
find / -mtime -1
```

This searches for items modified within approximately the last **24 hours**.

This is particularly useful in security investigations because one important question is:

> **What changed recently?**

Recently modified files can provide useful leads when investigating a potentially compromised system.

### Find items modified more than 7 days ago

```bash
find ~ -mtime +7
```

This searches for items whose modification time is more than seven days old.

---

## 📦 Search by File Size

The `-size` option allows files to be searched according to their size.

### Find large files

```bash
find / -size +100M
```

This searches for files larger than 100 MB.

### Find empty files

```bash
find / -size 0
```

This searches for files with a size of zero.

In a security investigation, unexpectedly large or empty files can be worth examining further.

---

## 🔐 Search by Permissions

The `-perm` option searches for files based on their permission settings.

### Example

```bash
find / -perm 777
```

This searches for files with `777` permissions.

This can help identify files with potentially dangerous or overly permissive access settings.

---

## 👤 Search by User

The `-user` option searches for files owned by a specific user.

### Example

```bash
find / -user suspicioususer
```

This searches for files owned by `suspicioususer`.

In an investigation, this can help identify files associated with a particular or suspicious account.

---

## 🧩 Combining Criteria

The real power of `find` comes from combining multiple search criteria.

For example:

```bash
find / -type f -name "*.log" -mtime -1
```

This searches for:

- Regular files
- Ending in `.log`
- Modified within the last day

Instead of searching for everything, I can describe exactly what I want to find.

### Investigation mindset

```text
Starting location
        +
Search criteria
        +
Additional criteria
        =
Precise search
```

This makes `find` more than just a file-search command. It can become an **investigative tool** for narrowing down evidence on a system.

---

## ⚡ `find` vs `locate`

I also learned the difference between `find` and `locate`.

### `find`

- Searches the filesystem directly.
- Reflects the current state of the filesystem.
- Supports many different search criteria.
- Useful when looking for recent changes.

### `locate`

- Searches a pre-built database of file paths.
- Is generally very fast.
- The database may not immediately contain newly created or recently changed files.

### Simple comparison

```text
find   → Check the filesystem now
locate → Search a stored file index
```

During my hands-on practice, `locate` was not installed in my Ubuntu environment, so I continued using `find`.

---

## 🧪 Hands-On Practice

I created two temporary files for testing:

```bash
touch ~/findme.txt
touch ~/notes.log
```

### Finding the test file

```bash
find ~ -name "findme.txt"
```

Result:

```text
/home/shikha/findme.txt
```

### Finding `.log` files

```bash
find ~ -name "*.log"
```

This returned my test file along with another existing `.log` file.

### Finding directories

```bash
find ~ -type d
```

This displayed directories under my home directory.

### Finding regular files

```bash
find ~ -type f
```

This displayed regular files under my home directory.

### Finding recently modified items

```bash
find ~ -mtime -1
```

This displayed items modified within the previous day, including my test files and other recently changed system/user files.

This was a useful reminder that **recently modified does not automatically mean suspicious**. It simply gives an investigator something that may deserve further examination.

### Searching `/tmp`

```bash
find /tmp -type f
```

Some protected directories returned:

```text
Permission denied
```

This was caused by access restrictions on those directories rather than an incorrect `find` command.

### Cleaning up

After completing the practice, I removed the temporary files:

```bash
rm ~/findme.txt ~/notes.log
```

---

## 🛡️ Cybersecurity Relevance

File searching can be useful during security investigations.

For example, an analyst might ask:

```text
What changed recently?
        ↓
Which files were modified?
        ↓
Are any of them unusual?
        ↓
Who owns them?
        ↓
What permissions do they have?
        ↓
Do multiple clues point to the same file?
```

Commands such as `find` allow these questions to be converted into targeted searches.

---

## 💡 What I Learned

The most important lesson from today was not simply memorizing `find` options.

It was learning to **search systematically**.

Instead of looking everywhere randomly:

> **Start with what you know → define what you are looking for → choose the right criteria → examine the results → follow the clues.**

This way of thinking is useful beyond Linux commands. It is also an important mindset for cybersecurity investigations.

---

## 🧠 Quick Reference

| Option | Purpose | Example |
|---|---|---|
| `-name` | Search by name/pattern | `find ~ -name "*.log"` |
| `-type f` | Find regular files | `find ~ -type f` |
| `-type d` | Find directories | `find ~ -type d` |
| `-mtime` | Search by modification time | `find ~ -mtime -1` |
| `-size` | Search by file size | `find / -size +100M` |
| `-perm` | Search by permissions | `find / -perm 777` |
| `-user` | Search by owner | `find / -user suspicioususer` |

### 🔑 Key Takeaway

> **`find` turns a broad filesystem search into a precise investigation by letting you describe exactly what you are looking for.**

---

**Day 54/90 — Linux Command Line Phase 🔐**