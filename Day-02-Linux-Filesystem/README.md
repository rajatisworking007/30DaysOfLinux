# 🐧 Day 02 — Linux Filesystem

> **30 Days of Linux — Day 02**  
> Learn how Linux organizes files, directories, users, configuration, devices, processes, and system data.

## 🎯 Learning Objectives

By the end of Day 02, you should be able to:

- Understand the Linux filesystem hierarchy.
- Explain what `/` means.
- Navigate using absolute and relative paths.
- Understand `~`, `.` and `..`.
- Understand important directories such as `/home`, `/etc`, `/var`, `/tmp`, `/usr`, `/dev`, `/proc` and `/sys`.
- Find hidden files.
- Identify files with `file`.
- Inspect metadata with `stat`.
- Navigate Linux without getting lost.
- Explain why filesystem knowledge matters in cybersecurity.

---

# 1. What Is the Linux Filesystem?

Linux organizes files and directories in a **hierarchical tree structure**.

Unlike Windows, where you commonly see:

```text
C:\
D:\
E:\
```

Linux starts with a single filesystem root:

```text
/
```

A simplified structure:

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── user
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

Everything on the Linux system exists somewhere under `/`.

---

# 2. `/` — The Filesystem Root

The `/` directory is the starting point of the filesystem.

Try:

```bash
cd /
pwd
```

Expected:

```text
/
```

Then:

```bash
ls
```

You will see directories similar to:

```text
bin
boot
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

For example:

```bash
cat /etc/passwd
```

means:

```text
/
└── etc
    └── passwd
