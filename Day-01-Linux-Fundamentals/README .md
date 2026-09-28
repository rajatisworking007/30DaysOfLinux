# 🐧 Day 01 — Linux Fundamentals

> **Goal:** Understand what Linux is, how a Linux system works, and learn the essential commands needed to start working in the terminal.

---

## 🎯 Learning Objectives

By the end of Day 01, you should understand:

- What Linux is
- What the Linux kernel does
- What a Linux distribution is
- Linux architecture
- What a terminal and shell are
- What Bash is
- Normal users vs `root`
- What `sudo` does
- Essential Linux commands
- How to use Linux documentation

---

# 1. 🐧 What is Linux?

Linux is an **open-source operating-system kernel**.

The kernel is the core component that manages system resources and communicates between software and hardware.

```text
Applications
      ↓
Shell / Utilities
      ↓
Linux Kernel
      ↓
Hardware
```

The kernel manages:

- CPU
- RAM
- Processes
- Filesystems
- Networking
- Hardware devices

---

# 2. 🧩 Linux vs Linux Distribution

**Linux** is the kernel.

A **Linux distribution** combines the Linux kernel with system utilities, libraries, package managers, applications, and other components.

Examples:

```text
Ubuntu
Debian
Fedora
Arch Linux
Kali Linux
Parrot OS
```

Conceptually:

```text
Linux Kernel
     +
System Utilities
     +
Package Manager
     +
Applications
     ↓
Linux Distribution
```

---

# 3. 🏗️ Linux Architecture

```text
┌──────────────────────┐
│     Applications     │
├──────────────────────┤
│    Shell / Tools     │
├──────────────────────┤
│    Linux Kernel      │
├──────────────────────┤
│      Hardware        │
└──────────────────────┘
```

### Hardware

CPU, RAM, storage, network card, USB devices, etc.

### Kernel

Controls and manages system resources.

### Shell

Provides an interface for interacting with the operating system.

### Applications

Programs such as Firefox, VS Code, Python, Git, and Nmap.

---

# 4. 💻 What is a Terminal?

A terminal is an interface where you enter commands.

For example:

```bash
whoami
```

Basic flow:

```text
You
 ↓
Terminal
 ↓
Shell
 ↓
Kernel
 ↓
System Resources / Hardware
```

The terminal itself is **not** the shell.

---

# 5. 🐚 What is a Shell?

A shell is a program that interprets commands and communicates with the operating system.

Common shells include:

- Bash
- Zsh
- Fish

Example:

```bash
echo "Hello Linux"
```

---

# 6. 🐚 What is Bash?

**Bash** stands for **Bourne Again SHell**.

Bash is both:

- A command interpreter
- A scripting language

Example:

```bash
#!/bin/bash

echo "System Information"
whoami
uname -a
```

Later in this course, Bash will be used to automate Linux tasks.

---

# 7. 👤 Users and Root

Linux is a multi-user operating system.

Check your current user:

```bash
whoami
```

Check user and group information:

```bash
id
```

Linux also has a special administrative account:

```text
root
```

Root has very high privileges.

Root normally has:

```text
uid=0
```

A normal user generally has a non-zero UID.

This privilege model is fundamental to Linux security.

---

# 8. 🔐 What is `sudo`?

`sudo` allows an authorized user to execute a command with elevated privileges.

Example:

```bash
sudo apt update
```

Conceptually:

```text
Normal User
     ↓
   sudo
     ↓
Elevated Privileges
```

Do not use `sudo` blindly. Understand the command first.

---

# 9. 💻 Essential Linux Commands

## `pwd`

**Print Working Directory**

```bash
pwd
```

Shows your current location.

Example:

```text
/home/user
```

---

## `ls`

Lists files and directories.

```bash
ls
```

Detailed listing:

```bash
ls -l
```

Show hidden files:

```bash
ls -a
```

Both:

```bash
ls -la
```

---

## `cd`

**Change Directory**

```bash
cd /tmp
```

Check your location:

