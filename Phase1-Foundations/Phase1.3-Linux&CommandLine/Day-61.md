# Day 61 --- Linux Shell Scripting

## Overview

Day 61 focused on moving from using Linux commands individually to
combining them into a reusable Bash script. The practical work
demonstrated scripting, execute permissions, variables, command
substitution, automation, and the security relevance of scripts.

## Learning Objectives

-   Understand what a shell script is.
-   Learn the basic structure of a Bash script.
-   Understand the shebang, comments, commands, and execute permission.
-   Use variables and command substitution.
-   Understand conditions and loops.
-   Understand scripting as automation.
-   Understand defensive and malicious uses of scripts.
-   Connect scripting with Linux permissions and suspicious-script
    analysis.

## What Is a Shell Script?

A shell script is a text file containing a sequence of commands that can
be executed automatically.

Shell scripts can automate repetitive tasks, gather system information,
perform routine checks, process information, support security
investigations, and help build small security tools.

## Structure of a Bash Script

### Shebang

The shebang identifies the interpreter used to execute the script.

``` bash
#!/bin/bash
```

### Comments

Comments begin with `#` and are ignored by the shell during execution.
They explain the purpose or logic of a script.

### Commands

Commands are normally executed from top to bottom.

``` bash
echo "System information:"
date
whoami
```

### Execute Permission

A newly created script is normally a text file. To run it directly, it
needs the execute (`x`) permission.

``` bash
chmod +x script.sh
```

This connects scripting directly with Linux file permissions.

## Variables

Variables provide named storage for values that can be reused.

``` bash
filename="notes.txt"
echo "$filename"
```

Variables make scripts more flexible because information can be stored
once and reused.

## Command Substitution

Command substitution captures the output of a command so it can be
stored or reused.

``` bash
today=$(date)
echo "Today is $today"
```

## Conditions

Conditions allow a script to make decisions.

``` bash
if [ -f "notes.txt" ]; then
    echo "File exists"
fi
```

## Loops

Loops allow a script to repeat an action for multiple items.

``` bash
for file in *.log
do
    echo "$file"
done
```

## From Commands to Automation

The progression is:

**Commands → Scripts → Variables → Conditions and Loops → Automation**

Individual commands perform actions. Scripts combine commands into
reusable sequences. Variables store and reuse information. Conditions
allow decisions, and loops allow repetition.

## Scripts in Cybersecurity

### Defensive Uses

-   System information collection
-   Repetitive security checks
-   Evidence gathering
-   Log processing
-   Monitoring
-   Routine security tasks

### Threat Uses

Attackers can use scripts to automate malicious actions, modify systems,
establish persistence, execute unwanted commands, and perform repeated
actions.

Scripts are therefore dual-use tools. Their purpose depends on what
their commands and logic are designed to do.

## Understanding Suspicious Scripts

Understanding legitimate scripts helps security analysts examine
unfamiliar scripts.

Important elements include:

-   Shebang and interpreter
-   Commands being executed
-   Variables
-   Conditions
-   Loops
-   File permissions
-   Files and system resources being accessed
-   Actions performed by the script

A script should be understood by examining what its commands actually do
rather than judging it only by its filename.

# Day 61 Task --- Write Your First Script

The practical task was to create a harmless Bash script named
`sysinfo.sh`.

The script gathered basic system information:

-   Current date and time
-   Current logged-in user
-   Current working directory

It also stored the output of `pwd` in a variable named `location`.

The script content was:

``` bash
#!/bin/bash
# sysinfo.sh - a simple system information script

echo "=== System Information ==="
echo "Date:"
date

echo "Logged in as:"
whoami

location=$(pwd)
echo "Current directory: $location"

echo "=== End of report ==="
```

## Creating the Script

The file was created using:

``` bash
nano sysinfo.sh
```

## Execution Before Permission Change

The first attempt to run the script was:

``` bash
./sysinfo.sh
```

The result was:

``` text
-bash: ./sysinfo.sh: Permission denied
```

The script existed, but it did not have execute permission.

## Adding Execute Permission

Execute permission was added:

``` bash
chmod +x sysinfo.sh
```

The file permissions were checked:

``` bash
ls -l sysinfo.sh
```

Observed result:

``` text
-rwxr-xr-x 1 shikha shikha 223 Sep 22 06:44 sysinfo.sh
```

The `x` characters confirmed that execute permission had been added.

## Running the Script

The script was then executed successfully:

``` bash
./sysinfo.sh
```

It printed a system information report containing the date and time,
logged-in user, current directory, and closing message.

The script was run a second time successfully, demonstrating that the
same process could be repeated without manually entering each command.

## Understanding the Variable

The script used:

``` bash
location=$(pwd)
```

`pwd` produced the current working directory. Command substitution
captured that output and stored it in `location`.

The value was then retrieved using:

``` bash
echo "Current directory: $location"
```

# Reflection and Reasoning

## Execute Permission

The execute permission was the missing piece between having a text file
containing Bash commands and being able to run the file directly.

Before `chmod +x`, Linux returned `Permission denied`. After the execute
permission was added, `./sysinfo.sh` executed successfully.

## Repetitive Task to Automate

A useful cybersecurity example would be a basic system-security check
that collects system information, running processes, network
connections, recent login activity, and relevant logs. A script could
perform these checks consistently instead of requiring every command to
be entered manually.

## Connection to Day 56

Writing a harmless script makes the structure of a suspicious script
easier to understand. The analyst can recognize the interpreter,
commands, variables, conditions, loops, permissions, and system
resources being accessed.

On Day 56, the suspicious script was analyzed without execution. On Day
61, a known benign script was created and safely executed. Understanding
both situations helps distinguish script structure from script intent.

# Cybersecurity Connection

Shell scripts can support defensive activities such as system checks,
evidence collection, log processing, monitoring, and automation.

The same capability can be misused to automate unwanted commands, modify
systems, establish persistence, or perform malicious actions.

The safety of a script depends on what its commands and logic actually
do.

# Connections to Previous Days

**Day 51 --- Linux Permissions:** The `x` permission was applied to a
script so it could be executed directly.

**Day 55 --- Pipes and Redirection:** Earlier command-line skills
provide building blocks that can be incorporated into scripts.

**Day 56 --- Suspicious Script Investigation:** Script structure and
commands can be examined to understand behavior without blindly
executing an unknown file.

**Days 57--59 --- Processes, Network, and Logs:** Information learned
from these areas can later be collected or processed through scripts.

**Day 60 --- Software Management:** The Linux phase progressed from
using and maintaining tools toward creating repeatable tools.

# Key Takeaways

-   A shell script is a text file containing commands that can be
    executed as a sequence.
-   The shebang identifies the interpreter.
-   Commands normally execute from top to bottom.
-   Comments explain scripts and are ignored during execution.
-   A script needs execute permission to run directly.
-   `chmod +x` adds execute permission.
-   Variables store values for reuse.
-   Command substitution captures command output.
-   Conditions allow decisions.
-   Loops allow repetition.
-   Scripting turns commands into reusable and repeatable processes.
-   Scripts can support defensive cybersecurity automation.
-   Scripts can also be used maliciously.
-   Understanding benign scripts helps analysts understand suspicious
    scripts.
-   Shell scripting is a step from using command-line tools toward
    building with them.

## Day 61 Progress

**61 days completed --- 29 days remaining.**