```

---

# 3. `/` vs `/root`

Do not confuse these.

```text
/       → filesystem root
/root   → root user's home directory
```

For example:

```bash
cd /
```

takes you to the filesystem root.

```bash
cd /root
```

attempts to enter the root user's home directory.

The root **directory** and root **user** are different concepts.

---

# 4. `/home` — Normal Users

Normal users usually have personal directories under `/home`.

Example:

```text
/home
├── rajat
├── alice
└── bob
```

Check:

```bash
ls /home
```

Your home directory can be checked with:

```bash
echo $HOME
```

Example:

```text
/home/rajat
```

---

# 5. `~` — Home Directory Shortcut

The symbol `~` represents the current user's home directory.

```bash
cd ~
pwd
```

If your username is `rajat`, you may see:

```text
/home/rajat
```

So:

```bash
cd ~
```

and:

```bash
cd /home/rajat
```

can reach the same location.

---

# 6. `/etc` — Configuration

`/etc` contains system and application configuration files.

Explore it:

```bash
ls /etc
```

Important examples include:

```text
/etc/passwd
/etc/shadow
/etc/hosts
/etc/hostname
/etc/os-release
/etc/ssh/
```

Check your Linux distribution:

```bash
cat /etc/os-release
```

The exact output depends on your distribution.

### Example

```text
PRETTY_NAME="Parrot OS"
NAME="Parrot Security"
```

---

# 7. `/etc/passwd`

You will study users and groups later, but recognize this file now:

```bash
cat /etc/passwd
```

A line may look like:

```text
root:x:0:0:root:/root:/bin/bash
```

Fields are separated by `:`.

Conceptually:

```text
username : password-field : UID : GID : description : home : shell
```

For now, remember:

```text
/etc/passwd → user account information
```

---

# 8. `/var` — Variable Data

`/var` contains data that changes frequently while the system operates.

Explore:

```bash
ls /var
```

Important locations include:

```text
/var/log
/var/cache
/var/lib
```

---

# 9. `/var/log` — Logs

System and application logs are commonly stored under:

```text
/var/log
```

Explore:

```bash
ls /var/log
```

Depending on your distribution, you may see files such as:

```text
syslog
auth.log
kern.log
```

Not every Linux distribution uses the same files.

Example:

```bash
head /var/log/auth.log
```

If the file does not exist, your distribution may use a different logging system.

### Cybersecurity connection

Logs can help answer:

```text
Who logged in?
What happened?
When did it happen?
Which service generated an event?
```

---

# 10. `/tmp` — Temporary Files

`/tmp` is commonly used for temporary data.

```bash
cd /tmp
pwd
```

Expected:

```text
/tmp
```

List its contents:

```bash
ls -la
```

Create a test file:

```bash
touch linux-test.txt
```

Check it:

```bash
ls -l linux-test.txt
```

Remove it:

```bash
rm linux-test.txt
```

### Security connection

`/tmp` can be useful during security investigations because applications and users may create temporary files there.

A file in `/tmp` is **not automatically malicious**. Always investigate context, owner, permissions, timestamps and contents.

---

# 11. `/usr` — Programs and Resources

`/usr` contains a large portion of user-space programs and resources.

Explore:

```bash
ls /usr
```

Important locations:

```text
/usr/bin
/usr/sbin
/usr/lib
/usr/share
```

Example:

```bash
ls /usr/bin | head
```

---

# 12. `/bin` — Essential Commands

Traditionally, `/bin` contains essential executable commands.

```bash
ls /bin
```

On many modern Linux distributions, `/bin` may be a symbolic link to `/usr/bin`.

Check:

```bash
ls -ld /bin
```

You may see:

```text
/bin -> usr/bin
```

---

# 13. `/sbin` — System Administration Programs

Traditionally, `/sbin` contains system administration programs.

```bash
ls /sbin
```

Modern distributions may merge these into `/usr/sbin`.

---

# 14. `/boot` — Boot Files

`/boot` contains files involved in booting the operating system.

```bash
ls /boot
```

Depending on your system, you may find kernel, initramfs and bootloader-related files.

Avoid modifying `/boot` casually.

---

# 15. `/dev` — Device Files

Linux represents many devices through filesystem interfaces.

Explore:

```bash
ls /dev
```

You may see:

```text
null
zero
random
urandom
tty
```

### `/dev/null`

`/dev/null` discards data.

```bash
echo "hello" > /dev/null
```

Nothing is displayed.

This is commonly used in shell scripts and commands.

---

# 16. `/proc` — Processes and Kernel Information

`/proc` is a **virtual filesystem**.

```bash
ls /proc
```

You may see numbered directories:

```text
1
2
3
...
```

These numbers correspond to process IDs (PIDs).

Try:

```bash
ls /proc/1
```

System information is also exposed:

```bash
cat /proc/cpuinfo
```

```bash
cat /proc/meminfo
```

```bash
cat /proc/version
```

Much of `/proc` is generated dynamically by the Linux kernel rather than being ordinary files stored on disk.

---

# 17. `/sys` — Hardware and Kernel Information

`/sys` is another virtual filesystem.

```bash
ls /sys
```

It exposes information related to:

- hardware
- devices
- drivers
- kernel subsystems

Remember:

```text
/proc → processes + kernel information
/sys  → hardware + devices + kernel information
```

---

# 18. `/run` — Runtime Data

`/run` contains runtime information created after boot.

```bash
ls /run
```

It may contain information associated with:

- system services
- users
- locks
- runtime state

The exact contents depend on the system.

---

# 19. `/media`

Desktop Linux systems commonly use `/media` for removable media such as:

- USB drives
- external storage
- CD/DVD media

---

# 20. `/mnt`

`/mnt` is traditionally used as a temporary mount point.

For now:

```text
/mnt → common mount point
```

Storage and mounting will be covered later.

---

# 21. `/opt`

`/opt` is commonly used for optional or third-party software.

Example:

```text
/opt/my-application
```

---

# 22. `/srv`

`/srv` can contain data provided by system services.

For example:

```text
/srv
```

may be used by server applications.

---

# 23. Filesystem Cheat Sheet

| Directory | Common Purpose |
|---|---|
| `/` | Filesystem root |
| `/home` | Normal user home directories |
| `/root` | Root user's home |
| `/etc` | Configuration |
| `/var` | Variable data |
| `/var/log` | Logs |
| `/tmp` | Temporary files |
| `/usr` | Programs and resources |
| `/bin` | Essential commands |
| `/sbin` | System administration commands |
| `/boot` | Boot-related files |
| `/dev` | Device interfaces |
| `/proc` | Processes/kernel information |
| `/sys` | Hardware/kernel interfaces |
| `/run` | Runtime state |
| `/mnt` | Common temporary mount point |
| `/media` | Removable media |
| `/opt` | Optional software |
| `/srv` | Service data |

---

# 24. Absolute Paths

An absolute path starts from `/`.

Examples:

```text
/home/rajat/Documents
/etc/passwd
/var/log
```

Example:

```bash
cat /etc/hostname
```

The path is interpreted from the filesystem root:

```text
/
└── etc
    └── hostname