```bash
pwd
```

Return home:

```bash
cd ~
```

or:

```bash
cd
```

---

## `whoami`

```bash
whoami
```

Shows the current username.

---

## `id`

```bash
id
```

Displays user and group information.

---

## `uname`

```bash
uname
```

Shows the kernel name.

More detailed:

```bash
uname -a
```

---

## `clear`

```bash
clear
```

Clears the terminal.

---

## `history`

```bash
history
```

Shows previously executed commands.

---

## `man`

`man` provides manual pages.

```bash
man ls
```

Exit with:

```text
q
```

You do not need to memorize every command. Learn how to find documentation.

---

# 10. 🧱 Understanding Command Structure

Linux commands commonly follow:

```text
command + options + arguments
```

Example:

```bash
ls -la /home
```

```text
ls       → command
-la      → options
/home    → argument
```

Another example:

```bash
mkdir test
```

```text
mkdir    → command
test     → argument
```

---

# 11. 🧪 Practical Lab

Run these commands yourself:

```bash
pwd
whoami
id
uname -a
ls
ls -la
cd /tmp
pwd
cd ~
pwd
history
```

Then identify your Linux distribution:

```bash
cat /etc/os-release
```

Find:

- Distribution name
- Distribution version
- Kernel information
- Current username
- Home directory

---

# 🔥 Day 01 Challenge

Complete these without copying the exact commands from the lesson.

### Challenge 1

Find your username.

### Challenge 2

Find your current directory.

### Challenge 3

Find your Linux distribution.

### Challenge 4

Find your kernel version.

### Challenge 5

Go to `/tmp`, verify your location, then return to your home directory.

### Challenge 6

Find the manual page for `ls`.

---

# 🧠 Knowledge Check

Try answering without searching:

1. What is Linux?
2. What is the Linux kernel?
3. What is a Linux distribution?
4. What is the difference between Linux and a distribution?
5. What is a terminal?
6. What is a shell?
7. What is Bash?
8. What does `pwd` do?
9. What does `ls` do?
10. What does `cd` do?
11. What does `whoami` do?
12. What does `uname -a` show?
13. What is `sudo`?
14. What is the difference between a normal user and root?
15. What does `man` do?

---

# 🛠️ Troubleshooting

If you see:

```text
command not found
```

try:

```bash
which <command>
```

and:

```bash
echo $PATH
```

For help:

```bash
<command> --help
```

Example:

```bash
ls --help
```

Or:

```bash
man <command>
```

---

# 📝 Key Takeaways

```text
Linux
 └── Kernel

Distribution
 ├── Linux Kernel
 ├── System Utilities
 ├── Package Manager
 └── Applications

Terminal
 └── Interface

Shell
 └── Command Interpreter

Bash
 └── Shell + Scripting Language

Root
 └── Administrative User

sudo
 └── Authorized elevated execution
```

---

# ✅ Completion Checklist

- [ ] Understand Linux vs Linux kernel
- [ ] Understand Linux distributions
- [ ] Understand Linux architecture
- [ ] Understand terminal vs shell
- [ ] Understand Bash
- [ ] Understand normal users vs root
- [ ] Understand `sudo`
- [ ] Practiced `pwd`
- [ ] Practiced `ls`
- [ ] Practiced `cd`
- [ ] Practiced `whoami`
- [ ] Practiced `id`
- [ ] Practiced `uname`
- [ ] Practiced `history`
- [ ] Practiced `man`
- [ ] Identified my Linux distribution
- [ ] Completed the Day 01 challenge
- [ ] Completed the knowledge check

---

# 🏆 Day 01 Complete

When everything above is complete, mark Day 01 in the main README:

```markdown
- [x] **Day 01 — Linux Fundamentals**
```

## ➡️ Next

[Day 02 — Linux Filesystem](../Day-02-Linux-Filesystem/)

---

<p align="center">

**Day 01 / 30**

🐧 **Learn → Practice → Break → Fix → Document**

</p>
