# Day 55 — Linux Pipes & Redirection

## 📌 Overview

Day 55 focused on one of the ideas that makes the Linux command line powerful: **combining simple commands to solve practical problems**.

Instead of relying on one command to perform every task, Linux provides small, focused commands that can be connected together using **pipes**.

I also learned how to use **output redirection** to save command results to files and the difference between overwriting and appending data.

These skills are especially useful in cybersecurity because security analysts often work with large amounts of logs, configuration data, and other system information that needs to be filtered and processed efficiently.

---

## 🎯 Objectives

By the end of this task, I learned how to:

- Understand the purpose of the pipe `|`
- Connect the output of one command to another command
- Use `wc -l` to count lines
- Combine `grep` and `wc`
- Understand command composition
- Use `>` for output redirection
- Use `>>` to append output
- Save search results into a file
- Understand how pipelines can help during security investigations

---

# 🔗 1. The Pipe `|`

A pipe connects two commands.

```bash
command1 | command2
```

The output of the first command becomes the input of the second command.

### Example

```bash
ls /etc | wc -l
```

Here:

1. `ls /etc` lists the contents of `/etc`
2. `|` sends that output to the next command
3. `wc -l` counts the lines

### My result

```text
167
```

This demonstrated that the output of one command can become the input for another command.

---

# 🔎 2. Combining `grep` and `wc`

I used:

```bash
grep "tcp" /etc/services | wc -l
```

The first command searches `/etc/services` for lines containing `tcp`.

The pipe sends those matching lines to `wc -l`.

`wc -l` then counts them.

### My result

```text
220
```

Without the pipe:

```bash
grep "tcp" /etc/services
```

the matching lines are displayed.

With the pipe:

```bash
grep "tcp" /etc/services | wc -l
```

the matching lines are counted.

This demonstrates how combining commands can answer a different question without needing a specialized command.

---

# 🧩 3. Command Composition

The Linux command line encourages the use of **small, focused tools**.

Instead of asking:

> Which single command can do everything?

A better approach is:

> What question am I trying to answer, and which small steps can I connect to answer it?

For example:

```text
Search → Filter → Count → Sort → Inspect
```

Each command performs a specific task.

This leads to an important idea:

> **Combination beats features.**

Simple tools can become powerful when they are connected together.

---

# 🛠️ 4. Useful Commands for Pipelines

Several commands can be combined to process information.

| Command | Purpose |
|---|---|
| `grep` | Search/filter lines |
| `wc` | Count lines, words, and characters |
| `wc -l` | Count lines |
| `sort` | Sort output |
| `uniq` | Remove adjacent duplicate lines |
| `head` | Display the first few lines |
| `tail` | Display the last few lines |

### Example

```bash
grep "error" app.log | wc -l
```

Counts lines containing `error`.

```bash
grep "error" app.log | sort | uniq
```

Finds error lines, sorts them, and removes adjacent duplicates.

```bash
grep "error" app.log | head
```

Displays the first few matching lines.

---

# 📁 5. Output Redirection

Normally, a command sends its output to the terminal.

Output redirection allows that output to be sent to a file instead.

The two operators covered today were:

```text
>   Overwrite
>>  Append
```

---

# ✏️ 6. `>` — Overwrite

Example:

```bash
ls /etc > etclist.txt
```

The output of `ls /etc` is saved into `etclist.txt`.

The output is not displayed on the terminal because it has been redirected to the file.

If the file already exists, `>` replaces its previous contents.

### Important

```text
> = overwrite/replace
```

Because it can overwrite existing data, it should be used carefully.

---

# ➕ 7. `>>` — Append

Example:

```bash
date >> record.txt
```

The output is added to the end of `record.txt`.

Existing content is preserved.

During the practical task, I first used:

```bash
date > record.txt
```

and then:

```bash
date >> record.txt
```

The file contained two different timestamps:

```text
Tue Sep 15 19:28:38 UTC 2026
Tue Sep 15 19:28:57 UTC 2026
```

This demonstrated the difference between replacing and appending.

### Important

```text
>> = append
```

---

# ⚖️ 8. `>` vs `>>`

| Operator | Action | Existing content |
|---|---|---|
| `>` | Writes output | Replaced |
| `>>` | Appends output | Preserved |

### Easy way to remember

**One arrow → replace**

**Two arrows → add**

---

# 🔍 9. Saving Search Results