```

---

# 25. Relative Paths

A relative path is interpreted from your **current directory**.

Suppose:

```bash
pwd
```

returns:

```text
/home/rajat
```

and:

```text
/home/rajat
├── Documents
├── Downloads
└── Projects
```

Then:

```bash
cd Documents
```

means:

```text
/home/rajat/Documents
```

---

# 26. Absolute vs Relative Example

Suppose you are currently in:

```text
/home/rajat
```

These can reach the same location:

```bash
cd /home/rajat/Documents
```

Absolute path.

```bash
cd Documents
```

Relative path.

---

# 27. `.` — Current Directory

A single dot means:

```text
.
```

Current directory.

Example:

```bash
ls .
```

is equivalent to:

```bash
ls
```

And:

```bash
cd .
```

keeps you in the same directory.

---

# 28. `..` — Parent Directory

Two dots mean:

```text
..
```

Parent directory.

Suppose:

```text
/home/rajat/Documents
```

Run:

```bash
cd ..
```

Now:

```text
/home/rajat
```

Again:

```bash
cd ..
```

Now:

```text
/home
```

Again:

```bash
cd ..
```

Now:

```text
/
```

---

# 29. The Four Symbols You Must Know

Memorize:

```text
/   → filesystem root
~   → current user's home
.   → current directory
..  → parent directory
```

These appear constantly in Linux and cybersecurity.

---

# 30. Navigation Example

```bash
cd ~
pwd
```

Example:

```text
/home/rajat
```

Go into Documents:

```bash
cd Documents
pwd
```

Output:

```text
/home/rajat/Documents
```

Go back:

```bash
cd ..
pwd
```

Output:

```text
/home/rajat
```

Go to root:

```bash
cd /
pwd
```

Output:

```text
/
```

Go directly to logs:

```bash
cd /var/log
pwd
```

Output:

```text
/var/log
```

---

# 31. Hidden Files

Linux normally hides files and directories whose names begin with `.`.

Examples:

```text
.bashrc
.profile
.ssh
```

Run:

```bash
ls
```

They may not appear.

Run:

```bash
ls -a
```

They appear.

For detailed information:

```bash
ls -la
```

Example:

```text
.
..
.bashrc
.profile
.ssh
Documents
Downloads
```

Remember:

```text
.  → current directory
.. → parent directory
```

---

# 32. Why Hidden Files Matter in Cybersecurity

Hidden files are not automatically secret or malicious.

They are simply files whose names begin with `.`.

For example:

```text
/home/user
├── notes.txt
├── password.txt
└── .secret
```

This:

```bash
ls
```

may not show `.secret`.

This:

```bash
ls -la
```

will.

This kind of awareness is useful in CTFs and **OverTheWire Bandit**.

---

# 33. `file` — Identify a File

The `file` command identifies the type of data in a file.

Example:

```bash
file /etc/passwd
```

You may see:

```text
/etc/passwd: ASCII text
```

Try:

```bash
file /bin/ls
```

The output will describe the executable.

### Why this matters

A filename can be misleading.

For example:

```text
secret.txt
```

does not guarantee that it contains plain text.

Use:

```bash
file secret.txt
```

to investigate.

---

# 34. `stat` — File Metadata

`stat` provides detailed metadata.

Try:

```bash
stat /etc/passwd
```

You may see:

```text
File
Size
Blocks
Inode
Links
Access
Uid
Gid
Access time
Modify time
Change time
```

For now, remember:

```text
stat → detailed metadata about a filesystem object
```

---

# 35. Inodes

Linux filesystems use an **inode** to store metadata about filesystem objects.

Try:

```bash
ls -li
```

Example:

```text
123456 -rw-r--r-- 1 rajat rajat 1200 notes.txt
```

The first number is the inode number.

An inode is associated with information such as:

- file type
- permissions
- owner
- group
- size
- timestamps
- links

You will study this in more depth later.

---

# 36. Symbolic Links

A symbolic link points to another path.

You may see:

```text
/bin -> usr/bin
```

The arrow indicates a symbolic link.

Check:

```bash
ls -ld /bin
```

Symbolic links become important in:

- system administration
- software management
- configuration
- security
- privilege escalation concepts

---

# 37. Filesystem Investigation Example

Imagine you are investigating a Linux machine.

### Who are the users?

```bash
cat /etc/passwd
```

### What OS is installed?

```bash
cat /etc/os-release
```

### What logs exist?

```bash
ls -lah /var/log
```

### What temporary files exist?

```bash
ls -lah /tmp
```

### What processes exist?

```bash
ls /proc
```

### What is in the user's home?

```bash
ls -la ~
```

This is the beginning of a Linux investigation workflow.

---

# 🧪 Practical Lab

Perform these commands in your Linux VM.

## Step 1 — Start at home

```bash
cd ~
pwd
```

Record the output.

## Step 2 — Explore root

```bash
cd /
pwd
ls -la
```

## Step 3 — Explore `/etc`

```bash
cd /etc
pwd
ls -la
cat /etc/os-release
```

## Step 4 — Explore logs

```bash
cd /var/log
pwd
ls -lah
```

## Step 5 — Explore `/tmp`

```bash
cd /tmp
pwd
ls -lah
touch linux-day2-test.txt
ls -l linux-day2-test.txt
file linux-day2-test.txt
stat linux-day2-test.txt
rm linux-day2-test.txt
```

## Step 6 — Explore `/proc`

```bash
cd /proc
ls | head
cat /proc/cpuinfo
cat /proc/meminfo
```

## Step 7 — Explore `/dev`

```bash
ls /dev | head -30
echo "Hello Linux" > /dev/null
```

## Step 8 — Return home

```bash
cd ~
pwd
```

---

# 🔥 Day 02 Challenge

Try these **without looking at the answers**.

### Challenge 1

Go to `/` and list everything, including hidden entries.

### Challenge 2

Find your home directory using `~` and verify it with `pwd`.

### Challenge 3

From your home directory, navigate to `/tmp` using a relative path. Do not simply use `cd /tmp`.

### Challenge 4

From `/tmp`, reach `/` using parent-directory navigation.

### Challenge 5

Find at least three hidden files/directories in your home directory.

### Challenge 6

Find your Linux distribution.

Hint:

```text
/etc/
```

### Challenge 7

Find information about your CPU.

Hint:

```text
/proc/
```

### Challenge 8

Determine the type of:

```text
/etc/passwd
```

Use:

```bash
file /etc/passwd
```

### Challenge 9

Display detailed metadata for:

```text
/etc/passwd
```

Use:

```bash
stat /etc/passwd
```

### Challenge 10 — Bandit Preparation

You are currently in:

```text
/home/rajat/projects/security/labs
```

Without using an absolute path, move to:

```text
/home/rajat
```

Hint: use `..`.

---

# 🧠 Knowledge Check

Answer these without looking back:

1. What does `/` represent?
2. What is the difference between `/` and `/root`?
3. What does `~` represent?
4. What does `.` represent?
5. What does `..` represent?
6. What is `/home` used for?
7. What is `/etc` used for?
8. Where are Linux logs commonly stored?
9. What is `/tmp`?
10. What is `/dev`?
11. What is `/proc`?
12. What is `/sys`?
13. What is the difference between absolute and relative paths?
14. How do you display hidden files?
15. What does `file` do?
16. What does `stat` do?
17. What is an inode?
18. Why is `/etc` important for security?
19. Why can `/var/log` be useful during investigation?
20. Why is understanding paths important for Bandit?

---

# 🛠️ Troubleshooting

## `No such file or directory`

Check where you are:

```bash
pwd
```

Then inspect the directory:

```bash
ls
```

For example:

```bash
ls /var
ls /var/log
```

## `Permission denied`

Check:

```bash
ls -l <file>
```

Do not immediately use `sudo`. First understand why permission was denied.

Permissions will be covered in detail later.

## Lost in the filesystem?

Use:

```bash
pwd
ls -la
```

To return home:

```bash
cd ~
```

---

# 🎯 Day 02 Must-Know Commands

```bash
pwd
ls
ls -l
ls -a
ls -la
ls -lh
cd
cd ~
cd ..
cd /
cat
file
stat
```

Must-know concepts:

```text
/       → filesystem root
~       → user's home
.       → current directory
..      → parent directory

