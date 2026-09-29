# 🐧 Day 03 — Essential Linux Commands

> Learn the commands you will use constantly in Linux, system administration, and cybersecurity.

---

## 🎯 Learning Objectives

By the end of Day 03, you should be able to:

- [ ] Navigate the Linux filesystem
- [ ] Create, copy, move, and delete files
- [ ] Read file contents
- [ ] Search for files and text
- [ ] Get basic system information
- [ ] Use Linux documentation and command history

---

## 📚 1. File & Directory Commands

| Command | Purpose |
|---|---|
| `ls` | List files |
| `ls -l` | Detailed listing |
| `ls -la` | Include hidden files |
| `pwd` | Show current directory |
| `cd` | Change directory |
| `mkdir` | Create directory |
| `touch` | Create empty file |
| `cp` | Copy files |
| `mv` | Move / rename files |
| `rm` | Remove files |
| `rm -r` | Remove directories |

### Example

```bash
mkdir practice
cd practice
touch file.txt
cp file.txt backup.txt
mv backup.txt copy.txt
ls -la
```

---

## 📄 2. Reading Files

```bash
cat file.txt
less file.txt
head file.txt
tail file.txt
```

- `cat` → Display file
- `less` → Read large files
- `head` → Beginning of file
- `tail` → End of file

---

## 🔍 3. Searching

### Find Files

```bash
find . -name "file.txt"
find . -name "*.txt"
```

### Search Text

```bash
grep "Linux" file.txt
grep -r "Linux" .
```

---

## ⚙️ 4. System Information

```bash
whoami
id
hostname
uname -a
date
```

| Command | Purpose |
|---|---|
| `whoami` | Current user |
| `id` | User and group information |
| `hostname` | System hostname |
| `uname -a` | Kernel/system information |
| `date` | Current date and time |

---

## 🆘 5. Getting Help

```bash
man ls
ls --help
history
which ls
```

- `man` → Manual/documentation
- `--help` → Quick command help
- `history` → Previous commands
- `which` → Command location

---

# 🧪 Practical Lab

Run these commands yourself:

```bash
mkdir day3
cd day3

touch notes.txt
echo "Linux is powerful" > notes.txt

cat notes.txt

cp notes.txt backup.txt
mv backup.txt copy.txt

ls -la

grep "Linux" notes.txt
find . -name "*.txt"

whoami
hostname
uname -a

cd ..
rm -r day3
```

---

# 🔥 Day 03 Challenge

Create a directory called:

```text
linux-challenge
```

Inside it:

1. Create 3 files.
2. Put different text in each file.
3. Copy one file.
4. Rename one file.
5. Find a specific file using `find`.
6. Search for specific text using `grep`.
7. Display the files.
8. Delete the entire directory.

### Checklist

- [ ] Created directory
- [ ] Created 3 files
- [ ] Added text
- [ ] Copied a file
- [ ] Renamed a file
- [ ] Used `find`
- [ ] Used `grep`
- [ ] Deleted directory

---

# 🧠 Command Structure

Most Linux commands follow:

```text
command + options + arguments
```

Example:

```bash
ls -la /home
```

```text
ls       → Command
-la      → Options
/home    → Argument
```

---

# 📝 Knowledge Check

1. What does `pwd` show?
2. Difference between `ls` and `ls -la`?
3. How do you create a directory?
4. How do you create an empty file?
5. How do you copy a file?
6. How can `mv` rename a file?
7. What does `rm -r` do?
8. What is `grep` used for?
9. What is `find` used for?
10. What does `whoami` show?
11. How do you find the location of a command?
12. How do you access a command's manual?

---

# 🛠️ Troubleshooting

```bash
which <command>
<command> --help
man <command>
pwd
ls -la
```

---

# 🔑 Key Takeaways

```text
ls       → List
cd       → Navigate
pwd      → Current location
mkdir    → Create directory
touch    → Create file
cp       → Copy
mv       → Move / Rename
rm       → Remove
cat      → Read
find     → Find files
grep     → Search text
whoami   → Current user
man      → Manual
```

These commands form the foundation of everyday Linux usage and will be used repeatedly in **OverTheWire Bandit and cybersecurity labs**.

---

# ✅ Day 03 Completion

- [ ] Read the concepts
- [ ] Practiced the commands
- [ ] Completed the practical lab
- [ ] Completed the challenge
- [ ] Completed the knowledge check
- [ ] Can use `find` and `grep`
- [ ] Can manipulate files without help

---

## 🎉 Day 03 Complete

**Next:** [Day 04 — Files & Directories](../Day-04-Files-Directories/)