I used redirection together with `grep`:

```bash
grep "https" /etc/services > findings.txt
```

This searched `/etc/services` for lines containing `https` and saved the results to `findings.txt`.

I then checked the saved results with:

```bash
cat findings.txt
```

The output included:

```text
https 443/tcp
https 443/udp
```

This demonstrates how command output can be captured and reviewed later.

---

# 🔄 10. Pipes + Redirection

Pipes and redirection can also be used together.

For example:

```bash
grep "failed" auth.log | wc -l > failed-count.txt
```

The process would be:

```text
auth.log
   ↓
grep "failed"
   ↓
matching lines
   ↓
wc -l
   ↓
number of matches
   ↓
failed-count.txt
```

This allows a command pipeline to process information and then save the final result.

---

# ⌨️ 11. Understanding Command Input

I also tested:

```bash
grep "failed" | wc -l
```

Because I did not provide a file to `grep`, it waited for input from the terminal.

This helped me understand that commands can receive input from different sources.

A command can receive input from:

- A file
- The keyboard/terminal
- Another command through a pipe

I stopped the waiting command safely using:

```text
Ctrl+C
```

This was a useful practical observation about command input and standard input.

---

# 🔐 12. Cybersecurity Connection

Pipes are useful during cybersecurity investigations because analysts frequently work with large amounts of information.

For example, a log file may contain thousands of entries.

Instead of manually reading everything, an analyst can build a pipeline:

```text
Search
   ↓
Filter
   ↓
Count
   ↓
Sort
   ↓
Remove duplicates
   ↓
Inspect
```

This helps reduce noise and focus on relevant evidence.

For example:

```bash
grep "failed" auth.log | wc -l
```

could help determine how many log lines contain a particular keyword.

The important skill is not simply knowing commands. It is knowing **how to combine commands to answer a specific investigation question**.

---

# 🧠 13. Investigator Mindset

Today's lesson reinforced an important investigation workflow:

### 1. Start with a question

What information am I trying to find?

### 2. Break the question into smaller steps

Search → filter → count → organize → inspect.

### 3. Choose simple tools

Use commands that each perform one clear job.

### 4. Connect the tools

Use pipes to pass information between commands.

### 5. Save useful findings

Use redirection when the output needs to be preserved.

---

# 🔗 14. Connection to Previous Days

Day 55 builds directly on the Linux skills learned earlier:

| Day | Skill |
|---|---|
| Day 48 | Linux filesystem |
| Day 49 | Navigation |
| Day 50 | Navigation practice |
| Day 51 | File permissions |
| Day 52 | Users, groups, root and sudo |
| Day 53 | Reading and filtering files |
| Day 54 | Finding files |
| **Day 55** | **Pipes and redirection** |

The progression is:

```text
Where are things?
       ↓
How do I navigate there?
       ↓
Who can access them?
       ↓
What's inside?
       ↓
Where can I find something?
       ↓
How can I combine tools to investigate efficiently?
```

---

# 🧪 15. Practical Task Summary

### Count `/etc` output

```bash
ls /etc | wc -l
```

Result:

```text
167
```

### Count `tcp` lines

```bash
grep "tcp" /etc/services | wc -l
```

Result:

```text
220
```

### Test overwrite

```bash
date > record.txt
```

### Test append

```bash
date >> record.txt
```

Result: Two timestamps were stored in the same file.

### Save HTTPS search results

```bash
grep "https" /etc/services > findings.txt
```

Then:

```bash
cat findings.txt
```

### Clean up practice files

```bash
rm etclist.txt record.txt findings.txt
```

---

# 💡 Key Learnings

- `|` connects commands.
- The output of one command can become the input of another.
- `grep` can filter information before another command processes it.
- `wc -l` counts lines.
- `>` redirects output and overwrites existing file contents.
- `>>` redirects output and appends to existing contents.
- Pipes allow small commands to be combined into useful workflows.
- Redirection allows useful output to be saved for later analysis.
- A command waiting for input is not necessarily broken; it may simply be waiting for stdin.
- Linux command-line efficiency comes from **composition**, not from trying to memorize one command for every task.

---

## 🧠 Final Takeaway

> **The command line isn't about knowing every command. It's about knowing how to make simple commands work together.**

Day 55 helped me move from simply learning individual Linux commands to thinking about how those commands can be connected to solve real questions.

This is an important step toward using Linux as an investigation tool in cybersecurity.