/home   → users
/etc    → configuration
/var    → variable data
/tmp    → temporary files
/usr    → programs/resources
/boot   → boot files
/dev    → devices
/proc   → processes/kernel information
/sys    → hardware/kernel information
/root   → root user's home
```

---

# 🧪 Final Day 02 Test

Complete this sequence without looking at the lesson:

```bash
cd /
ls -la

cd /etc
cat os-release

cd /var/log
ls -lah

cd /tmp
pwd

touch day2-test.txt
file day2-test.txt
stat day2-test.txt
rm day2-test.txt

cd /proc
cat cpuinfo | head

cd /dev
ls | head

cd ~
pwd
ls -la
```

If you understand what each command does, you have a solid Day 02 foundation.

---

# 🔐 Why Day 02 Matters for Cybersecurity

Later you will constantly encounter paths such as:

```text
/etc/passwd
/etc/shadow
/etc/ssh/
/etc/hosts
/var/log/
/tmp/
/home/user/
/home/user/.ssh/
/proc/
/dev/
```

For example:

```text
/var/log/auth.log
```

can be mentally broken down as:

```text
/          → filesystem root
var        → variable system data
log        → log directory
auth.log   → authentication-related log
```

Filesystem knowledge becomes useful in:

- Linux administration
- CTFs
- OverTheWire Bandit
- system investigation
- incident response
- privilege escalation
- malware analysis
- Bash scripting
- server administration

---

# ✅ Completion Checklist

- [ ] I understand the Linux filesystem tree.
- [ ] I understand `/`.
- [ ] I understand the difference between `/` and `/root`.
- [ ] I understand `/home`.
- [ ] I understand `/etc`.
- [ ] I understand `/var`.
- [ ] I understand `/tmp`.
- [ ] I understand `/usr`.
- [ ] I understand `/dev`.
- [ ] I understand `/proc`.
- [ ] I understand `/sys`.
- [ ] I understand absolute paths.
- [ ] I understand relative paths.
- [ ] I understand `~`.
- [ ] I understand `.`.
- [ ] I understand `..`.
- [ ] I can find hidden files.
- [ ] I can use `file`.
- [ ] I can use `stat`.
- [ ] I completed the practical lab.
- [ ] I completed the challenges.
- [ ] I can explain the major filesystem directories.
- [ ] I can navigate Linux without constantly getting lost.

---

# 🏆 Day 02 Complete

If you can complete the lab and challenges without blindly copying commands, move to:

## ➡️ Day 03 — Essential Linux Commands

Day 03 will go deeper into:

```text
cat
less
head
tail
grep
find
locate
which
whereis
echo
touch
cp
mv
rm
mkdir
```

These commands will become part of your everyday Linux and cybersecurity toolkit.

---

## 📚 Learning Flow

```text
📖 Learn
   ↓
💻 Run the examples
   ↓
🧪 Complete the lab
   ↓
🔥 Solve the challenges
   ↓
🧠 Answer the knowledge check
   ↓
🛠️ Troubleshoot
   ↓
📝 Document what you learned
   ↓
✅ Complete the checklist
   ↓
➡️ Continue to Day 03
```

> **Rule:** Don't just memorize Linux commands. Understand **what the command does, where you are, and why the path works.**
